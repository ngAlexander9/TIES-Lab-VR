# Cloud Compare Process

## Open Point Cloud in CloudCompare
- Load scan into CloudCompare **File->Open**

## Remove Unwanted Points from Scans
Sometimes the scanner will misregister points (due to reflection, transparent surfaces, etc.) - these points will need to be removed, or they will interfere with the mesh generation. It is easier to clean up the mesh in CloudCompare than in Meshlab.
- Select desired scan(s) in file tree (each point is registered to one scan, so the scan correlating the point to be removed need to be selected)
- Select segment tool (scissors in toolbar)
  - Use segment tool to select desired points
  - Click segment in to trim to selected points
  - Click Check mark to confirm
  - Scan will be split into .segmented and .remaining delete .remaining points (unwanted)
  - Repeat for all scans

## Merge Scans into One File for Meshlab
Once the scans have been cleaned, then export the scans in the correct format for Meshlab. 
- Select all prepared scans and merge them into one scan **Edit -> Merge**
  - Scans should combine into one scan file. You might see a prompt to generate a scalar field with original cloud index - this will assign each scan a different color. It does not affect the final cloud.
- In my experience, the simpler the cloud is, the easier it is to generate a mesh. I found it best to (following merging all the scans) segment each room/hallway as its individual cloud, then exporting each room as a separate .ply.
- Export merged scan as .ply **File->Save->Save as type .ply**

Use .ply in Meshlab to generate mesh.

## Additional Considerations
- Particularly large scans may require sufficient hardware to run. Specifically, when attempting this process with Leica's sample dataset (office-setting), CloudCompare would overload resources (either CPU or RAM) and crash, even on the TIES Lab workstation.
- Most unwanted points are distinct and easily separable from the main body of the room. However, some unwanted points may be inside the rest of the point cloud - it may be easier to temporarily segment out the walls/ceiling/floor of the cloud in order to isolate the unwanted points, then re-merge.
- It may help to view the cloud in 'real color'. Select the desired scan, and in the properties window, change the Colors entry to RGB.
- There seems to be tools to compute normals/generate meshes in CloudCompare, but in testing, proved to be very unstable. Meshlab process 
