# Serialize and deserialize JSON objects<a name="serialization-json-serialize-deserialize"></a>

 Once a class has been [registered with a serialization context](serialization-register-objects.md) objects of that class can be serialized and deserialized\. Objects are serialized to JSON with the `AZ::JsonSerialization::Store()` function, and deserialized from JSON with `AZ::JsonSerialization::Load()`\. 

 This article includes reference for these methods, examples of using serialization and deserialization, and how to interpret result codes from JSON the serializer\. For information on how specific types are serialized, see [Data types in serialized JSON](serialization-json-data-types.md)\. 

## Serialization<a name="serialization-json-serialize"></a>

Serialization into JSON is done with the `static AZ::JsonSerialization::Store()` method\. This method has several overloads, depending on how you want the object to be serialized and what information is available at the time of serialization\. By default, the global serialization context is used\.


**AZ::JsonSerialization::Store\(\) overloads**  

|  |  | 
| --- |--- |
|  <pre>template<typename T><br />static AZ::JsonSerializationResult::ResultCode<br />AZ::JsonSerialization::Store(rapidjson::Value& output,<br />    rapidjson::Document::AllocatorType& allocator, <br />    const T& object, <br />    AZ::JsonSerializerSettings settings = AZ::JsonSerializerSettings{});</pre>  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/serialization-json-serialize-deserialize.html)  | 
|  <pre>template<typename T><br />static AZ::JsonSerializationResult::ResultCode<br />AZ::JsonSerialization::Store(rapidjson::Value& output,<br />    rapidjson::Document::AllocatorType& allocator,<br />    const T& object,<br />    const T& defaultObject,<br />    AZ::JsonSerializerSettings settings = AZ::JsonSerializerSettings{});</pre>  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/serialization-json-serialize-deserialize.html) | 
|  <pre>static AZ::JsonSerializationResult::ResultCode<br />AZ::JsonSerialization::Store(rapidjson::Value& output,<br />    rapidjson::Document::AllocatorType& allocator,<br />    const void* object,<br />    const void* defaultObject,<br />    const AZ::Uuid& objectType, <br />    AZ::JsonSerializerSettings settings = AZ::JsonSerializerSettings{});</pre>  | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/serialization-json-serialize-deserialize.html) | 

The behavior of the `AZ::JsonSerialization::Store()` methods can be controlled by setting an instance of `AZ::JsonSerializerSettings` as the `settings` argument\.


**AZ::JsonSerializerSettings**  

|  |  | 
| --- |--- |
| bool m\_keepDefaults | If true, then defaults are written to the JSON value when serialized\.*Default*: `false` | 
| AZ::SerializeContext\* m\_serializeContext | The serialization context to query for information about how to serialize the provided object\.*Default*: The global seralization context retrieved from the `ComponentApplicationBus` event bus\. | 
| AZ::JsonSerializationResult::JsonIssueCallback m\_reporting | Callback method invoked when an error is encountered during serialization\. This function has no access to the object being serialized or the JSON value being written to, but can be used for altering result codes\.*Default*: The default issue reporter, which logs warnings and errors encountered in serialization\. | 
| AZ::JsonRegistrationContext\* m\_registrationContext | JSON registration context\. For examples of how to use a custom JSON context, see the source code\. *Default*: The global registration context retrieved from the event bus\.  | 

**Example Serialization example**  
The following is a short example demonstrating how to serialize a simple class\. Details regarding registering the class with the serialization context are omitted\.  

```
class SerializableClass
{
    double  m_var1;
    int     m_var2;
}

// ... Register with serialization context

SerializableClass instance;
instance.m_var1 = 42.0;
instance.m_var2 = 88;
 
rapidjson::Document document;
AZ::JsonSerializationResult::ResultCode result = AZ::JsonSerialization::Store(document, document.GetAllocator(), instance);
if (result.GetProcessing() == AZ::JsonSerializationResult::Processing::Halted)
{
    AZ_Warning("Serialization", false,
        "Unable to fully serialize SerializableClass to json because %s.",
        result.ToString().c_str());
}
 
rapidjson::StringBuffer buffer;
rapidjson::Writer<decltype(buffer)> writer(buffer);
document.Accept(writer);
AZ_TracePrintf("Serialization", "SerializableClass as Json:\n%s", buffer.GetString());
```

## Deserialization<a name="serialization-json-deserialize"></a>

Deserialization from JSON into an object is done with the `static AZ::JsonSerialization::Load()` method\. This method has two overloads \- one for use when an instance of the deserialized object type is available, and the other using `void*` and RTTI information\.


**AZ::JsonSerialization::Load\(\) overloads**  

|  |  | 
| --- |--- |
|  <pre>template<typename T><br />static AZ::JsonSerializationResult::ResultCode<br />AZ::JsonSerialization::Load(T& object,<br />    const rapidjson::Value& root,<br />    AZ::JsonDeserializerSettings settings = AZ::JsonDeserializerSettings{});</pre>  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/serialization-json-serialize-deserialize.html)  | 
|  <pre>static AZ::JsonSerializationResult::ResultCode<br />AZ::JsonSerialization::Load(void* object,<br />    const AZ::Uuid& objectType,<br />    const rapidjson::Value& root,<br />    AZ::JsonDeserializerSettings settings = AZ::JsonDeserializerSettings{});</pre>  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/serialization-json-serialize-deserialize.html)  | 

The behavior of the `AZ::JsonSerialization::Load()` methods can be controlled by setting an instance of `AZ::JsonDeserializerSettings` as the `settings` argument\.


**AZ::JsonDeserializerSettings**  

|  |  | 
| --- |--- |
| bool m\_clearContainers | If true, then container members of the target object to deserialize into are cleared before beginning deserialization\. This option has no effect for classes with a fixed layout\. *Default*: `false`  | 
| AZ::SerializeContext\* m\_serializeContext | The serialization context to query for information about how to deserialize to the object\.*Default*: The global seralization context retrieved from the `ComponentApplicationBus` event bus\. | 
| AZ::JsonSerializationResult::JsonIssueCallback m\_reporting | Callback method invoked when an error is encountered during deserialization\. This function has no access to the object being serialized or the JSON value being written to, but can be used for altering result codes\.*Default*: The default issue reporter, which logs warnings and errors encountered in deserialization\. | 
| AZ::JsonRegistrationContext\* m\_registrationContext | JSON registration context\. For examples of how to use a custom JSON context, see the source code\. *Default*: The global registration context retrieved from the event bus\.  | 

**Example Deserialization example**  
The following is a short example demonstrating how to deserialize\. Details regarding how to load JSON data into memory and registering with the serialization context are omitted\.  

```
rapidjson::Document document;
// ...read json document from file.
 
SerializableClass instance;
AZ::JsonSerializationResult::ResultCode result = AZ::JsonSerialization::Load(instance, document);
if (result.GetProcessing() == AZ::JsonSerializationResult::Processing::Halted)
{
    AZ_Warning("Deserialization", false,
        "Unable to fully deserialize SerializableClass from json because %s.",
        result.ToString().c_str());
}
```

## Result codes<a name="serialization-json-result-codes"></a>

 The JSON serializer uses the `AZ::JsonSerializationResult::ResultCode` type to report errors, warnings, and successful serialization and deserialization of objects\. Result codes are broken down into three parts: task, processing result, and final outcome\. These values can be obtained with the `GetTask()`, `GetProcessing()`, and `GetOutcome()` methods respectively\. When checking results, you should first start with the processing to see if the task was successfully completed or if an error was encountered\. For non\-`Success` values, the task indicates where in processing the error was encountered, and the outcome reflects why the failure occurred\. 

 To write serialization results to a string, use the `AZ::JsonSerializationResult::ResultCode::AppendToString()` and `AZ::JsonSerializationResult::ResultCode::ToString()`, or `AZ::JsonSerializationResult::ResultCode::ToOSString()` methods\. 


**Processing results**  

|  |  | 
| --- |--- |
| Completed | Processing completed successfully\. | 
| Altered | Processing completed after encountering an error\. Error recovery was performed, so the input and output will not necessarily match\. | 
| PartialAlter | Processing completed after encountering multiple errors, and was able to perform error recovery by making multiple alterations\. | 
| Halted | Processing failed and was unable to complete\. This indicates an unrecoverable error or other serious failure\. | 


**Tasks**  

|  |  | 
| --- |--- |
| RetrieveInfo | Retrieve information from the system, such as querying a serialization context\. | 
| CreateDefault | Creation of a default instance to use to provide default values during processing\. | 
| Convert | Type conversion between values\. | 
| Clear | Clearing a field or value\. | 
| ReadField | Reading a field from JSON to write to an object value\. | 
| WriteValue | Writing from an object value to a JSON field\. | 
| Merge | Merging two JSON values or documents together\. | 
| CreatePatch | Creation of a patch to transform one JSON value to another\. | 


**Outcomes**  

|  |  | 
| --- |--- |
| Success | The task completed successfully\. | 
| Skipped | The task skipped a field or value\. | 
| PartialSkip | The task skipped one or more fields while processing a JSON object or array\. | 
| DefaultsUsed | Task completed using only default values\. | 
| PartialDefaults | Task completed using defaults for some values\. | 
| Unavailable | Task tried to use space which isn't available\. | 
| Unsupported | An unsupported action was requested while performing the task\. | 
| TypeMismatch | The source and target were unrelated, and no type conversion could be performed\. | 
| TestFailed | A test check against a value failed\. | 
| Missing | A required field or value was missing\. | 
| Invalid | A field or element contained an invalid value\. | 
| Unknown | Unknown information was encountered during the task\. | 
| Catastrophic | An unidentifiable or unknown catastrophic error occurred during the task\. | 