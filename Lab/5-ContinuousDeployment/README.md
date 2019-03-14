# Continuous Deployment

## Release Pipeline

Azure DevOps provides Release pipelines for Continuous Deployment. These pipelines are responsible for creating Azure Resources and deploying code on these Azure resources. We will divide this workshop into two parts: -> Creating Utilities and UnbreakablePipelineDemo-CD

## 5(a) Creating Utilities
As a part of the workshop we will create 4 Resources in Azure cloud. These are as follows:

1. Virtual Machines - Staging and Production: The VM's are the infrastructure where the sample application is deployed. First the application is deployed to Staging and if it passes the Quality Gate it is moved to Production. 
2. Azure Functions - MonspecValidation and SelfHealing: These Azure functions have specific purposes

**MonspecValidation**: After the build is deployed to Staging it needs to pass a Quality Gate which checks for Performance signature of the application to validate if the build can be moved to production. 

**SelfHealingFunction**: In the case that a bad build makes it to Production, Dynatrace opens a problem and makes a call to the Self Healing function. The function then makes calls to Azure Devops API and reverts back to a previous good build. 

**Dynatrace One Agent**: The Dynatrace Oneagent is installed on both Staging and Production VM's for monitoring 

## Setting up Create Utilities Pipeline 
1. Select the Create Utilitles Pipeline and click on Edit
2. In the Pipeline view, there are some items that need attention. Click on the 2 Jobs, 8 Tasks. 
![](../../images/AzureDevopsCreateUtilities1.PNG)
3. Set Agent Job to be Hosted VS2017
![](../../images/AzureDevopsCreateUtilities2.PNG)
4. Update the tasks with appropriate values
![](../../images/AzureDevopsCreateUtilities3.PNG)
5. Update the tasks with appropriate values
![](../../images/AzureDevopsCreateUtilities4.PNG)
6. Create a New Service Connection
![](../../images/AzureDevopsCreateUtilities5.PNG)
7. Update the Deployment Group Name
![](../../images/AzureDevopsCreateUtilities6.PNG)
8. Go to Variables and update the Dynatrace-Tenant and Dynatrace Token information
![](../../images/AzureDevopsCreateUtilities7.PNG)
9. Save and create a new release 
![](../../images/AzureDevopsCreateUtilities8.PNG)

## Expected Output
1. Login to Dynatrace tenant to verify that the OneAgent is installed on two hosts: 
![](../../images/AzureDevopsCreateUtilities9.PNG)
2. Login to Azure portal and ensure that the following resources are created
![](../../images/AzureDevopsCreateUtilities10.PNG)

## 5(b) UnbreakablePipelineDemo-CD
This section is to update the pipeline which will deploy the sample application and run the Quality gate. 

## Setting up UnbreakablePipelineDemo-CD
1. Update the UnbreakablePipelineDemo-CD by clicking on Edit -> and Select Staging environment
![](../../images/AzureDevopsUbpCD1.PNG) 
2. For the Deployment Group Job, add the name of the Deployment group created previously and add Staging in the required tags section
![](../../images/AzureDevopsUbpCD2.PNG)
3. Select Production in task and update the Tag to Production 
![](../../images/AzureDevopsUbpCD3.PNG)
4. Go to Variables -> Enter Dynatrace Tenant, Dynatrace token, Dynatrace API Token
![](../../images/AzureDevopsUbpCD4.PNG)
5. Configure the Quality Gate -> Click on the gate and Enable Gates. Add a new Gate and select Azure Function. Enter the function URL (get this from Azure Portal and append: /api/validatePerfSig. 
![](../../images/AzureDevopsUbpCD6.PNG)
Enter the Function Key which is available in the Azure Portal
![](../../images/AzureDevopsUbpCD7.PNG)
Enter these values in the Azure Devops Gate
![](../../images/AzureDevopsUbpCD5.PNG)
6. Save the changes and Create a new Release. Select the latest Build and Deploy the release Pipeline
![](../../images/AzureDevopsUbpCD8.PNG)
7. Ensure all Steps are executed successfully
![](../../images/AzureDevopsUbpCD9.PNG)
8. The gate gets executed twice
![](../../images/AzureDevopsUbpCD10.PNG)
9. The Quality Gate is validating two Performance metrics:
**Response time of the Service and Failure rate**
![](../../images/AzureDevopsUbpCD11.PNG)
10. After the Quality gate succeeds the release moves to Production and the same app is deployed on the Production Virtual Machine
![](../../images/AzureDevopsUbpCD12.PNG)
11. Verify that both Staging and Production services are Deployed into Production and the Deployment Event has been pushed to the service:
![](../../images/AzureDevopsUbpCD13.PNG)
12. **Simulate Build Number 2** -  Go to UnbreakablePipelineDemo-CD -> Variables and set the SimulatedBuildNumber to 2. This build throws errors in Staging Environment thereby Failing the Quality check. The build is determined to be bad and is not pushed to Production - Stopping Bad build from moving through the Pipeline.  
![](../../images/AzureDevopsUbpCD14.PNG)
13. Quality Gate Fails - This is expected:
![](../../images/AzureDevopsUbpCD15.PNG)



