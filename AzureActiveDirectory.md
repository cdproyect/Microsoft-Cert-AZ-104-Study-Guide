- [Azure Active Directory](#azure-active-directory)
    - [Select Azure Active Directory editions](#select-azure-active-directory-editions)
  - [Hybrid identity for linking on-premises Active Directory with Azure AD](#hybrid-identity-for-linking-on-premises-active-directory-with-azure-ad)
  - [Azure AD Licenses](#azure-ad-licenses)
  - [Essential feature on Azure AD](#essential-feature-on-azure-ad)
    - [App management](#app-management)
  - [Protect your apps through conditional-access policies](#protect-your-apps-through-conditional-access-policies)
  - [Monitor your app access](#monitor-your-app-access)
  - [Azure AD Identity Protection](#azure-ad-identity-protection)
  - [Get started with Azure AD](#get-started-with-azure-ad)
    - [Stage 1: Build a secure foundation](#stage-1-build-a-secure-foundation)
    - [Stage 2: Add users, manage devices, and configure synchronization](#stage-2-add-users-manage-devices-and-configure-synchronization)
    - [Stage 3: Manage your applications](#stage-3-manage-your-applications)
    - [Stage 4: Monitor your administrators, do access reviews, and automate user life cycles](#stage-4-monitor-your-administrators-do-access-reviews-and-automate-user-life-cycles)
    - [Create a tenant](#create-a-tenant)
    - [Associate a subscription](#associate-a-subscription)

# Azure Active Directory

Azure Active Directory (Azure AD) is a cloud-based identify and access management solution. It helps you secure internal, external, and customer identifies.

Azure AD stores your users in a tenant that represents an organization

Active Directory and Azure AD share a similar name, but they're separate services that are used for different purposes.

[This link](https://docs.microsoft.com/en-us/learn/modules/configure-azure-active-directory/4-compare-active-directory-domain-services) provides a deep comparison between Active Directory Domain Services to Azure Active Directory.


Azure AD is a cloud-based identity solution that helps you manage users and applications. Active Directory manages objects, like devices and users, on your on-premises network. Here are some other differences:

| Service | Authentication | Structure | What it's used for
| - | - | - | - |
| Active Directory | Kerberos, NTLM (Network Lan Manager suite of Microsoft security protocols) | Forests, domains, organizational units | Authentication and authorization for on-premises printers, applications, file services, and more
| Azure Active Directory | Includes SAML, OAuth, WS-Federation | Tenants | Internet-based services and applications like Microsoft 365, Azure services, and third-party SaaS applications.

Azure AD doesn't replace Active Directory. The service you use depends on your organization's needs. The two services can be used together, so you can take advantage of their combined features and capabilities.

### Select Azure Active Directory editions

Azure Active Directory comes in four editions—Free, Microsoft 365 Apps, Premium P1, and Premium P2. The Free edition is included with an Azure subscription. The Premium editions are available through a Microsoft Enterprise Agreement, the Open Volume License Program, and the Cloud Solution Providers program. Azure and Microsoft 365 subscribers can also buy Azure Active Directory Premium P1 and P2 online.

The following table provides a summary of the fetures included per type of edition

To check price per edition follow [this link](https://azure.microsoft.com/pricing/details/active-directory)

| Feature | Free | Microsoft 365 Apps | Premium P1 | Premium P2
| - | - | - | - | - |
| Directory Objects | 500,000 | Unlimited | Unlimited | Unlimited
| Single Sign-On | Unlimited | Unlimited | Unlimited | Unlimited
| Core Identity and Access Management | X | X | X | X
| Business to Business Collaboration | X | X | X | X
| Identity & access Management for Microsoft 365 apps | | X | X | X
| Premium Features | | | X | X 
| Hybrid Identifies | | | X | X
| Advanced Group Access Management | | | X | X
| Conditional Access | | | X | X
| Identity Protection | | | | X
| Identity Governance | | | | X

## Hybrid identity for linking on-premises Active Directory with Azure AD

Your users will want to access applications from both the cloud and on-premises. You can use Azure AD and Active Directory together to provide an identity solution that spans on-premises and the cloud. A single user identity can be used for authentication and to access applications and resources, whatever their location. This user identity is called a hybrid identity.

Multiple authentication methods let you achieve hybrid identity for users:

- **Azure AD password hash synchronization.** Here, the user's passwored is hashed twice and synchronized between the on-premises Active Directory and Azure AD. Users have the same credentials to access resources and applications both on-premises and in the cloud.
- **Azure AD pass-through authentication.** Here, an agent is installed on on-premises servers that authenticate againsts the on-premises Active Directory. When an Azure AD user account tries to authenticate, password authentication is handled on-premises through these servers and Active Directory.
- **Federated authentication.** Here, the authentication process is performed by an on-premises Active Directory Federation Services (AD FS) server that validates users' passwords. Use this authentication method if you want advance measuers like smart card-based authentication for users.

The following table gives a references for which options to use for particular scenarios:

| Requirements | Password hash synchronization | Pass-through authentication | Federated authentication
| - | - | - | - | 
| Automatically synchronize to the cloud the users, contacts, and groups that have been set up on on-premises Active Directory | Yes | Yes | Yes 
| Allow users to access cloud application and resources by using their on-premises password. | Yes | Yes | Yes
Ensure that passwored hashes aren't store in the cloud | No | Yes | Yes
Use cloud-based multi-factor authentication | Yes | Yes | Yes
Use on-premises multi-factor authentication | No | No | Yes
Use smart card authentication for additional protection | No | No | Yes

## Azure AD Licenses

- Azure Active Directory Free
- Pay-as-you-go licenses for specific features
- Office 365 Apps
- Azure Active Directory Premium P1
- Azure Active Directory Premium P2

[Details here](https://docs.microsoft.com/en-gb/learn/modules/intro-to-azure-ad/3-understand-licenses-terminology)

## Essential feature on Azure AD
- **Azure AD B2B** Use Azure AD to invite external users to your tenant

- **Azure AD B2C** You can also use Azure AD B2C to manage your customers' identities and access

- **Azure AD Domain Services(DS)** Azure AD DS lets you add virtual machines to a domain without needing domain controllers. Your internal staff users can access virtual machines by using their company Azure AD credentials.

[Details here](https://docs.microsoft.com/en-gb/learn/modules/intro-to-azure-ad/4-essential-features)

### App management

Your company might provide many apps that internal and external users rely on. Users might want to access these apps from different devices and locations. You can use Azure AD as a cloud-based solution to manage user access for all of these apps.

You can manage different categories of apps in Azure AD:

- **Azure AD App Gallery applications.** Thousands of SaaS apps are integrated with Azure AD. Find these apps in Azure Marketplace

- **Custom applications** You can register your company-built apps with Azure AD. You then control and monitor authentication for these apps.

- **Non-gallery applications.** You can manually add any apps that you don't see in the gallery.

- **On-premises applications.** You can add on-premises apps by configure Azure AD Application Proxy. This process creates secure remote access for your on-premises apps. To connect them, download and install the Application Proxy connector on-premises.

[More Details here] (https://docs.microsoft.com/en-gb/learn/modules/intro-to-azure-ad/4-essential-features)

## Protect your apps through conditional-access policies

Use conditional-access policies to require users to pass additional authentication challenges before they access an app. For example, you can configure a conditional-access policy to require users to complete a multi-factor authentication challenge after their credentials are verified and before they access the app.

Conditional-access policies are available for Premium P1 and Premium P2 license tiers.

## Monitor your app access

Azure AD can help monitor your app sign-ins by generating reports that cover sign-in dates, user details, apps the user has used, risk detection, location, and more. Access those reports through the Azure portal or specific APIs for programmatic usage.

Reports available for all licensing tiers.

## Azure AD Identity Protection

Azure AD Identity Protection helps you to automatically detect, investigate, and remediate identity risks for users. Identity Protection also lets you export all the information that was collected about risks. Export the information to third-party tools and solutions so that you can further analyze it.

Identity Protection uses risk policies to automatically detect and respond to threats. You configure a risk policy to set up how Identity Protection should respond to a particular type of risk. Use policies in this way to save time and give you peace of mind.

By using automated risk detection and remediation through Identity Protection, the admin first configures the risk policies. These policies then monitor for identity risks. When a risk is detected, the policies enforce measures to remediate it. For example, a policy might require a user to reset their password in response to a detected risk. The user then resets their password, and the risk is remediated.

You configure risk policies through the Azure portal. For example, the following risk policy detects user risks and remediates them by requiring the user to reset their password.

Identity Protection is available for the Premium P2 licensing tier.

## Get started with Azure AD

Your organization has decided to use Azure Active Directory (Azure AD) to manage secure access. Users include doctors, external healthcare partners, and all internal staff members. You've been asked to look into implementing secure access for your organization.

Here, you'll learn how to take a phased approach to deploying Azure AD for your organization. You'll learn how to lay a foundation, deploy Azure AD by creating a tenant, and associate a subscription with it.

[Deploy in phases](https://docs.microsoft.com/en-gb/learn/modules/intro-to-azure-ad/5-get-started)
A good way to deploy Azure AD is in phases. Your deployment is split into several stages. Each stage addresses a key aspect of Azure AD. A phase includes tasks that you'll need to complete before you go to the next stage. This approach lays a secure foundation for your Azure AD instance.

### Stage 1: Build a secure foundation

Configure baseline security features before you add or create user accounts. The work you do here helps ensure your Azure AD instance is in a secure state from the start. The following table describes your tasks.

| Task | Description | License needed
| - | - | - |
| **Assign more than one global administrator.**| Give at least two Azure AD accounts the global admin role. Make sure you don't use these accounts daily. Ensure the accounts have long and complicated passwords.| Free
| **User regular administrative roles where possible.** | Admins who aren't global admins should never have more permissions than they need to do their work. Use these regular admin roles by default. Avoid using the global admin roles unless you need to. | Free
| **Configure Privileged Identity Management (PIM) to track administrators | Use PIM to monitor how your admin roles are used. This action helps you improve your governance and compliance. | Azure AD Premium P2 
| **Configure self-service password reset. | Let internal users reset their passwords through policies that you configure. This action reduces the number of help desk tickets for password resets. | Free
| **Create a list of banned passwords.** | Use this list to prevent users from using passwords that are common phrases or words in your organization. Your list can include your company name or headquarters location, for example.| Free
| **Warn users to not reuse credentials** | When someone reuses the same credentials on multiple platforms, an attacker can use the credentials to access all of those platforms if a single platform is compromised.| Free
| **Set passwords to never expire for cloud-based user accounts** | Routine password resetting tempts users to increment their existing passwords. For example, they might change their password from R4ndom1Strong to R4ndom2Strong, and so on. In this case, because most of the password remained the same it increases the risk of using already exposed credentials to gain access to an account.| Free
| **Enforce multi-factor authentication through conditional-access policies.** | Configure conditional-access policies to require users to pass multiple authentication challenges before they can access an application.| Azure AD Premium P1
| **Configure Azure Active Directory Identity Protection (AADIP).** | Flag and block suspicious sign-ins and compromised user credentials for your organization's users. You can also use AADIP to automatically trigger multi-factor authentication or a password reset, depending on the severity of the detected risk.| Azure AD Premium P2

### Stage 2: Add users, manage devices, and configure synchronization

Now you can add users and plan how to handle external guest-user access. The following table describes your tasks in this stage.

| Task | Description | License needed
| - | - | - |
| **Install and configure Azure AD Connect.** | Use Azure AD Connect to synchronize users from your on-premises instance of Active Directory to Azure. | Free
| **Use password hash synchronization.** | You can synchronize password changes and detect and fix bad passwords. You get reports about leaked user credentials. | Free
| **Use password writeback** | Configure password writeback so any changes to passwords in Azure are written to your on-premises instance of Active Directory.| Azure AD Premium P1
| **Use Azure AD Connect Health** | Use Azure AD Connect Health to monitor the health statistics for your Azure AD Connect environment. | Azure AD Premium P1
| **Give users the licenses they need at a group level** | When you assign licenses at a group level, you control licensing for many users simultaneously. This action saves your organization time and reduces complexity. | Free
| **Use Azure AD B2B Collaboration for guest-user access.** | Use this resource to ensure that external healthcare partner users can use their own work or social identities to access your applications and services. You don't need to manage their credentials for them. | Required licenses depend on which features you want the guest users to access.
|  **Prepare a device-management strategy.** | Put together a plan based on which devices your company allows. For example, will you permit Bring Your Own Device (BYOD), or will the company accept only devices that it has given to users? | Free
| **Provide authentication methods that don't require passwords** | Make authentication more convenient. For example, if users have installed Microsoft Authenticator on their phones, they can receive a notification that provides a code to enter at sign-in, along with a PIN or a biometric attribute like their fingerprint.| Azure AD Premium P1

### Stage 3: Manage your applications

You can now integrate your applications with Azure AD. The following table describes your tasks in this stage.

| Task | Description | License needed
| - | - | - |
| **Identify applications** | Investigate the applications in your organization. Your organization could, for example, have applications on-premises or software-as-a-service (SaaS) applications in the cloud. Choose applications that you want to manage in Azure AD.| N/A
| **Use SaaS applications in the Azure AD gallery.** | Your organization probably uses SaaS applications that are already in the gallery and that you find in the Azure portal. Use these applications from the gallery whenever you can. You can save time by integrating your applications and Azure AD.| Free
| **Integrate your on-premises applications by using Application Proxy.** |  You can let Azure AD users sign in to your on-premises applications by using their Azure AD account. | Free

### Stage 4: Monitor your administrators, do access reviews, and automate user life cycles

Now you can address how much privilege your admins should have, and you can complete access reviews. In this stage, you also configure how to automate common user life-cycle tasks. The following table describes your tasks in this stage.

| Task | Description | License needed
| - | - | - |
| **Use PIM to control administrator access.** | Ensure that admins can use their account only after they pass a multi-factor authentication challenge or receive approval from an accepted approver. | Azure AD Premium P2
| **Complete access reviews for Azure AD directory roles in PIM.** | Configure access review policies in PIM so you can regularly review administrative access based on your organization's requirements for privileged roles. | Azure AD Premium P2
| **Configure dynamic group membership policies.** | Save time and effort by automatically adding users to specific groups based on known profile information, like department or region. For example, you can automatically add all users who are part of the human resources department to a user group called Human Resources. | Azure AD Premium P1 or P2
| **Use group-based application assigment.** | Use group-based access management to give all group members access to an application. When you use dynamic groups, users who are removed from a group automatically lose access to the application. This action helps keep your applications secure. | Free
| **Configure automated user account provisioning and deactivation.** | Automatically create application-specific accounts to allow users to use SaaS applications, based on existing Azure AD users and groups. You can also automatically deprovision user accounts when a user leaves the organization. This action keeps your organization protected from unauthorized access. | Free

### Create a tenant 

After you lay the groundwork for your instance of Azure AD, you can begin to configure and start using it. You need to create a tenant, which is considered a resource in Azure.

Use the Azure portal to create a tenant and a new Azure AD resource.

Use a form in the Azure portal to create your Azure AD directory

### Associate a subscription 

After you create your tenent, associate it with a subscription. In the Azure portal, go to your subscription and change it to your new directory.


