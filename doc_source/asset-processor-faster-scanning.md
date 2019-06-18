# Enabling Asset Processor's Faster Scanning Mode<a name="asset-processor-faster-scanning"></a>

Asset Processor's **Faster Scanning Mode** speeds up Lumberyard's startup scan by disabling checking for cache changes that occurred while Asset Processor was not running\. This can save you time when processing many assets in your project\.

By default, **Faster Scanning Mode** is disabled\. You can enable or disable this mode any time without restarting the Asset Processor, including during the scan\. Asset Processor saves your preference between sessions\.

**To enable Faster Scanning Mode**

1. Open Asset Processor

1. Choose **Tools** and select **Faster Scanning Mode**\.   
![\[Enable Faster Scanning Mode in Asset Processor to process game assets quickly.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/shared-asset-processor-faster-scanning.png)

**To perform a full scan**

1. Clear **Faster Scanning Mode**\.

1. Do one of the following: 
   + Choose **Start Scan**\. This starts a full scan immediately, which checks for files missing from the cache and rebuilds the appropriate source files\.
   + Restart Lumberyard Editor\. Asset Processor runs a full scan automatically\.

Asset Processor's batch version also supports a command line parameter for **Faster Scanning Mode**\.

```
AssetProcessorBatch.exe --fastAnalysisMode
```

When you enable the feature you can also use console mode `stdout` as well as open GUI log windows that indicate the effectiveness of **Faster Scanning Mode**\. The output message displays the number of files that required full analysis and the total number of files\.

**Example**  

```
AssetProcessor: Builder optimization: 0 / 17589 files required full analysis, 542 sources found but not processed by anyone
```

In addition, Asset Processor indicates the number of files in your assets folders that are not recognized by any builder, such as `.p4ignore` or PSD files and other files not involved in asset processing\. Because these files barely impact performance \(several hundred files may take milliseconds in total\) this number is usually unimportant\. 

However, if this number is particularly large, consider examining your assets directories and adding exclusions to the `AssetProcessorPlatformConfig.ini` file\. You can exclude entire directories, which can be faster than analyzing whether or not they are being built\.

For more information, see [Configuring the Asset Pipeline](asset-pipeline-configuring.md)\.

## Performing a Full Scan<a name="asset-processor-full-scan"></a>

When you choose a full scan, Asset Processor performs the following actions\. Low cost actions contribute to less than 1% of the total time\.
+ \(Low\) Determines which builders are responsible for building a file\. Asset Processor examines builder patterns, such as `*.tif` or `*.fbx` when they register\.
+ \(Low\) Lookup the file in the database to determine what happened to it the previous time\.
+ \(Low\) Compares the new job fingerprints to the previously emitted jobs to check for differences\.
+ \(Moderate\) Generates a job fingerprint that includes modtimes of source files and dependencies and the versions of the involved builders\.
+ \(High\) Checks the cache directory and ensures that every product that was emitted last time for this source file is still present\.
+ \(Very high\) Sends the file to the registered builders so that they can spawn jobs for the job queue\.

If all of the following are true for a given source file found during the scan, then that file can be excluded from reanalysis\.
+ The source file hasn't changed on disk \(it has the same modtime as previously\)\.
+ The files on which the source file depends haven't changed on disk \(it has the same modtime as previously\)\.
+ The builders assigned to that source file successfully processed it last time\. This means there were no failures or errors\.
+ The builders assigned to that source file didn't get a new version or a new analysis fingerprint\.
+ There are no new builders that may operate on that source file\.
+ There are no builders that were previously enabled which could have operated on that source file but have since been removed\.
+ There are no builders that have changed the set of source files\.

Asset Processor performs a check at the beginning of the scan and does the following actions\. These actions are low cost\.
+ \(Very low\) Performs a narrow query into the database to determine when the fingerprint data for this file was previously processed\.
+ \(Very low\) Checks whether the source file in question had any version or analysis fingerprint changes by the builder\. Asset Processor compares the data to the previous processed time\.
+ \(Very low\) Gathers the modification times of the source file and any declared files on which it depended during the previous processing time\.
+ \(Very low\) Compares the modtime with the previously recorded time in the database\.
+ \(Low\) Gets the declared list of files on which the source file depended during the previous processing time\.

If any of these checks fail, the source goes through the normal, unchanged analysis pipeline\. This means that **Faster Scanning Mode** makes no changes to the actual analysis\.