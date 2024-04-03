# static-website-cdn

This is a project to demonstrate deployment of a Static Web Site on azure cloud with CDN endpoint configured to acess the website with the following URL.
https://endpoint-lmvdj3nf22ikm.azureedge.net/

Created Bicep Modules for deploying resources
1. storageaccount.bicep
    This file deploys an Azure Storage account, and then configures it to support static website hosting.
    As enabling static website hosting isn't possible directly in Bicep or an ARM template,so a deployment script is used to enable the feature.

2. cdn.bicep 
   This file deploys CDN Profile and End Point.
3. main.bicep
   The above modules are called in Main.Bicep file.

Parameters:
Three environments Dev,Stage and Prod are created and the following files are used to pass parmeters  for the bicep file in future these can be extended as per the requirement to add aditional resources.
 1. dev.parameters.json
 2. stage.parameters.json
 3. prod.parameters.json


 Pipline Files:
 1. azure-pipeline.yaml
    In this pipline three environments Dev,Stage and Prod are created using three different resource groups.
    The following three variable groups are used to pass pipeline variables (ClientId,Client Secret and Tenant ID)of a Service principle created 
     a. static-website-variable-group-dev
     b. static-website-variable-group-stage
     c. static-website-variable-group-prod 
 2. azure-deploy-template.yaml

 Power Shell Script File (Pester Tests):
 1. verify-website.tests.ps1 
    A power shell script file is created for runing Pester Tests which validates Storage Account,CDN Profile, CDN End Point, Static Website and its content.
