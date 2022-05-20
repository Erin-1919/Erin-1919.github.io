---
title: "Esri ECCE Blog – Customized Script Tool in ArcGIS"
layout: post
---

This is a blog post on Esri ECCE website: [Handy Script Tool to Summarize Tree Characteristics within a Moving Search Window]( https://ecce.esri.ca/unb-blog/2019/03/11/handy-script-tool-to-summarize-tree-characteristics-within-a-moving-search-window/)

```
import arcpy
import pandas as pd

### Set the working envrionment
env = r"C:\EsriECCE\Blog"
arcpy.env.workspace = env
arcpy.env.overwriteOutput = True

### Obtain script parameter values
input_FC = arcpy.GetParameterAsText(0)
output_TB = arcpy.GetParameterAsText(1) #.xls
NeighborSize = arcpy.GetParameterAsText(2) # type in numbers with the unit as meter
Species = arcpy.GetParameterAsText(3) 

### Store treeIDs (FID) of input feature class into a list
tree_id = []
with arcpy.da.SearchCursor(input_FC, ["FID"]) as cursor:
    for row in cursor:
        tree_id.append(row[0])      

### Define the fuction with the parameter "tree_id" and "species" to calculate surrounding trees' characteristics
def statsfunction(tree_id,species):   
    whereclause1 = """ "FID" = %d """%(tree_id)
    whereclause2 = """"SpeClass" = '%s'"""%(species)
   
    arcpy.MakeFeatureLayer_management(input_FC, "Target", whereclause1)
    
    if species == "":
        # Select trees falling in the selected circular buffer according to their spatial location        
        arcpy.SelectLayerByLocation_management(in_layer = input_FC, 
                                               overlap_type="WITHIN_A_DISTANCE", 
                                               select_features = "Target", 
                                               search_distance = NeighborSize, 
                                               selection_type = "NEW_SELECTION", 
                                               invert_spatial_relationship="NOT_INVERT")
        
        arcpy.Statistics_analysis(in_table = input_FC, 
                                  out_table="C:/Users/think/Documents/ArcGIS/Default.gdb/Statistics",  
                                  statistics_fields="DBH MEAN;TreeHeight MEAN;BA SUM;CurOcDefo MEAN;CumOcDefo MEAN;OBJECTID COUNT")
    
    else:
        arcpy.MakeFeatureLayer_management(input_FC, "FiltedTrees", whereclause2)
        
        
        arcpy.SelectLayerByLocation_management(in_layer = "FiltedTrees", 
                                               overlap_type = "WITHIN_A_DISTANCE", 
                                               select_features = "Target", 
                                               search_distance = NeighborSize, 
                                               selection_type="NEW_SELECTION", 
                                               invert_spatial_relationship="NOT_INVERT")
          
        arcpy.Statistics_analysis(in_table = "FiltedTrees", 
                                  out_table="C:/Users/think/Documents/ArcGIS/Default.gdb/Statistics",  
                                  statistics_fields="DBH MEAN;TreeHeight MEAN;BA SUM;CurOcDefo MEAN;CumOcDefo MEAN;OBJECTID COUNT")
    
    Stats = [None]*6
    with arcpy.da.SearchCursor ("Statistics", ["MEAN_DBH","MEAN_TreeHeight","SUM_BA","MEAN_CurOcDefo","MEAN_CumOcDefo","COUNT_OBJECTID"]) as cursor: 
        
        ## For each row in cursor, assign the value in the list accordingly   
        for row in cursor:
            for i in range(6):
                Stats[i] = row[i]
        return Stats
        
### Prepare for the dataframe storing all returned records
Tree_list = pd.DataFrame(columns=["AvgDBH","AvgHeight","TotalBasalArea","AvgCurrentDefol","AvgCumulativeDefol","Count",], index=tree_id)  

### Call the function for each tree id
for tid in tree_id:
    temp_list = []
    STATS = statsfunction(tid,Species)
    temp_list += STATS[0:7]
    Tree_list.loc[tid] = temp_list

### Export the results and store them in an Excel file
Tree_list.to_excel(output_TB)

### Delet the table
arcpy.Delete_management("Statistics")
```
