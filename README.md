# UnbreakablePipeline Workshop for Azure DevOps and Dynatrace 


Azure Devops provides multiple development collaboration tools. For this Workshop we will be using the following tools to create a high performant, resilient, self- healing pipeline:
*Azure Pipelines:* Creating CI/CD pipelines for deploying the test application. You can read more on Azure Devops Pipelines [here](https://docs.microsoft.com/en-us/azure/devops/pipelines/index?view=vsts).

Pre Reqs 
1. Sign up for Azure account. You can do it [here.](https://azure.microsoft.com/en-us/)
2. Sign up for Azure Devops. You can do it [here.](https://azure.microsoft.com/en-ca/services/devops/)
3. Sign up for Dynatrace trial. You can do it [here.](https://www.dynatrace.com/trial/)

Concepts
## The UnbreakablePipeline  comprises of 2 main components 
*Quality Gate* To effectively Shift Left and prevent sub optimal code from making it downstream in a pipeline 
*Remediation as Code* To fix / handle sub optimal code before it impacts users

Sample Application
To demonstrate the Unbreakable Pipeline concept we use a simple node.js Sample application with a single webpage and some service endpoints. The application is coded to exibit different behavior for different Builds. Throughout the course of the workshop we will update the Build Name by changing the *SimulateBuildNumber* Variable in the pipelines. 

| Build Number | Behavior |
| --- | --- |
| **1** | Run Normally without any issues |
| **2** | 50% of the requests return HTTP 500 |
| **3** | Run Normally without any issues |
| **4** | if Environment is Staging run normally, if Environment = Production 10% requests return HTTP 500 |



