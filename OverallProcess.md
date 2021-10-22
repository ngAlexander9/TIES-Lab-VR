# Overall Process Steps

## Leica BLK360 Scanner

1. Use Leica scanner to take scans of desired locations

See leica.md for additional considerations and references regarding producing higher quality scans

## Leica's Cyclone REGISTER Software

1. Connect to Leica scanner through Cyclone software and import scans to project
2. Ensure scans are properly oriented, use automatic alignment if possible
3. Export scans as point cloud (.e57, .ptx) *May take a long time to process*

## Cloud Compare

1. Import point cloud file
2. Inspect point cloud for fidelity
3. Merge scans as required
4. Clean unwanted points from point cloud
5. Segment point cloud into rooms for better mesh generation
6. Export point cloud as .ply

See CloudCompareProcess.md for additional considerations and references

## Meshlab

1. Import .ply point cloud file
2. Simplify point cloud
3. Compute normals
4. Generate mesh with poisson surface reconstruction
5. Generate texture for mesh using point color data
6. Export mesh, texture, and material files as .obj, .png, and .mtl

See MeshlabProcess.md for additional considerations and references

## Import .obj into Unreal/Unity
