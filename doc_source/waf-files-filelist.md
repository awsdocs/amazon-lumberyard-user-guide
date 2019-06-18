# Waf File List \(\*\.waf\_files\)<a name="waf-files-filelist"></a>

Waf files are JSON\-based and used to represent all files in the build plus their uber file and the VisualStudioFilter\. By default, the uber file option is set to false\. When the uber option is false, all files are treated as individual compilation units\. `NoUberFile` is a fixed key that represents files that are individually compiled regardless of the uber file flag state\.

Files are organized hierarchically into three levels:
+ **Level 1 – Uber file target file**

  The first level represents the uber file designation for the source files that are defined in the group\. Uber file names must include the extension of the compilation types for the files defined\. Only \.cpp is supported\. You can use the reserved name **NoUberFile** to prevent grouping the files defined into a single uber file, regardless of the Uber File option setting\. 
+ **Level 2 – Visual Studio filter name**

  The second level represents the Visual Studio project filter, which helps organize files in the group into user\-defined folders and subfolders\. Folder filter names can be shared across multiple uber file groupings because the folder groupings are not tied to uber file grouping definitions\. The reserved name **root** represents the base of the project in the hierarchy\. 
+ **Level 3 – List of source files**

  The third level below each Visual Studio filter name group includes the source file names, relative to the current project folder\. 

The following is an example \*\.waf\_files content file used by CryFont:

```
{
    "CryFont_Uber_0.cpp":
    {
        "Source Files":
        [
            "CryFont.cpp",
            "FFont.cpp",
            "FFontXML.cpp",
            "FontRenderer.cpp",
            "FontTexture.cpp",
            "GlyphBitmap.cpp",
            "GlyphCache.cpp",
            "ICryFont.cpp",
            "NullFont.cpp"
        ],
        "Header Files":
        [
            "CryFont.h",
            "FFont.h",
            "FontRenderer.h",
            "FontTexture.h",
            "GlyphBitmap.h",
            "GlyphCache.h",
            "NullFont.h",
            "resource.h",
            "FBitmap.h",
            "StdAfx.h"
        ]
    },
    "NoUberFile":
    {
        "Root":
        [
            "StdAfx.cpp"
        ]
    }
}
```