# Importing Resource Definitions into Cloud Canvas<a name="cloud-canvas-ui-rm-resource-importer"></a>

You can use the Cloud Canvas resource importer to add definitions of existing AWS resources to a Cloud Canvas resource group\. You can add resources by using the Cloud Canvas Resource Manager in Lumberyard Editor or at a command line prompt\.

## Importing Resources using Lumberyard Editor<a name="cloud-canvas-ui-rm-resource-importer-ly-editor"></a>

In Lumberyard Editor, you can import a resource by specifying an [Amazon Resource Name \(ARN\)](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) or by choosing from a list\.

**To import a resource by using an ARN**

1. From the Lumberyard Editor top menu, choose **AWS**, **Cloud Canvas**, **Resource Manager**\.

1. In the navigation pane, select a resource group\.

1. In the detail window, click **Import resource**, **Import using ARN**\. You can also open the context \(right\-click\) menu for the resource in the navigation pane and choose **Import resource**, **Import using ARN**\.  
![\[Import using ARN\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/cloud_canvas/cloud-canvas-resource-importer-using-arn.png)

1. In the **Import using ARN** dialog box, provide the ARN and name of the resource that you are going to import\. Both are required\.  
![\[Provide the resource name and ARN\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/cloud_canvas/cloud-canvas-resource-importer-using-arn-dialog-box.png)

   After you have provided both items of information, the **Import** button is enabled\.

1.  **Import**\.

**To import a resource by choosing from a list**

1. From the Lumberyard Editor top menu, choose **AWS**, **Cloud Canvas**, **Resource Manager**\.

1. In the navigation pane, select a resource group\.

1. In the detail window, choose **Import resource**, **Import using ARN**\. You can also open the context \(right\-click\) menu for the resource in the navigation pane and choose **Import resource**, **Import using ARN**\.  
![\[Import from list\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/cloud_canvas/cloud-canvas-resource-importer-from-list-dialog-box.png)

1. In the **Import from list** dialog box, choose the AWS Region of the resource for **Region**\. The default value is the region of the project stack if it exists\. Resources start loading in the list as soon as you choose a region that has importable resources\.  
![\[Choose AWS Region\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/cloud_canvas/cloud-canvas-resource-importer-region-selector.png)

1. You can use the AWS service selector to filter the resources by service, and then use the **Search** box to filter resources by name\.  
![\[Filter by AWS service and resource name\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/cloud_canvas/cloud-canvas-resource-importer-filter-by-name-and-ddb.png)

1. Select the check box to the left of each resource that you want to import\.  
![\[Choose the resources to import\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/cloud_canvas/cloud-canvas-resource-importer-choose-resources.png)

1.  **Configure**\.

1. In the **Configuration** dialog box, provide a reference name for each resource, or accept the default\. The default name is the original name of the resource on AWS\.

1. To delete a selected resource from the list, open the context \(right\-click\) menu for the resource and choose **Delete**\.  
![\[Delete a resource\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/cloud_canvas/cloud-canvas-resource-importer-delete-selected-resource.png)

1. When you are ready, click **Import**\. A progress bar displays\. An **Import Error** message informs you of any errors that occur\.  
![\[Import progress\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/cloud_canvas/cloud-canvas-resource-importer-progress.png)

1. Click **X** to close the **Import from list dialog** box\. The resources that you imported are listed in the details pane of Cloud Canvas Resource Manager\.

## Importing Resource Definitions Using the Command Line<a name="cloud-canvas-ui-rm-resource-importer-command-line"></a>

To list and import resources using the Cloud Canvas command line, see [resource\-importer list\-importable\-resources](cloud-canvas-command-line.md#cloud-canvas-command-line-resource-importer-list-importable-resources) and [resource\-importer import\-resource](cloud-canvas-command-line.md#cloud-canvas-command-line-resource-importer-import-resource)\.

## Understanding Resource Definitions<a name="cloud-canvas-ui-rm-resource-importer-resource-definitions-caveat"></a>

When you use the Cloud Canvas resource importer to import the definition of a resource, it is important to understand that you are importing the resource's definition, not the resource itself\. For example, suppose you use the AWS console to create a high score table in DynamoDB called Table A\. You create a game client that uploads scores, and send out the client to your players\. Table A begins to populate with data from the players of your game\.

You then decide to use Cloud Canvas to manage your resources and deployments\. Using the Cloud Canvas Resource Manager, you import Table A because it has the exact configuration values that you want, and it has worked well for your use cases\.

When you create a deployment with the imported resource, the deployment contains Table B, which is a new table with Table A's structure but not its data\. Table B is managed by Cloud Canvas and has the same behavior as Table A\. However, Table B is not a reference to Table A, and it does not have Table A's data or history\. Keep this distinction in mind when you import resource definitions\.



## Automatically Imported Resource Definitions<a name="cloud-canvas-ui-rm-resource-importer-automatically-imported"></a>

Some of the existing resources that you select might be related to other resources\. For example, Lambda functions can respond to events from the selected triggers\. You can use event notifications from an Amazon S3 bucket to send alerts or trigger workflows\. Cloud Canvas imports the related resources for you automatically\.

Cloud Canvas uses the following naming conventions for automatically imported resource definitions\.


****  

|  Source  |  Naming Convention  |  Example Name of Imported Resource  | 
| --- | --- | --- | 
|  DynamoDB table, Lambda function, Amazon SNS topic, Amazon SQS queue  |  <resource\_name> \+ "AutoAdded" \+ <resource\_type> \+ <counter>  |  LambdaFunctionAutoAddedtable0  | 
|  Lambda function configuration resource??  |  <lambda\_function\_name> \+ "Configuration"  |  LambdaFunctionConfiguration  | 
|  Lambda function policy resource  |  <lambda\_function\_name> \+ "Permission"  |  LambdaFunctionPermission  | 
|  DynamoDB table Lambda function event source  |  <DynamoDB\_table\_name> \+ "EventSource"  |  DynamoTableEventSource  | 

## Resources Supported for Import<a name="cloud-canvas-ui-rm-resource-importer-resources-supported-for-import"></a>

The following sections list the resource attributes and related resources that Cloud Canvas imports for each supported AWS service\.

### Dynamo DB Tables<a name="w31aac23c28c25b7c26c13b5"></a>

For DynamoDB tables, Cloud Canvas imports the following resource attributes:
+ `AttributeDefinitions`
+ `GlobalSecondaryIndexes`
+ `KeySchema`
+ `LocalSecondaryIndexes`
+ `ProvisionedThroughput`
+ `StreamSpecification`

### Amazon S3 Buckets<a name="w31aac23c28c25b7c26c13b7"></a>

For Amazon S3 buckets, Cloud Canvas imports the following resource attributes:
+ `CorsConfiguration`
+ `LifecycleConfiguration`
+ `NotificationConfiguration`
+ `Tags`
+ `VersioningConfiguration`
+ `WebsiteConfiguration`

For Amazon S3 buckets, Cloud Canvas also imports the following related resources: 
+ Lambda functions
+ Amazon SQS queues
+ Amazon SNS topics

### Lambda Functions<a name="w31aac23c28c25b7c26c13b9"></a>

For Lambda functions, Cloud Canvas imports the following resource attributes: 
+ `Code`
+ `Description`
+ `Handler`
+ `MemorySize`
+ `Role`
+ `Runtime`
+ `Timeout`
+ `VpcConfig`

For Lambda functions, Cloud Canvas also imports the following related resources: 
+ Lambda function configurations 
+ Lambda function permissions 
+ DynamoDB tables 
+ Event source mappings 

### Amazon SNS Topics<a name="w31aac23c28c25b7c26c13c11"></a>

For Amazon SNS topics, Cloud Canvas imports the following resource attributes: 
+ `DisplayName`
+ `Subscription`

For Amazon SNS topics, Cloud Canvas also imports any Lambda functions that are related resources\. 

### SQS Queues<a name="w31aac23c28c25b7c26c13c13"></a>

For SQS queues, Cloud Canvas imports the following resource attributes: 
+ `DelaySeconds`
+ `MaximumMessageSize`
+ `MessageRetentionPeriod`
+ `ReceiveMessageWaitTimeSeconds`
+ `RedrivePolicy`
+ `VisibilityTimeout`