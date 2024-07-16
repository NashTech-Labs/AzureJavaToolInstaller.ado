# AzureJavaToolInstaller.ado
Use this template to acquire a specific version of Java from a user-supplied Azure blob or the tool cache and set JAVA_HOME.


## Parameters:

The pipeline requires the following parameters to be defined:


| Name  | Displayname | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | :-------------: | :-------------: | ------------- | :-------------: | ------------- |
| versionSpec | JDK version | string | '8' | | Required | Specifies the JDK version to make available on the path. Use a whole number version, such as 10. |
| jdkArchitectureOption | JDK architecture | string |  | x64, x86 | Required | Specifies the architecture (x86, x64) of the JDK |
| jdkSourceOption | JDK source | string |  | AzureStorage (Azure Storage), LocalDirectory (Local Directory), PreInstalled (Pre-installed) | Required | Specifies the source for the compressed JDK. The source can be Azure blob storage or a local directory on the agent or source repository, or you can use the pre-installed version of Java |
| jdkFile | JDK file | string |  | | Required when jdkSourceOption == LocalDirectory | Specifies the path to the JDK archive file that contains the compressed JDK. The path could be in your source repository or a local path on the agent. The file should be an archive (.zip, .tar.gz, .7z) containing the bin folder on the root level or inside a single directory. MacOS supports .pkg and .dmg files containing only one .pkg file inside. |
| azureResourceManagerEndpoint | Azure subscription | string |  | | Required when jdkSourceOption == AzureStorage | Specifies the Azure Resource Manager subscription for the JDK |
| azureStorageAccountName | Storage account name | string |  | | Required when jdkSourceOption == AzureStorage | Specifies Azure Classic or Resource Manager storage accounts. Select the storage account name in which the JDK is located |
| azureContainerName | Container name | string |  | | Required when jdkSourceOption == AzureStorage | Specifies the name of the container in the storage account where the JDK is located |
| azureCommonVirtualFile | Common virtual path | string |  | | Required when jdkSourceOption == AzureStorage | Specifies the path to the JDK inside the Azure storage container |
| jdkDestinationDirectory | Destination directory | string |  | | Required when jdkSourceOption != PreInstalled | Specifies the destination directory where the JDK should be extracted |
| azureResourceGroupName | Resource Group name | string |  | | Required when jdkSourceOption == AzureStorage | Resource Group name of the storage account |
| cleanDestinationDirectory | Clean destination directory | boolean | true | | Optional when jdkSourceOption != PreInstalled| Specifies the option to clean the destination directory before JDK is extracted into it |
| createExtractDirectory | Create directory for extracting | boolean | true | | Optional when jdkSourceOption != PreInstalled| By default, the task creates a directory similar to JAVA_HOME_8_X64_OpenJDK_zip for extracting JDK. This option disables the creation of that folder and, if set to false, JDK is located in the root of jdkDestinationDirectory instead |
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
