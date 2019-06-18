# Upgrading Decal Components<a name="upgrade-decal-component"></a>

Lumberyard 1\.5 introduces improvements to the decal component\. These changes may affect the rendering of legacy and pre\-1\.5 decal components\. Manually check each existing decal to ensure that they are rendering as intended, and that attributes are set correctly\.

The following changes to the decal component were made for Lumberyard 1\.5:
+ Projection type **OnStaticObjects** has been removed
+ The decal component now has the following projection types:
  + **Planar** \(forward rendered\)
  + **On Terrain** \(forward rendered\)
  + **On Terrain and Static Objects** \(deferred rendered\)

Use the following procedure to run a script that aids you in upgrading your legacy decals from Lumberyard 1\.4 and earlier to Lumberyard 1\.5 and later\.

**To run the legacy decal upgrade script**

1. Create a backup of the project\(s\) for which you intend to run this script\. Once you run this script, you cannot back out of the changes it performs\. To protect against the loss of data, be sure to perform this step\.

1. Download the [script](https://gamedev.amazon.com/forums/storage/attachments/3218-fixdecalspy27v2.zip)\. Extract it to Lumberyard's `\dev` directory\.

1. Open a command prompt\. Navigate to Lumberyard's `dev` directory\.

1. Use the Lumberyard bundled version of python to execute the script on your project or your project’s level\.

   For example:
   + `\dev\Tools\Python\2.7.11\windows\python.exe FixDecalsPy27.py D:\Lumberyard\1.6.0.0\dev\BeachCity`
   + `\dev\Tools\Python\2.7.11\windows\python.exe FixDecalsPy27.py D:\Lumberyard\1.6.0.0\dev\BeachCity\Levels\BeachCity_NightTime`
   + `\dev\Tools\Python\2.7.11\windows\python.exe FixDecalsPy27.py D:\Lumberyard\1.6.0.0\dev\BeachCity\Levels\BeachCity_NightTime\levels\Layers\`