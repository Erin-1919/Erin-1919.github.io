---
title: "Esri ECCE Blog: Customized Script Tool in ArcGIS"
layout: post
---

**I shared a blog post on the Esri Canada ECCE site detailing a Python script tool I developed for ArcGIS. The tool summarizes tree characteristics within a moving search window, making it easier to analyze spatial patterns in forest inventory data.**

## Summary of the Tool

The script uses ArcPy and pandas to automate the analysis of tree metrics such as diameter at breast height, height, basal area, and defoliation levels within a user-defined buffer around each tree. Users can filter by tree species and define the search radius. The tool outputs a summary table in Excel format, listing local statistics for each tree in the dataset.

The full blog post is available here:  
[Handy Script Tool to Summarize Tree Characteristics within a Moving Search Window](https://ecce.esri.ca/unb-blog/2019/03/11/handy-script-tool-to-summarize-tree-characteristics-within-a-moving-search-window/)

## Code Sample

Here is the full script used in the tool:

```python
import arcpy
import pandas as pd

# Set the working environment
env = r"C:\EsriECCE\Blog"
arcpy.env.workspace = env
arcpy.env.overwriteOutput = True

# Obtain script parameter values
input_FC = arcpy.GetParameterAsText(0)
output_TB = arcpy.GetParameterAsText(1)
NeighborSize = arcpy.GetParameterAsText(2)
Species = arcpy.GetParameterAsText(3)

# Store tree IDs (FID) in a list
tree_id = []
with arcpy.da.SearchCursor(input_FC, ["FID"]) as cursor:
    for row in cursor:
        tree_id.append(row[0])

# Define the function to compute statistics
def statsfunction(tree_id, species):
    whereclause1 = """ "FID" = %d """ % tree_id
    whereclause2 = """ "SpeClass" = '%s' """ % species

    arcpy.MakeFeatureLayer_management(input_FC, "Target", whereclause1)

    if species == "":
        arcpy.SelectLayerByLocation_management(
            in_layer=input_FC,
            overlap_type="WITHIN_A_DISTANCE",
            select_features="Target",
            search_distance=NeighborSize,
            selection_type="NEW_SELECTION",
            invert_spatial_relationship="NOT_INVERT",
        )
        arcpy.Statistics_analysis(
            in_table=input_FC,
            out_table="C:/Users/think/Documents/ArcGIS/Default.gdb/Statistics",
            statistics_fields="DBH MEAN;TreeHeight MEAN;BA SUM;CurOcDefo MEAN;CumOcDefo MEAN;OBJECTID COUNT",
        )
    else:
        arcpy.MakeFeatureLayer_management(input_FC, "FiltedTrees", whereclause2)
        arcpy.SelectLayerByLocation_management(
            in_layer="FiltedTrees",
            overlap_type="WITHIN_A_DISTANCE",
            select_features="Target",
            search_distance=NeighborSize,
            selection_type="NEW_SELECTION",
            invert_spatial_relationship="NOT_INVERT",
        )
        arcpy.Statistics_analysis(
            in_table="FiltedTrees",
            out_table="C:/Users/think/Documents/ArcGIS/Default.gdb/Statistics",
            statistics_fields="DBH MEAN;TreeHeight MEAN;BA SUM;CurOcDefo MEAN;CumOcDefo MEAN;OBJECTID COUNT",
        )

    Stats = [None] * 6
    with arcpy.da.SearchCursor("Statistics", ["MEAN_DBH", "MEAN_TreeHeight", "SUM_BA", "MEAN_CurOcDefo", "MEAN_CumOcDefo", "COUNT_OBJECTID"]) as cursor:
        for row in cursor:
            for i in range(6):
                Stats[i] = row[i]
        return Stats

# Prepare DataFrame to store results
Tree_list = pd.DataFrame(columns=["AvgDBH", "AvgHeight", "TotalBasalArea", "AvgCurrentDefol", "AvgCumulativeDefol", "Count"], index=tree_id)

# Loop through each tree and apply the function
for tid in tree_id:
    temp_list = []
    STATS = statsfunction(tid, Species)
    temp_list += STATS[0:7]
    Tree_list.loc[tid] = temp_list

# Export to Excel
Tree_list.to_excel(output_TB)

# Delete temporary statistics table
arcpy.Delete_management("Statistics")
