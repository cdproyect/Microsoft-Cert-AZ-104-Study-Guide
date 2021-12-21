# Azure Resource Manager


- **Resource Groups** Logical container for grouping resources could be based on lifecycle and security
- **Azure Subscription** Logical construct, used as billing unit, which contains resource groups and associated resources

All Subscriptions are controlled by Azure Resource Manager (ARM) is the orchestration layer for managing the Azure cloud, uses REST API endpoints via: Azure Portal, Azure CLI, Azure Powershell. Those request are not completed by ARM, it uses Azure Resource Providers to complete request (to create/update/delete an Azure resource). 
To do so there are a trust relationship between Azure AD Tenant and Azure Resource Management and Azure AD Tenant and Subscription Tenant.

## Using ARM Template

[Deploy Azure infrastructure by using JSON ARM templates](https://docs.microsoft.com/en-us/learn/modules/create-azure-resource-manager-template-vs-code/)

ARM templates are JavaScript Object Notation (JSON) files that define the infrastructure and configuration for your deployment. The template uses a declarative syntax. The declarative syntax is a way of building the structure and elements that outline what resources will look like without describing its control flow. Declarative syntax is different than imperative syntax, which uses commands for the computer to perform. Imperative scripting focuses on specifying each step in deploying the resources.

ARM templates are idempotent, which means you can deploy the same template many times and get the same resource types in the same state.


### What is IaC (Infrastructure as Code)

- Consistent configuration
- Improved scalability
- Faster deployments
- Better traceability

### ARM template file structure

ARM templates files are made up the following elements:

|Element|Description|
| -- | -- | 
| schema | A required section that defines the location of the JSON schema file that describes the structure of JSON data. The version number you use depends on the scope of the deployment and your JSON editor
| contentVersion | A required section that defines the version of your template (such as 1.0.0.0). You can use this value to document significant changes in your template to ensure you're deploying the right template.
| apiProfile | An optional section that defines a collection of API versions for resource types. You can use this value to avoid having to specify API versions for each resource in the template.
| parameters | An optional section where you define values that are provided during deployment. These values can be provided by a parameter file, by command-line parameters, or in the Azure portal.
| variables | An optional section where you define values that are used to simplify template language expressions.
| functions | An optional section where you can define user-defined functions that are available within the template. User-defined functions can simplify your template when complicated expressions are used repeatedly in your template.
| resources | A required section that defines the actual items you want to deploy or update in a resource group or a subscription.
| output | An optional section where you specify the values that will be returned at the end of the deployment.

## Guidance

The following suggestions help you take full advantage of ARM when working with your solutions:
- Define and deploy your infrastructure through the declarative syntax in Azure Resource Manager templates, rather than through imperative commands.
- Define all deoloyment and configuration steps in a template. you should have no manual steps for setting up your solution
- Run imperative commands to manage your resources, such as to start or stop an app or maching
- Arrange resources with the same lifecycle in a resource group. Use tags for all other organizing of resources.

