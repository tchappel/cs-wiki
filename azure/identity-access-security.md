# Identity, Access, and Security

## Directory Service

A central place to manage information about users, devices, applications and other resources within a network. It helps control who can access what.

**An identity and access management (IAM) service** is a system that manages digital identities and controls how users and devices authenticate and are authorized to access resources

there are __2 main types__ of directory services in the context of Microsoft:

1. **Active Directory (AD)** running on Windows Server: This is a directory service that organizations have traditionally used in their own physical locations (on-premises) to manage identities and access to resources within their internal network.

2. **Microsoft Entra ID**: This is Microsoft's cloud-based identity and access management service.

What does Microsoft Entra ID do?

Microsoft Entra ID provides several key services:

Authentication: This is the process of verifying a user's identity when they try to access applications or resources. This includes features like:

Self-service password reset: Allows users to reset their passwords without administrator intervention.

Multifactor authentication (MFA): Adds an extra layer of security by requiring users to provide more than one form of verification (e.g., password and a code from their phone).

Custom list of banned passwords: Allows organizations to prevent users from using weak or compromised passwords.

Smart lockout services: Helps protect against brute-force password attacks by temporarily locking accounts after too many failed login attempts.

Single Sign-On (SSO): This feature allows users to log in once with a single username and password and then access multiple applications without having to log in again. This simplifies the user experience and can improve security by centralizing identity management. When users change roles or leave the organization, managing their access becomes easier as it's tied to that single identity.

Application management: Microsoft Entra ID helps you manage both cloud and on-premises applications. Features include:
◦
Application Proxy: Allows users to securely access on-premises web applications from outside the network through Microsoft Entra ID.
◦
SaaS apps: Enables you to connect and manage various Software-as-a-Service (SaaS) applications (like Salesforce or Dropbox) through Microsoft Entra ID.
◦
The My Apps portal: Provides a central location for users to access all the applications they have permission to use.
◦
The SSO capabilities mentioned earlier also enhance application management.
•
Device management: Microsoft Entra ID can register devices in addition to user accounts. This allows for:
◦
Managing devices through tools like Microsoft Intune, which is a service for managing and securing mobile devices and applications. (Note: The text mentions Microsoft Intune, but doesn't fully explain what it is. It's a mobile device management (MDM) and mobile application management (MAM) provider).
◦
Device-based Conditional Access policies: These policies can restrict access to resources based on whether the device is known and managed, regardless of the user account trying to access it.
Connecting On-premises AD with Microsoft Entra ID
Initially, if you used on-premises Active Directory and also had cloud services using Microsoft Entra ID, you would have separate sets of user identities to manage. However, you can connect your on-premises Active Directory with Microsoft Entra ID to create a more consistent experience.
The text highlights Microsoft Entra Connect as a tool to achieve this connection. Microsoft Entra Connect synchronizes user identities between your on-premises Active Directory and Microsoft Entra ID. This synchronization is bidirectional, meaning changes in one system can be reflected in the other. This enables you to use features like SSO, multifactor authentication, and self-service password reset consistently across both your on-premises and cloud environments. This type of setup is often referred to as a hybrid identity solution.
Microsoft Entra Domain Services
Microsoft Entra Domain Services is a different service from Microsoft Entra ID, although it works in conjunction with it. It provides managed domain services in the cloud. These services include:
•
Domain join: Allows virtual machines (VMs) and other resources in Azure to join a domain, similar to how computers join an on-premises Active Directory domain.
•
Group Policy: Enables you to centrally manage the configuration and security settings of computers and users within the managed domain. (Note: Group Policy is a feature of Active Directory that allows administrators to define and enforce settings for users and computers).
•
Lightweight Directory Access Protocol (LDAP): A standard protocol for accessing and querying directory services.
•
Kerberos/NTLM authentication: These are common authentication protocols used in Windows environments.
The key benefit of Microsoft Entra Domain Services is that it provides these domain services without you having to deploy, manage, and patch domain controllers (DCs) in the cloud. Just like Microsoft manages the infrastructure for Microsoft Entra ID, it also handles the underlying infrastructure for Microsoft Entra Domain Services.
Why use Microsoft Entra Domain Services?
It's particularly useful for running legacy applications in the cloud that might not support modern authentication methods (like those used by Microsoft Entra ID) or when you don't want these applications to always need to look up directory information from your on-premises Active Directory. You can essentially move these older applications ("lift and shift") to the cloud into a Microsoft Entra Domain Services managed domain without having to fully modernize their authentication mechanisms or manage a traditional Active Directory infrastructure in Azure.
How Microsoft Entra Domain Services works
When you create a Microsoft Entra Domain Services managed domain:
•
You define a unique namespace, which becomes the domain name.
•
Two Windows Server domain controllers are automatically deployed in the Azure region you select. This pair of domain controllers is called a replica set.
•
Azure handles the management, configuration, and updates of these domain controllers, including backups and encryption of the stored data. You don't need to manage them directly.
Information Synchronization
It's important to understand how information flows between Microsoft Entra ID and Microsoft Entra Domain Services:
•
There is a one-way synchronization from Microsoft Entra ID to Microsoft Entra Domain Services. This means that users and groups created or managed in Microsoft Entra ID are replicated to the managed domain.
•
However, resources created directly within the Microsoft Entra Domain Services managed domain (like organizational units, group policy objects, etc.) are NOT synchronized back to Microsoft Entra ID.
•
In a hybrid environment where you have on-premises Active Directory, Microsoft Entra Connect synchronizes identity information from your on-premises AD to Microsoft Entra ID. This information is then, in turn, synchronized to the Microsoft Entra Domain Services managed domain. The provided diagram illustrates the synchronization from on-premises AD to Microsoft Entra ID.
Using Microsoft Entra Domain Services
Once you have a Microsoft Entra Domain Services managed domain, applications, services, and virtual machines in Azure that are connected to this domain can use familiar Active Directory features like:
•
Domain join
•
Group Policy
•
LDAP
•
Kerberos/NTLM authentication
This allows you to integrate your Azure-based resources with a managed domain environment, especially useful for scenarios involving legacy applications or the need for traditional domain services in the cloud.
Hopefully, this more detailed explanation clarifies the concepts presented in the text! Let me know if you have any more specific questions.

## Authentication (AuthN)

Authentication is the process of establishing the identity of a person, service, or device.

Azure supports multiple authentication methods, including standard passwords, single sign-on (SSO), multifactor authentication (MFA), and passwordless.

### Single Sign-On (SSO)

Simplifies authentication by allowing users to log in once and gain access to multiple applications without needing to re-enter credentials

### Multi-Factor Authentication (MFA)

Requires multiple authentication factors—typically:

- something you know (password) +
- something you have (e.g., phone, security key), or something you are (biometrics). 

MFA adds security layers but __still often relies on passwords as one of the factors__.

### Passwordless Authentication

__Eliminates passwords entirely__ and relies on other authentication methods, such as biometrics (fingerprint, facial recognition), security keys, or one-time passcodes. This reduces the risks associated with password breaches, phishing, and credential reuse.

Microsoft Entra ID offeres these three passwordless authentication options:

- Windows Hello for Business
- Microsoft Authenticator app
- FIDO2 security keys (Fast IDentity Online)


## Other concepts


Azure external identities
Microsoft Entra External ID
Azure AD B2C

The following capabilities make up External Identities:

Business to business (B2B) collaboration - Collaborate with external users by letting them use their preferred identity to sign-in to your Microsoft applications or other enterprise applications (SaaS apps, custom-developed apps, etc.). B2B collaboration users are represented in your directory, typically as guest users.
B2B direct connect - Establish a mutual, two-way trust with another Microsoft Entra organization for seamless collaboration. B2B direct connect currently supports Teams shared channels, enabling external users to access your resources from within their home instances of Teams. B2B direct connect users aren't represented in your directory, but they're visible from within the Teams shared channel and can be monitored in Teams admin center reports.
Microsoft Azure Active Directory business to customer (B2C) - Publish modern SaaS apps or custom-developed apps (excluding Microsoft apps) to consumers and customers, while using Azure AD B2C for identity and access management.

Azure conditional access

## Azure role-based access control (RBAC)

The principle of least privilege says you should only grant access up to the level needed to complete a task.

Azure provides built-in roles that describe common access rules for cloud resources. You can also define your own roles.

So, if you hire a new engineer and add them to the Azure RBAC group for engineers, they automatically get the same access as the other engineers in the same Azure RBAC group. Similarly, if you add additional resources and point Azure RBAC at them, everyone in that Azure RBAC group will now have those permissions on the new resources as well as the existing resources.

Scopes include:

A management group (a collection of multiple subscriptions).
A single subscription.
A resource group.
A single resource.
Observers, users managing resources, admins, and automated processes illustrate the kinds of users or accounts that would typically be assigned each of the various roles.

Azure RBAC is hierarchical, in that when you grant access at a parent scope, those permissions are inherited by all child scopes. For example:

When you assign the Owner role to a user at the management group scope, that user can manage everything in all subscriptions within the management group.
When you assign the Reader role to a group at the subscription scope, the members of that group can view every resource group and resource within the subscription.

Azure RBAC is enforced on any action that's initiated against an Azure resource that passes through Azure Resource Manager. Resource Manager is a management service that provides a way to organize and secure your cloud resources