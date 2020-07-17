# Lumberyard Asset File Types<a name="lumberyard-file-types"></a>

See the following tables for supported asset data file types in Lumberyard\.

Lumberyard supports the `.xml` file format and the following image file formats:
+ `.bmp`
+ `.jpg`
+ `.pgm`
+ `.png`
+ `.raw`
+ `.r16`
+ `.tga`
+ `.tif`

**3D Art Asset File Types**

The following file formats are used for static geometry:


****  

| File Type | Where Created | Description | 
| --- | --- | --- | 
| \*\.cgf \(Static Geometry File\) | DCC tool | Contains static geometry data, such as grouped triangles, tangent spaces, vertex colors, physics data, and spherical harmonics data\. | 
| \*\.chr \(Character Asset File\) | DCC tool | The base character used for animations\. | 
| \*\.cdf \(Character Definition File\) | Lumberyard | Defines the base character and associated attachments\. This file is created with Geppetto and contains a reference to the \.chr file\. | 
| \*skin \(Character Skinned Render Mesh\) | DCC tool | Contains skinned character data, including the mesh, vertex weighting, vertex colors, and morph targets\. | 
| \*\.fbx \(Filmbox File\) | DCC Tool | Contains mesh, material, camera, and animation data\. Provides interoperability between DCC tools\. | 
| \*\.scenesettings \(Scene Settings File\) | Lumberyard | Contains configuration and rules settings from an \.fbx file\.  | 
| \*\.abc \(Alembic Cache File\) | DCC tool | Contains non\-procedural, application\-independent set of baked geometric data such as baked meshes and their materials\.  | 
| \*\.cax \(CAD/CAE Exchange File\) | Lumberyard | Contains compressed game assets read from the \.abc file and streamed in\-game on demand from disk\.  | 
| \*\.trb \(Terrain Block File\) | Lumberyard | Contains terrain data and associated level objects such as water and vegetation\.  | 

**Material and Texture File Types**

The following files are used for the **Material Editor**\. For more information, see [Working with shaders and materials](mat-intro.md)\.


****  

| File Type | Where Created | Description | 
| --- | --- | --- | 
| \*\.mtl \(Material File\) | DCC Tool |  Contains settings for shaders, surface types, and references to textures\.  | 
| \*\.dds \(DirectDraw Surface\) | DCC tool | Contains compressed source texture files\. | 
| \*\.sbsar \(Substance Files\) | Allegorithmic Substance Designer | Contains procedural materials\. | 

**Animation File Types**

The following file types are used for the **Animation Editor**\. For more information, see [Animation Editor File Types](char-animation-editor-file-types.md)\. 


****  

| File Type | Where Created | Description | 
| --- | --- | --- | 
| \*\.actor \(Actor File\) | DCC tool | A character with at least one bone\.  | 
| \*\.motion \(Motion File\) | DCC tool | Individual animation clips for a character, such as walk, run, and so on\. | 
| \*\.motionset \(Motion Set File\) | Lumberyard | Contains a list of motion files for a character\. For example, you can create a motion set named Run\.motionset that contains the run\.motion, sprint\.motion, and jog\.motion files\. | 
| \*\.animgraph \(Animation Graph File\) | Lumberyard | Contains the state machines, transitions, conditions, blend trees, and so on\. | 
| \*\.assetinfo \(Asset Info File\) | Lumberyard | Contains the configuration and settings for the \.actor and \.motion files\. Animation Editor and the FBX Settings tool can create this file\.  | 

The following file types are used for the Geppetto and Mannequin systems\. For more information on these file types, see [Character Animation Files](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/anim-char-file-types.html)\.


****  

| File Type | Where Created | Description | 
| --- | --- | --- | 
| \*\.adb \(Animation Database File\) | Lumberyard | The Mannequin system uses this file to store fragments and transitions\. This is typically referred to from the character Lua file and other systems such the hit death reaction system\.  | 
| \*\.i\_caf \(Intermediate Character Animation File\) | DCC tool | Contains the animated bone data for one or more characters in uncompressed format\. | 
| \*\.animsettings \(Animation Settings File\) | Lumberyard | Contains per\-animation compression settings\. This is a sidecar file that is stored next to the \.i\_caf file and describes how it should be compiled by the asset pipeline\. | 
| \*\.caf \(Character Animation File\) | Lumberyard | The compressed version of the intermediate \.i\_caf file\. Contains on\-demand asset data that is streamed in and out of the game as needed at runtime\.  | 
| \*\.chrparams \(Character Parameters File\) | Lumberyard | Contains skeletal characters\. This file has the same name as the \.chr file to which it refers to\. | 
| \*\.dba \(Animation Database\) | Lumberyard | Contains multiple compressed \.caf animation files that are streamed in and out of the game together\. Created by the Resource Compiler and defined in the \.chrparams file\. | 
| \*\.animevents \(Animation Events Database\) | Lumberyard | Stores a list of assets with timed event markups\. Geppetto creates this file, which is mapped to the \.chrparams file\. | 
| \*\.bspace \(Blend Space File\) | Lumberyard | Define how multiple animation assets are blended together\. Blend spaces are parameterized at runtime with movement parameters such as movement speed, movement direction, turning angle, or slope\. | 
| \*\.comb \(Blend Space Combination File\) | Lumberyard | Combines multiple blend spaces into one, usually of a higher order, and represents a multidimensional blend space\. | 
| \*\.grp \(Group Files\) | DCC Tool | Exported animation sequences used for track view sequences\. | 

**Audio Asset File Types**

The following file types are used for the audio system\. For more information, see [Adding Audio and Sound Effects](audio-intro.md)\.


****  

| File Type | Where Created | Description | 
| --- | --- | --- | 
| \*\.bnk \(Soundbank File\) | Audiokinetic Wwise | Contains compiled sound data and metadata\. | 
| \*\.wem \(Encoded Media File\) | Audiokinetic Wwise | Compiled streamable audio file\. | 