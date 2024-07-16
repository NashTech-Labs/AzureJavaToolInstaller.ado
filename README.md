# AzureJavaToolInstaller.ado
Use this template to acquire a specific version of Java from a user-supplied Azure blob or the tool cache and set JAVA_HOME.


## Parameters:

The pipeline requires the following parameters to be defined:


| Name  | Displayname | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | :-------------: | :-------------: | ------------- | :-------------: | ------------- |
| versionSpec |   | string |  | | Required | |
| jdkArchitectureOption |  | string |  | | Required |  |
| jdkSourceOption |  | string |  | | Required |  |
| jdkFile |  | string |  | | Optional |  |
| azureResourceManagerEndpoint |  | string |  | | Optional |  |
| azureStorageAccountName |  | string |  | | Optional |  |
| azureContainerName |  | string |  | | Optional |  |
| azureCommonVirtualFile |  | string |  | | Optional |  |
| jdkDestinationDirectory |  | string |  | | Optional |  |
| azureResourceGroupName |  | string |  | | Optional |  |
| cleanDestinationDirectory |  | boolean | true | | Optional |  |
| createExtractDirectory |  | boolean | true | | Optional |  |
--------------------------------------------------------------------------------------------------------------------------------------------------

These parameters provide multiple use case options for the template, enable/disable flags for the utilization of different templates as per the requirements.


## Use Cases

You can directly call a particular template as per the requirement. for example: 

 ```yaml
  # azure-pipeline.yml
  resources:
  repositories:
    - repository: Template
      type: github
      name: your_username/AzureJavaToolInstaller.ado
      ref: <respective branch name>
      endpoint: 'githubServiceConnectioNname'

  steps:
  # passing the parameters
  - template: AzureJavaToolInstaller.yml
    parameters:
        versionSpec: '${{parameters.versionSpec}}' 
        jdkArchitectureOption: '${{parameters.jdkArchitectureOption}}' 
        jdkSourceOption: '${{parameters.jdkSourceOption}}' 
        jdkFile: '${{parameters.jdkFile}}' 
        azureResourceManagerEndpoint: '${{parameters.azureResourceManagerEndpoint}}' 
        azureStorageAccountName: '${{parameters.azureStorageAccountName}}' 
        azureContainerName: '${{parameters.azureContainerName}}' 
        azureCommonVirtualFile: '${{parameters.azureCommonVirtualFile}}' 
        jdkDestinationDirectory: '${{parameters.jdkDestinationDirectory}}' 
        azureResourceGroupName: '${{parameters.azureResourceGroupName}}' 
        cleanDestinationDirectory: '${{parameters.cleanDestinationDirectory}}' 
        createExtractDirectory: '${{parameters.createExtractDirectory}}' 
  ```
Make sure to adjust the repository name, branch name, and parameter values according to your project's requirements.
