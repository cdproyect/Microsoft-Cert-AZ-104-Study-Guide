# Manage Identifies and Governance in Azure

## User Accounts

Typically, Azure AD defines users in three ways:

- **Cloud identities.** These users exist only in Azure AD. Examples are administrator accounts and users that you manage yourself. Cloud identities can be in Azure Active Directory or an external Azure Active Directory, if the user is defined in another Azure AD instance. When these accounts are removed from the primary directory, they are deleted.
- **Directory-synchronized identities.** These users exist in an on-premises Active Directory. A synchronization activity that occurs via Azure AD Connect brings these users in to Azure. Their source is Windows Server AD.
- **Guest users.** These users exist outside Azure. Examples are accounts from other cloud providers and Microsoft accounts such as an Xbox LIVE account. Their source is Invited user. This type of account is useful when external vendors or contractors need access to your Azure resources. Once their help is no longer necessary, you can remove the account and all of their access.

### Manage User Accounts

- **Portal** You can add new users through the Azure portal. In addition to Name and User name, there is profile information like Job Title and Department.
- **Microsoft 365 Admin Center**.
- **Microsoft Intune admin console**.
- **Azure CLI.**

#### Create bulk user accounts

Azure Active Directory (Azure AD) supports bulk user create and delete operations and supports downloading lists of users. Just fill out the comma-separated values (CSV) template. You can download the template from the Azure AD portal. To create users in the Azure portal, you must be signed in as a Global administrator or User administrator.

Consider:

- **Naming conventions**. Ex. last name, first name + @domain
- **Passswords.** mplement a convention for the initial password of the newly created user. Figure out a way for the new users to receive their password in a secure way. Methods commonly used include generating a random password and emailing it to the new user or their manager.

---
**Note**

PowerShell is also available for buld user uploads.

---

### Create group accounts

Azure AD allows you to define two different types of groups.

- **Security groups.** Security groups are used to manage member and computer access to shared resources for a group of users. For example, you can create a security group for a specific security policy. By doing it this way, you can give a set of permissions to all the members at once, instead of having to add permissions to each member individually. This option requires an Azure AD administrator.
- **Microsoft 365 groups.** Microsoft 365 groups provide collaboration opportunities by giving members access to a shared mailbox, calendar, files, SharePoint site, and more. You can give people outside of your organization access to the group. Both users and admins can use Microsoft 365 groups.

### Adding members to groups

There are different ways you can assign access rights:

- **Assigned.** Lets you add specific users to be members of this group and to have unique permissions
- **Dynamic User.** Lets you use dynamic membership rules to automatically add and remove members. When a member's attributes change, Azure reviews the dynamic group rules for the directory. If the member meets the rule requirements, they're added. If the member no longer meets the rules requirements, they're removed.
- **Dynamic Device (Secure groups only).** Lets you use dynamic group rules to automatically add and remove devices. If a device's attributes change, Azure reviews the dynamic group rules for the directory. If the device meets the rule requirements, they're added. If the device no longer meets the rules requirements, they're removed.

### Create administrative units

It can be useful to restrict administrative scope by using administrative units in organizations that are made up of independent divisions of any kind.

#### Example for using administrative units

Consider the example of a large university that's made up of many autonomous schools (School of Business, School of Engineering, and so on). Each school has a team of IT admins who control access, manage users, and set policies for their school.

A central administrator could:

- Create a role with administrative permissions over only Azure AD users in the business school administrative unit.
- Create an administrative unit for the School of Business.
- Populate the administrative unit with only the business school students and staff.
- Add the business school IT team to the role, along with its scope.

#### Considerations

- You can mange administrative units by using the Azure portal, PowerShell cmdlets and scripts, or Microsoft Graph.
- In the portal, you can manage administrative units if you are a Global Administrator or a Privileged Role Administrator.
- Administrative units apply scope only to management permissions. They don't prevent members or administrators from using their default use permissions to browse other users, groups, or resources outside the adminstrative unit.

## Subscriptions

An Azure subscription is a logical unit of Azure services that is linked to an Azure account. Billing for Azure services is done on a per-subscription basis. If your account is the only account associated with a subscription, then you are responsible for billing.

### Azure accounts

Subscriptions have accounts. An Azure account is simply an identity in Azure Active Directory (Azure AD) or in a directory that is trusted by Azure AD, such as a work or school organization. If you don't belong to one of these organizations, you can sign up for an Azure account by using your Microsoft Account, which is also trusted by Azure AD.

Every Azure subscription is associated with an Azure Active Directory. Users and services that access resources of the subscription first need to authenticate with Azure Active Directory.

### Types of Subscriptions

Azure offers free and paid subscription options to suit different needs and requirements. The most commonly used subscriptions are:

- Free
- Pay-As-You-Go
- Enterprise Agreement
- Student

### Plan and control expenses

The ways that Cost Management help you plan for and control your costs include: Cost analysis, budgets, recommendations, and exporting cost management data.

- **Cost analysis.** You use cost analysis to explore and analyze your organizational costs. You can view aggregated costs by organization to understand where costs are accrued and to identify spending trends. And you can see accumulated costs over time to estimate monthly, quarterly, or even yearly cost trends against a budget.

- **Budgets.** Budgets help you plan for and meet financial accountability in your organization. They help prevent cost thresholds or limits from being surpassed. Budgets can also help you inform others about their spending to proactively manage costs. And with them, you can see how spending progresses over time.

- **Recommendations.** Recommendations show how you can optimize and improve efficiency by identifying idle and underutilized resources. Or, they can show less expensive resource options. When you act on the recommendations, you change the way you use your resources to save money. To act, you first view cost optimization recommendations to view potential usage inefficiencies. Next, you act on a recommendation to modify your Azure resource use to a more cost-effective option. Then you verify the action to make sure that the change you make is successful.

- **Exporting cost management data.** If you use external systems to access or review cost management data, you can easily export the data from Azure. And you can set a daily scheduled export in CSV format and store the data files in Azure storage. Then, you can access the data from your external system.

### Apply resource tagging

You can apply tags to your Azure resources to logically organize them by categories. Each tag consists of a name and a value. For example, you can apply the name Environment and the value Production or Development to your resources. After creating your tags, you associate them with the appropriate resources.

With tags in place, you can retrieve all the resources in your subscription with that tag name and value. This means, you can retrieve related resources from different resource groups.

There are a few things to remember about tagging:

- Each resource or resource group can have a maximum of 50 tag name/value pairs.
- Tags applied to the resource group are not inherited by the resources in that resource group.

### Apply cost savings

- **Reservations** help you save money by paying ahead. You can pay for one-year or three-years of virtual machine, SQL Database compute capacity, Azure Cosmos DB throughput, or other Azure resources. Pre-paying allows you to get a discount on the resources you use. Reservations can significantly reduce your virtual machine, SQL database compute, Azure Cosmos DB, or other resource costs up to 72% on pay-as-you-go prices. Reservations provide a billing discount and don't affect the runtime state of your resources.

- **Azure Hybrid Benefits** is a pricing benefit for customers who have licenses with Software Assurance. Azure Hybrid Benefits helps maximize the value of existing on-premises Windows Server or SQL Server license investments when migrating to Azure. There's an Azure Hybrid Benefit Savings Calculator to help you determine your savings.

- **Azure Credits** is monthly credit benefit that allows you to experiment with, develop, and test new solutions on Azure. For example, as a Visual Studio subscriber, you can use Microsoft Azure at no extra charge. With your monthly Azure credit, Azure is your personal sandbox for dev/test.

Azure regions pricing can vary from one region to another, even in the US. Double check the pricing in various regions to see if you can save a little.

Budgets help you plan for and drive organizational accountability. With budgets, you can account for the Azure services you consume or subscribe to during a specific period. They help you inform others about their spending to proactively manage costs, and to monitor how spending progresses over time. When the budget thresholds you've created are exceeded, only notifications are triggered. None of your resources are affected and your consumption isn't stopped. You can use budgets to compare and track spending as you analyze costs.

Pricing Calculator:

The Pricing Calculator provides estimates in all areas of Azure including compute, networking, storage, web, and databases.

## [Azure Policy](https://docs.microsoft.com/en-gb/learn/modules/configure-azure-policy/4-create-azure-policies)

### Management Groups

If your organization has several subscriptions, you may need a way to efficiently manage access, policies, and compliance for those subscriptions. Azure management groups provide a level of scope above subscriptions. You organize subscriptions into containers called management groups and apply your governance conditions to the management groups. Management group enable:

- Organizational alignment for your Azure subscriptions through custom hierarchies and grouping.
- Targeting of policies and spend budgets across subscriptions and inheritance down the hierarchies.
- Compliance and cost reporting by organization (business/teams).

All subscriptions within a management group automatically inherit the conditions applied to the management group. For example, you can apply policies to a management group that limits the regions available for virtual machine (VM) creation. This policy would be applied to all management groups, subscriptions, and resources under that management group by only allowing VMs to be created in that region.

#### Adding management groups

You can create the management group by using the portal, PowerShell, or Azure CLI.

- The **Management Group ID** is the directory unique identifier that is used to submit commands on this management group. This identifier is not editable after the creationg as it is used throughout the Azure system to identify this group.
- **The Display Name** field is the name that is displayed within the Azure Portal. A separate display name is an optional field when creating the management group and can be changed at any time.

### Implement Azure policies

Azure Policy is a service in Azure that you use to create, assign, and manage policies. These policies enforce different rules over your resources, so those resources stay compliant with your corporate standards and service level agreements. Azure Policy runs evaluations and scans for resources that are not compliant.

The main advantages of Azure policy are in the areas of enforcement and compliance, scaling, and remediation.

- **Enforcement and compliance.** Turn on built-in policies or build custom ones for all resource types. Real-time policy evaluation and enforcement. Periodic and on-demand compliance evaluation.
- **Apply policies at scale.** Apply policies to a Management Group with control across your entire organization. Apply multiple policies and aggregate policy states with policy initiative. Define an exclusion scope.
- **Remediation.** Real-time remediation, and remediation on existing resources.
  
Azure Policy will be important to you if your team runs an environment where you need to govern:

- Multiple engineering teams (deploying to and operating in the environment)
- Multiple subscriptions
- Need to standardize/enforce how cloud resources are configured
- Manage regulatory compliance, cost control, security, or design consistency

**Use cases**

- Specify the resource types that your organization can deploy.
- Specify a set of virtual machine SKUs that your organization can deploy.
- Restrict the locations your organization can specify when deploying resources.
- Enforce a required tag and its value.
- Audit if Azure Backup service is enabled for all Virtual machines.

#### Create Azure policies

To implement Azure Policies, you can follow these steps.

1. **Browse Policy Definitions.** A Policy Definition expresses what to evaluate and what actions to take. Every policy definition has conditions under which it is enforced. And, it has an accompanying effect that takes place if the conditions are met. For example, you could prevent VMs from being deployed if they are exposed to a public IP address.
1. **Create Initiative Definitions.** An initiative definition is a set of Policy Definitions to help track your compliance state for a larger goal. For example, ensuring a branch office is compliant.
1. **Scope the Initiative Definition.** You can limit the scope of the Initiative Definition to Management Groups, Subscriptions, or Resource Groups.
1. **View Policy Evaluation results.** Once an Initiative Definition is assigned, you can evaluate the state of compliance for all your resources. Individual resources, resource groups, and subscriptions within a scope can be exempted from having policy rules affect it. Exclusions are handled individually for each assignment.

#### Create policy definitions

There are many Built-in Policy Definitions for you to choose from. Sorting by Category will help you locate what you need. For example,

- The Allowed Virtual Machine SKUs enables you to specify a set of virtual machine SKUs that your organization can deploy.
- The Allowed Locations policy enables you to restrict the locations that your organization can specify when deploying resources. The Allowed Locations policy can be used to enforce your geo-compliance requirements.

When there isn't an applicable policy you can add a new Policy Definition. You can import a policy definitions from [GitHub](https://github.com/Azure/azure-policy/tree/master/samples). New Policy Definitions are added almost every day.

#### Create initiative definitions

Once you have determined which Policy Definitions you need, you create an Initiative Definition. This definition will include one or more policies. There is a pick list on the right side of the New Initiative definition page (not shown) to make your selection.

#### Scope the initiative definition

Once our Initiative Definition is created, you can assign the definition to establish its scope. A scope determines what resources or grouping of resources the policy assignment gets enforced on.

#### Determine compliance

Once your policy is in place, you can use the Compliance blade to review non-compliant initiatives, non-compliant policies, and non-compliant resources.

Policy conditions are evaluated against your existing resources. Although the portal does not show the evaluation logic, the compliance state results are shown. The compliance state result is either compliant or non-compliant.

## Role-based access control

### Overview of Role-based access control

Securing your Azure resources, such as virtual machines, websites, networks, and storage, is a critical function for any organization using the cloud. Your company wants to ensure that your data and assets are protected, but still grant your employees and partners the access they need to perform their jobs.

You decide to use role-based access control. You need to ensure assets are protected, but users can still access the resources they need.

Access management for cloud resources is a critical function for any organization that is using the cloud. Role-based access control (RBAC) helps you manage who has access to Azure resources, what they can do with those resources, and what areas they have access to.

Azure RBAC is an authorization system built on Azure Resource Manager that provides fine-grained access management of resources in Azure.

#### Examples of what can you do with Azure roles

Here are some examples of what you can do with Azure RBAC:

- Allow an application to access all resources in a resource group
- Allow one user to manage virtual machines in a subscription and another user to manage virtual networks
- Allow a DBA group to manage SQL databases in a subscription
- Allow a user to manage all resources in a resource group, such as virtual machines, websites, and subnets

#### Concepts

- **Security principal.** Object that represents something that is requesting access to resources. Examples: user, group, service principal, managed identity

- **Role definition.** Collection of permissions that lists the operations that can be performed. Examples: Reader, Contributor, Owner, User Access Administrator

-**Scope.** Boundary for the level of access that is requested. Examples: management group, subscription, resource group, resource

-**Assignment.** Attaching a role definition to a security principal at a particular scope. Users can grant access described in a role definition by creating an assignment. Deny assignments are currently read-only and can only be set by Azure.

#### Considerations

Using Azure RBAC, you can segregate duties within your team and grant only the amount of access to users that they need to perform their jobs. Instead of giving everybody unrestricted permissions in your Azure subscription or resources, you can allow only certain actions at a particular scope.

When planning your access control strategy, it's a best practice to grant users the least privilege to get their work done.

### Create a role definition

Each role is a set of properties defined in a JSON file. This role definition includes Name, Id, and Description. The definition also includes the allowable permissions (Actions), denied permissions (NotActions), and scope (read access, etc.) for the role.

![role-definition](img/role-definition.png)

#### Actions and NotActions

The Actions and NotActions properties can be tailored to grant and deny the exact permissions you need. this table defines how the Owner, Contributor, and Reader roles.

| Built-in Role | Action | NotActions |
| - | - | - |
|Owner (allow all actions)| * | |
|Contributor (allow all actions exept writing or deleting role assignment)|* | Microsoft.Authorization/*/Delete, Microsoft.Authorization/*/Write, Microsoft.Authorization/*/elevateAccess/Action |
|Reader (allow all read actions)| */read | 

#### Scope your role

After denining the Actions and NotActions, you must scope the role.

The AssignableScopes property of the role specifies the role scope. The scope can be subscriptions, resource groups, or resources.

Example:

```json
* /subscriptions/[subscription id]
* /subscriptions/[subscription id]/resourceGroupts/[resource group name]
* /subscriptions/[subscription id]/resourceGroupts/[resource group name]/[resource]
```
### Create a role assignment

A role assignment is the process of scoping a role definition to a user, group, service principal, or managed identity. The purpose of the role assignment is to grant access. Access is revoked by removing a role assignment.

For example, in the diagram, the Marketing group has been assigned the Contributor role for the pharma-sales resource group. Users in the Marketing group can create or manage any Azure resource in the pharma-sales resource group. Marketing users don't have access to resources outside the pharma-sales resource group, unless they are part of another role assignment.

![role-assignment](img/role-assignment.png)

<span stype="color:red">---
Note

A resource inherits role assignments from its parent resource.

---</span>

### Compare Azure roles to Azure Active Directory roles

At a high level, Azure RBAC roles control permissions to manage Azure resources, while Azure AD administrator roles control permissions to manage Azure Active Directory resources. The following table compares some of the differences.

|Azure RBAC roles|Azure AD roles|
| - | - |
|Manage access to Azure resources. | Manage access to Azure Active Directory resources.
|Scope can be specified at multiple levels (management group, subacription, resource group, resource)| Scope is at the tenant level
| Role information can be accessed in Azure portal, Azure CLI, Azure PowerShell, Azure Resource Manager templates, REST API.| Role information can be accessed in Azure admin portal, Microsoft 365 admin portal, Microsoft Graph AzureAD PowerShell.

<span stype="color:red">---
Note

Azure Resource Manager roles should be used instead of Classic administrator roles.

---</span>