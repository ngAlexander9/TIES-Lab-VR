# MeshLab Process

## Import .ply Point Cloud File

- Import the pointcloud file as .ply into MeshLab **File -> Import Mesh**
- See [CloudCompareProcess.md](https://github.com/ngAlexander9/TIES-Lab-VR/blob/master/CloudCompareProcess.md) for details on generating a clean pointcloud

## Simplify Point Cloud and Compute Normals

- Reduce number of points for smooth remeshing.
  - **Filters -> Point Set -> Point Cloud Simplification**. Enter **Number of samples** to be ~5% of original number of points. Make sure **Best Sample Heuristic** is checked.
- Make sure the Simplified point cloud is selected in the Layer Dialog (right). It might be prudent to save this mesh as a file **File -> Export Mesh**. The file each layer is saved as is in the detail of the Layer Dialog (click the >). **Changes to layers are not saved until export mesh is run on that layer.**
- Compute normals **Filters -> Point Set -> Compute normals for point sets**. **Neighbor num** between 10-100, initially try 10. For **Smooth Iteration**, initially try 0 (5-10 may give better results).
- Make sure normals are properly computed by going to **Render -> Show Normal**. Should display many blue lines **If blue lines are on exterior of room, then normals need to be inverted (see below)**

## Generate Mesh with Poisson Surface Reconstruction

- **Filters -> Remeshing, Simplification and Reconstruction -> Surface Reconstruction: Screened Poisson**. Initially use default parameters, but can be adjusted.
  - This should create another layer called Poisson. Make sure this layer is selected for further operations
- The meshing may have created extra surfaces. To remove them, **Filters -> Selection -> Select Faces with edges longer than ...**. The default value is automatically computed. Click on apply. Delete faces by clicking on the delete face button (triangle face with three vertices with cross over it).
- Some noise may still persist. **Filters -> Cleaning and Repairing -> Remove isolated pieces (wrt Face Num.)**. Use the default value, and make sure **Remove unreferenced vertices** is checked 
- Final cleaning option **Filters -> Selection -> Select non Manifold Vertices**. Click apply. then click on delete face button.
- Additional cleaning of mesh can be manually done by using **Select Faces in a rectangular region**.
- It is a good idea at this stage to **Export Mesh** the poisson layer as .obj.

## Generate Texture for Mesh Using Point Color Data

- Convert the vertex color to a texture
  - **Filters -> Texture -> Per Vertex Texture Function**. Click apply.
  - **Filters -> Texture -> Convert PerVertex UV into PerWedge UV**. Click apply.
  - **Filters -> Texture -> Parametrization: trivial Per-triangle.**
    - Quads-per-line: 0
    - Texture Dimension: 5000 (maybe more, see below)
    - Inter-triangle border: 0 (maybe more, see below)
    - Method: Basic (sometimes Space-optimizing crashes)
    - Click apply.
  - **Filters -> Texture -> Transfer: Vertex Color to Texture**
    - Texture file: (file name for .png)
    - Texture width: Same as Texture Dimension
    - Texture height: Same as Texture Dimension
    - Check Assign texture and Fill texture
    - Click apply.
  - **Export mesh for changes to apply**
- There should now be three files generated: a .obj file (containing the mesh), a .png (containing the texture), and a .mtl (material file for joining them). These three files are used in Blender, Unity, Unreal, etc.

## Additional Considerations
- If the texture generated appears to have mis-colored borders around the triangles, one solution may be to increase the texture dimension size and inter-triangle border.
