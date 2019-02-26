
Azure Devops 
1. Create Personal Access Token - This is required for communication between Azure Devops and Microsoft Azure. You can read more about PATs [here] (https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=vsts) ![](./images/CreatingPAT.png)
2. Create Deployment Group: The release pipeline will create two VM's (Staging and Production) in Microsoft Azure and deploy the app into these VM's. 
![](./images/CreateDeploymentGroup.PNG)

Dynatrace
We need a couple of things from Dynatrace before we launch the Release Pipeline
1. Your Dynatarce Tenant URL 
2. Your Dynatrace Tenant Token : You can get both these from Deploy Dynatrace -> Start Installation -> Linux
Tenant URL looks like: https://XXXXX.live.dynatrace.com
Tenant Token is specified as Api-Token in the URL portion of the wget command. 
![](./images/DynatraceTenantInfo.PNG)
3. Your Dynatrace API Token: Go to Settings -> Integration -> Dynatrace API -> Generate token 
![](./images/DynatraceAPIToken.PNG)
Copy all the values into the Azure_Devops_Values.txt 
