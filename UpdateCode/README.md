# Update Azure Function Names

## Why do we need to update the Function Names
The project deploys some Azure Functions. By default Azure creates a DNS record for each Azure Function, this DNS name needs to be unique for each user. Hence we will change the name of the functions in the ARM template parameters file which will be used to create the DNS record for the functions. 

## How to update the Function Names
Go to Repos -> files -> functionarmTemplate.parameters.json and edit the file. Replace "yourname" with your name and commit the code. 

![](../images/AzureDevopsUpdateFunction.PNG)
