# Dynamic Content Engineering Details<a name="cloud-canvas-cloud-gem-dc-engineering"></a>

This topic provides programmatic details about the dynamic content update process\. This includes manifest file information, Dynamic Content Cloud Gem EBus events, and Dynamic Content Cloud Gem service API\. For information about the `lmbr_aws` CLI extensions enabled by the Dynamic Content Cloud Gem, see [Using lmbr\_aws for Dynamic Content](cloud-canvas-cloud-gem-dc-lmbr-aws.md)\.

## Manifest File<a name="cloud-canvas-cloud-gem-dc-engineering-manifest-file"></a>

In your Lumberyard installation, the default location of the manifest file is `<GameFolder>/AWS/DynamicContent/DynamicContentManifest.json`\.

The following is a simple example manifest for the `SamplesProject` `DontDie` sample\.

```
"Files": [
{
"hash": "3bebdb5bdb8cff74642e5f7f3dc4e900", 
"outputRoot": "@user@", 
"bucketPrefix": "static-data", 
"keyName": "gameproperties.csv", 
"cacheRoot": "@assets@", 
"platformType": "", 
"localFolder": "staticdata/csv"
}
]
```

The following table describes the properties in the manifest file\.


****  

| Property | Description | 
| --- | --- | 
| hash | MD5 hash of the file\. | 
| outputRoot | Base output directory\. | 
| bucketPrefix | Prefix inside the bucket for the file | 
| keyName | Name of the file key in the bucket, which will be appended to the beginning of the hash\. The final key name has the format bucketPrefix/keyName\. | 
| cacheRoot | Root directory to search for copies of the outdated file asset\. | 
| platformType | Windows \(pc\), macOS \(osx\_gl\), or Linux \(linux\)\. An empty value specifies all operating systems\. | 
| localFolder | Directory to write locally within the outputRoot\. The full output has the format outputRoot/localFolder/keyName\. | 

## EBus Events<a name="cloud-canvas-cloud-gem-dc-engineering-ebus-events"></a>

The Dynamic Content Cloud Gem provides an EBus API and includes calls exposed to Lua\. The basic top\-level update request looks like this:

```
EBUS_EVENT_RESULT(requestSuccess,
      CloudCanvas::DynamicContent::DynamicContentRequestBus,
      RequestManifest, manifestName)
```

`requestSuccess (bool)` – Specifies whether the request was successfully sent\.

`manifestName(char*)` – Specifies the plaintext name of the manifest \(for example, `DynamicContentTest.json`\)\. The system handles `.pak` file and operating system naming conventions \(for example, `DynamicContentTest.shared.pak`\)\.

### Manifest Received<a name="cloud-canvas-cloud-gem-dc-engineering-manifest-received"></a>

The following EBus events are triggered when a manifest has been received successfully or unsuccessfully\.

#### Success<a name="cloud-canvas-cloud-gem-dc-engineering-manifest-received-success"></a>

```
EBUS_EVENT(CloudCanvas::DynamicContent::DynamicContentRequestBus, ManifestUpdated, bucketName, bucketPrefix)
```

When all `.pak` files are complete, a `RequestCompleted` event is broadcast\.

#### Failure<a name="cloud-canvas-cloud-gem-dc-engineering-manifest-received-failure"></a>

```
EBUS_EVENT(CloudCanvas::DynamicContent::DynamicContentRequestBus, ManifestFailed, bucketName, bucketPrefix, errorStr)
```

## Service API<a name="cloud-canvas-cloud-gem-dc-engineering-serviceapi"></a>

The Dynamic Content Cloud Gem exposes API calls through Amazon API Gateway for both the Cloud Gem Portal and the game client\.

The following tables list the calls for the portal\.


****  

| Portal API Call | Description | 
| --- | --- | 
| /service/status GET  | Returns the service's status\. | 
| /portal/info/\{file\_name\} GET  | Return detailed information about a specific file\. This includes the file's name, staging status, staging start and end dates \(optional\), and parent \(optional\)\. | 
| /portal/info/\{file\_name\} DELETE  | Request deletion of an existing item from the bucket and table\. | 
| /portal/content GET  | Request the list of files to display in the web portal\. | 
| /portal/content DELETE  | Request to deletion of all content from the bucket and staging table\. | 
| /portal/content POST  | Request alteration of the staging settings on a provided list of files\. | 

The following table lists the calls for the client\.


****  

| Client API Call | Description | 
| --- | --- | 
| /client/content POST | Request presigned URLs for a list of files\. Returns the URLs or a failure message\. | 