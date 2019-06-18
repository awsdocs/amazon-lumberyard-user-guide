# Lumberyard 1\.7<a name="lumberyard-migrating-1-7"></a>

If you are upgrading your projects to Lumberyard 1\.7, use the following instructions to migrate your projects with AWS resources managed by the Cloud Canvas Resource Manager and created using previous versions of Lumberyard\.

**To update your projects with AWS resources to work with Lumberyard 1\.7**

1. Use the `lmbr_aws update-project-code` command to update the contents of the `\project\AWS\project-code` directory\.
**Note**  
If you use source control, you must check out these files before executing the `update-project-code` command\.

   After executing the `update-project-code` command, you must add any new files in this directory to your source control system\.

1. Edit the `project-template.json` file \(located in the `\project\AWS` directory\) to make the following changes:

   1. In the `Parameters` object, add a `CloudCanvasStack` parameter as shown below\. The default value for this parameter is Project\. The `ConfigurationKey` parameter should be present and remain unchanged\.

      ```
      "Parameters": {
              "CloudCanvasStack": {
                  "Type": "String",
                  "Description": "Identifies this stack as a Lumberyard Cloud Canvas managed stack.",
                  "Default": "Project"
              },
              "ConfigurationKey": {
                  "Type": "String",
                  "Description": "Location in the configuration bucket of configuration data."
              }
          },
      ```

   1. In the `Configuration` bucket resource definition, remove the `DeletionPolicy` property as shown below\.

      ```
      "Resources": {
       
            ...
        
              "Configuration": {
                  "Type": "AWS::S3::Bucket",
                  "DeletionPolicy": "Retain", <==== DELETE THIS LINE
                  "Properties": {
      ...
      ```

1. Edit the `deployment-access-template.json` file \(located in the `\project\AWS` directory\) to add the `CloudCanvasStack` parameter as shown below\. The default value for this parameter is DeploymentAccess\. 

   The following parameters should be present and remain unchanged: `ProjectResourceHandler`, `ConfigurationBucket`, `ConfigurationKey`, `ProjectPlayerAccessTokenExchangeHandler`, `ProjectStack`, `DeploymentName`, `DeploymentStack`, and `DeploymentStackArn`\.

   ```
   "Parameters" : {
       
           "CloudCanvasStack": {
               "Type": "String",
               "Description": "Identifies this stack as a Lumberyard Cloud Canvas managed stack.",
               "Default": "DeploymentAccess"
           },
   
           "ProjectResourceHandler": {
               "Type": "String",
               "Description": "Service token of the custom resource handler."
           },
           
   		...
   ```

1. Edit the `deployment-template.json` file \(located in the `\project\AWS` directory\) to make the following changes:

   1. Add a `CloudCanvasStack` parameter as shown below\. The default value for this parameter is `Deployment`\. 

      The following parameters should be present and remain unchanged: `ProjectResourceHandler`, `ConfigurationBucket`, `ConfigurationKey`, `DeploymentName`, and `ProjectStackId`\.

      ```
      "Parameters" : {
          
              "CloudCanvasStack": {
                  "Type": "String",
                  "Description": "Identifies this stack as a Lumberyard Cloud Canvas managed stack.",
                  "Default": "Deployment"
              },
      
              "ProjectResourceHandler": {
                  "Type": "String",
                  "Description": "Service token of the custom resource handler."
              },
       
              ...
      ```

   1. For each of the `AWS::CloudFormation::Stack` resource definitions in the `Resources` object, add the following parameters as shown below: `DeploymentStackArn`, `DeploymentName`, and `ResourceGroupName`\.

      You must change the value for the `ResourceGroupName` parameter for each stack resource to use the resource name\.

      The following parameters should be present and remain unchanged: `ProjectResourceHandler`, `ConfigurationBucket`, and `ConfigurationKey`\.

      ```
      "Resources": {
       
              ...
              "DontDieAWS": {
                  "Type": "AWS::CloudFormation::Stack",
                  "Properties": {
                      "TemplateURL": { "Fn::GetAtt": [ "DontDieAWSConfiguration", "TemplateURL" ] },
                      "Parameters": {
                          "DeploymentStackArn": { "Ref": "AWS::StackId" },
                          "DeploymentName": { "Ref": "DeploymentName" },
                          "ResourceGroupName": "DontDieAWS", <== Change this value to match the resource name for each stack resource.
                          "ProjectResourceHandler": { "Ref": "ProjectResourceHandler" },
                          "ConfigurationBucket": { "Fn::GetAtt": [ "DontDieAWSConfiguration", "ConfigurationBucket" ] },
                          "ConfigurationKey": { "Fn::GetAtt": [ "DontDieAWSConfiguration", "ConfigurationKey" ] }
                      }
                  }
              }
              ...
      ```

1. Edit the `resource-template.json` file \(located in the `project\resource-group\resource-group-name` directory for each of your projects\) to add the following parameters as shown below: `CloudCanvasStack`, `DeploymentStackArn`, `DeploymentName`, and `ResourceGroupName`\. The default value for the `CloudCanvasStack` parameter is ResourceGroup\.

   The following parameters should be present and remain unchanged: `ProjectResourceHandler`, `ConfigurationBucket`, and `ConfigurationKey`\. Any other resource group\-specific parameters must also remain unchanged\.

   ```
   "Parameters": {
           "CloudCanvasStack": {
               "Type": "String",
               "Description": "Identifies this stack as a Lumberyard Cloud Canvas managed stack.",
               "Default": "ResourceGroup"
           },
           "DeploymentStackArn": {
               "Type": "String",
               "Description": "ARN of the deployment stack that owns this resource group stack."
           },
           "DeploymentName": {
               "Type": "String",
               "Description": "Name of the resource group's deployment."
           },
           "ResourceGroupName": {
               "Type": "String",
               "Description": "Name of the resource group."
           },
           "ProjectResourceHandler": {
               "Type": "String",
               "Description": "Service token of the custom resource handler."
           },
      		    ...
   ```