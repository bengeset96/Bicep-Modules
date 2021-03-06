
# Pipeline for Azure Container Registry

Pipeline for uploading Bicep modules to container registry. This offers possibilities for sharing and referencing modules from Bicep files. 

How does this work?

The first thing it will do is checkout self, that is checking out repository, so it is available for the build agent. It will then leverage PowerShell script named Get-ACRModulesUpdates.ps1 to check if the new commit in the module folder in the repository has some changes to it. Like added or changed file. 

If true, it will put the added or changed Bicep files into staging directory so the build agent can consume it. 

It will then run validation against these Bicep files to make sure everything is in the best shape before publishing as an artifact with the help of Validate-ACRModules.ps1.

Pipeline is also running task called CopyFiles, where it copies Publish-ACRModules.ps1 into staging directory. 

Next is publishing both Bicep and scripts as artifacts.

Now it is time for deploying!

Downloading the artifacts that were created for Bicep and scripts to work directory. 

Publish-ACRModules.ps1 will now be used for uploading to container registry. It even tags modules automatically.

Support for both Linux and Windows agent, so here you can use your preferred operating system.

This was a very general explanation, please look more into the pipeline and scripts folders if you want a deep understanding. Code as documentation, my favorite!










## Simple holistic solution design

![Image](./media/acrExampleDeployment.png)

