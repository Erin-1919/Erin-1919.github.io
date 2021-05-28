---
title: "Esri ECCE Blog – R ArcGIS Bridge"
layout: post
---

This is a blog post on Esri ECCE website: [Modeling Line Features on DGGS Grids in the R-ArcGIS Environment](https://ecce.esri.ca/ucalgary-blog/2020/03/24/modeling-line-features-dggs-r-arcgis/)

### Step 1. Generate DGGS grids with three different configurations covering the study area in the R environment
```
# Load libraries
library(dggridR)
library(rgdal)
library(ggplot2)

# Read the dataset
dsn.road = "H:/MajorRoads.shp"
MajorRoads = readOGR(dsn.road, layer="MajorRoads")

# Visualize the dataset
ggplot() +
  geom_polygon(data=MajorRoads, aes(x=long, y=lat, group=group), size = 1, fill=NA, color="black") + 
  scale_y_continuous(name = "Longitude") + scale_x_continuous(name = "Latitude") +
  theme_classic() + coord_equal()

# Construct DGG objectS
dggs.ISEA4H.20 = dgconstruct(projection = "ISEA", aperture = 4, topology = "HEXAGON", res = 20, precision = 7)
dggs.ISEA4T.20 = dgconstruct(projection = "ISEA", aperture = 4, topology = "TRIANGLE", res = 20, precision = 7)
dggs.ISEA4D.20 = dgconstruct(projection = "ISEA", aperture = 4, topology = "DIAMOND", res = 20, precision = 7)

# Create DGGS grids and export as .shp files
dgshptogrid(dggs.ISEA4H.20, dsn.road, cellsize = 0.00001, 
            savegrid = "H:/Roads_ISEA4H_20.shp")
dgshptogrid(dggs.ISEA4T.20, dsn.road, cellsize = 0.00001, 
            savegrid = "H:/Roads_ISEA4T_20.shp")
dgshptogrid(dggs.ISEA4D.20, dsn.road, cellsize = 0.00001, 
            savegrid = "H:/Roads_ISEA4D_20.shp")
```

### Step 2. Detect grid cells representing individual roads in the ArcGIS Pro environment
```
## Set the working envrionment
env = r"H:\ECCE_Blog_2020Winter.gdb"
arcpy.env.workspace = env
arcpy.env.overwriteOutput = True

InputFeature  = "Roads_ISEA4H_20" # Roads_ISEA4T_20 / Roads_ISEA4D_20
SpatilJoinOutput = "Roads_ISEA4H_spjoin" # Roads_ISEA4T_spjoin / Roads_ISEA4D_spjoin

## Spatial join the grid shapefile and the road shapefile
arcpy.SpatialJoin_analysis(InputFeature, "MajorRoads", SpatilJoinOutput, "JOIN_ONE_TO_MANY", "KEEP_COMMON", '', "INTERSECT", None, '')

## Add fields to store latitude and longitude values
arcpy.AddField_management(SpatilJoinOutput, "longitude", "DOUBLE")
arcpy.AddField_management(SpatilJoinOutput, "latitude", "DOUBLE")

## Calculate latitude and longitude for the cell centroids
arcpy.management.CalculateGeometryAttributes(SpatilJoinOutput, "longitude CENTROID_X;latitude CENTROID_Y", '', '')
```

### Step 3. Calculate the new road length after conversion in the R environment
```
# Load libraries
library(arcgisbinding)
library(dplyr)
library(geosphere)

# Print information regarding the ArcGIS product and license
arc.check_product()

# Open the datasets
Rd.ISEA4H = arc.open("H:/ECCE_Blog_2020Winter.gdb/Roads_ISEA4H_spjoin")
Rd.ISEA4T = arc.open("H:/ECCE_Blog_2020Winter.gdb/Roads_ISEA4T_spjoin")
Rd.ISEA4D = arc.open("H:/ECCE_Blog_2020Winter.gdb/Roads_ISEA4D_spjoin")

# Create a new dataframe to store results
ISEA4H.df = ISEA4T.df = ISEA4D.df = data.frame(StreetID = integer(), ConvertLength = double())
# create a vector to store street ID
road.id = (0:8)

# Creat a function to calculate the road length after being converted on DGGS grids
# Two parameters included road ID and the input dataset with different grid types
polyline.length = function(roadid,inputdf){
  # Import the subsection of the attribute tables
  df = arc.select(object = inputdf, fields = c('JOIN_FID','Type','longitude','latitude'))
  # Select those cells corresponding to a specific road
  road.matrix = filter(df, (JOIN_FID == roadid))
  # If the road is west-east directed (type is Avenue) then sort cells by longitude firstly
  # If the road is north-south directed (type is not Avenue) then sort cells by latitude firstly
  if(road.matrix$Type[1] == "Avenue"){
    centroid.matrix = road.matrix[,c("longitude","latitude")][order(road.matrix$longitude, road.matrix$latitude),]
  } else {
    centroid.matrix = road.matrix[,c("longitude","latitude")][order(road.matrix$latitude, road.matrix$longitude),]
  }
  # Calculate the the length after conversion
  Convert.length = lengthLine(centroid.matrix)
  # Report the converted length
  results = c(roadid,Convert.length)
  return(results)
}

# Call the function in three loops
for (rid in road.id) {ISEA4H.df = rbind(ISEA4H.df, polyline.length(rid,Rd.ISEA4H))}
for (rid in road.id) {ISEA4T.df = rbind(ISEA4T.df, polyline.length(rid,Rd.ISEA4T))}
for (rid in road.id) {ISEA4D.df = rbind(ISEA4D.df, polyline.length(rid,Rd.ISEA4D))}

# Summary all info in a new data frame for comparison
ConvertSummary = data.frame(MajorRoads)
ConvertSummary$ISEA4HLength = ISEA4H.df[,2]
ConvertSummary$ISEA4TLength = ISEA4T.df[,2]
ConvertSummary$ISEA4DLength = ISEA4D.df[,2]
```
