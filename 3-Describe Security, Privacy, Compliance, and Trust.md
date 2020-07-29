# 3. Describe Security, Privacy, Compliance, and Trust (25-30%)

## 3.1. Describe securing network connectivity in Azure

### 3.1.A. describe Network Security Groups (NSG) [ref-docs](https://docs.microsoft.com/en-us/azure/virtual-network/security-overview)

Network Security Groups (NSG) allow you to filter network traffic to and from Azure resources in an Azure virtual network. An NSG can contain multiple inbound and outbound security rules that enable you to filter traffic to and from resources by source and destination IP address, port, and protocol.

| Property              | Explanation                                                                                                                                                                                                                |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Name                  | A unique name within the network security group.                                                                                                                                                                           |
| Priority              | - A number between 100 and 4096. - Rules are processed in priority order, with lower numbers processed before higher numbers, because lower numbers have higher priority. - Once traffic matches a rule, processing stops. |
| Source or destination | Any, or an individual IP address, classless inter-domain routing (CIDR) block (10.0.0.0/24, for example), service tag, or application security group.                                                                      |
| Protocol              | TCP, UDP, ICMP or Any.                                                                                                                                                                                                     |
| Direction             | Whether the rule applies to inbound, or outbound traffic.                                                                                                                                                                  |
| Port range            | You can specify an individual or range of ports. For example, you could specify 80 or 10000-10005.                                                                                                                         |
| Action                | Allow or deny                                                                                                                                                                                                              |

- When you create a network security group, Azure creates a series of default rules to provide a baseline level of security.
- You cannot remove the default rules, but you can override them by creating new rules with higher priorities.
- Network security group security rules are evaluated by priority using the 5-tuple information (source, source port, destination, destination port, and protocol) to allow or deny the traffic.
- A **flow record** is created for existing connections.
- Communication is allowed or denied based on the connection state of the flow record.
- The flow record allows a network security group to be stateful.
  > If you specify an outbound security rule to any address over port 80, for example, it's not necessary to specify an inbound security rule for the response to the outbound traffic. You only need to specify an inbound security rule if communication is initiated externally. The opposite is also true. If inbound traffic is allowed over a port, it's not necessary to specify an outbound security rule to respond to traffic over the port.

### 3.1.B. describe Application Security Groups (ASG) [ref-docs](https://docs.microsoft.com/en-us/azure/virtual-network/application-security-groups)

Application security groups enable you to configure network security as a natural extension of an application's structure, allowing you to group virtual machines and define network security policies based on those groups.

- This feature allows you to reuse your security policy at scale without manual maintenance of explicit IP addresses. The platform handles the complexity of explicit IP addresses and multiple rule sets, allowing you to focus on your business logic.
- Application Security Groups help simplify how you can filter and control network traffic coming into your organization and how that network traffic is allowed to move. They allow you to isolate multiple workloads and provide additional levels of protection for your virtual network in a more easily manageable way.

![ASG](https://docs.microsoft.com/en-us/learn/wwl-azure/secure-network-connectivity/media/application-security-group-2.png)

> https://docs.microsoft.com/en-us/learn/modules/secure-network-connectivity/7-define-application-security-groups

### 3.1.C. describe User Defined ~~Rules~~ Routes (UDR)

**User-defined**

- You can create custom, or user-defined(static), routes in Azure to override Azure's default system routes, or to add additional routes to a subnet's route table.
- In Azure, you create a route table, then associate the route table to zero or more virtual network subnets. Each subnet can have zero or one route table associated to it.

> https://docs.microsoft.com/en-gb/azure/virtual-network/virtual-networks-udr-overview#custom-routes

### 3.1.D. describe Azure Firewall

[Azure Firewall](https://azure.microsoft.com/services/azure-firewall) is a managed, cloud-based, network security service that protects your Azure Virtual Network resources. It is a fully stateful firewall as a service with built-in high availability and unrestricted cloud scalability.

- You can create, enforce, and log, application and network connectivity policies across subscriptions, and virtual networks, centrally.
- Azure Firewall uses a static public IP address for your virtual network resources, which allows outside firewalls to identify traffic originating from your virtual network.
- The service is fully integrated with Azure Monitor for logging and analytics.

### 3.1.E. describe Azure DDoS Protection (https://docs.microsoft.com/en-us/azure/virtual-network/ddos-protection-overview)

Distributed Denial of Service (DDoS) attacks attempt to overwhelm and exhaust an application’s resources, making the application slow or unresponsive to legitimate users. DDoS attacks can be targeted at any endpoint that is publicly reachable through the internet.

The Azure DDoS Protection service protects your Azure applications by scrubbing traffic at the Azure network edge before it can impact your service's availability.

Azure DDoS Protection provides the following service tiers:

- **Basic**. The Basic service tier is automatically enabled as part of the Azure platform. Always-on traffic monitoring and real-time mitigation of common network-level attacks provide the same defenses that Microsoft’s online services use. Azure’s global network is used to distribute and mitigate attack traffic across regions.
- **Standard**. The Standard service tier provides additional mitigation capabilities that are tuned specifically to Microsoft Azure Virtual Network resources. DDoS Protection Standard is simple to enable and requires no application changes. Protection policies are tuned through dedicated traffic monitoring and machine learning algorithms. Policies are applied to public IP addresses which are associated with resources deployed in virtual networks, such as Azure Load Balancer and Application Gateway.

| Feature                                         | DDoS Protection Basic                 | DDoS Protection Standard                                   |
| ----------------------------------------------- | ------------------------------------- | ---------------------------------------------------------- |
| Active traffic monitoring & always on detection | Yes                                   | Yes                                                        |
| Automatic attack mitigations                    | Yes                                   | Yes                                                        |
| Availability guarantee                          | Azure Region                          | Application                                                |
| Mitigation policies                             | Tuned for Azure traffic region volume | Tuned for application traffic volume                       |
| Metrics & alerts                                | No                                    | Real time attack metrics & resource logs via Azure Monitor |
| Mitigation reports                              | No                                    | Post attack mitigation reports                             |
| Mitigation flow logs                            | No                                    | NRT log stream for SIEM integration                        |
| Mitigation policy customization                 | No                                    | Engage DDoS Experts                                        |
| Support                                         | Best effort                           | Access to DDoS Experts during an active attack             |
| SLA                                             | Azure Region                          | Application guarantee & cost protection                    |
| Pricing                                         | Free                                  | Monthly & usage based                                      |

#### Distributed Denial of Service (DDoS) standard protection

DDoS standard protection can mitigate the following types of attacks:

- Volumetric attacks. The attack's goal is to flood the network layer with a substantial amount of seemingly legitimate traffic.
- Protocol attacks. These attacks render a target inaccessible, by exploiting a weakness in the layer 3 and layer 4 protocol stack.
- Resource (application) layer attacks. These attacks target web application packets to disrupt the transmission of data between hosts.

### 3.1.F. choose an appropriate Azure security solution (https://docs.microsoft.com/en-us/learn/modules/secure-network-connectivity/8-choose-azure-security-solutions)

#### Perimeter layer

The network perimeter layer is about protecting organizations from network-based attacks against your resources. Identifying these attacks, alerting, and eliminating their impact is important to keep your network secure. To do this:

- Use Azure DDoS Protection to filter large-scale attacks before they can cause a denial of service for end users.
- Use perimeter firewalls with Azure Firewall to identify and alert on malicious attacks against your network.

#### Network layer

At this layer, the focus is on limiting network connectivity across all your resources to only allow what is required. Segment your resources and use network-level controls to restrict communication to only what is needed.

- Use NSGs to create rules about inbound and outbound communication at this layer.
- As best practices:
  - Limit communication between resources through segmenting your network and configuring access controls.
  - Deny by default.
  - Restrict inbound internet access and limit outbound where appropriate.
  - Implement secure connectivity to on-premises networks.

#### Combine services

**Network security groups and Azure Firewall**.

- Azure Firewall complements network security group functionality.
- Network security groups provide distributed network layer traffic filtering to limit traffic to resources within virtual networks in each subscription.
- Azure Firewall is a fully stateful, centralized network firewall-as-a-service, which provides network and application-level protection across different subscriptions and virtual networks.

**Application Gateway WAF and Azure Firewall**.

- WAF is a feature of Application Gateway that provides your web applications with centralized, inbound protection against common exploits and vulnerabilities.
- Azure Firewall provides inbound protection for non-HTTP/S protocols (for example, RDP, SSH, FTP), outbound network-level protection for all ports and protocols, and application-level protection for outbound HTTP/S.

## 3.2. Describe core Azure Identity services

### 3.2.A. describe the difference between authentication and authorization

- **Authentication**. Authentication is the process of _establishing the identity_ of a person or service looking to access a resource. It involves the act of challenging a party for legitimate credentials and provides the basis for creating a security principal for identity and access control use. It establishes if they are who they say they are.

- **Authorization**. Authorization is the process of _establishing what level of access_ an authenticated person or service has. It specifies what data they're allowed to access and what they can do with it.

### 3.2.B. describe Azure Active Directory

Azure Active Directory is a Microsoft cloud-based identity and access management service. Azure AD helps employees of an organization sign in and access resources:

- **External resources** might include Microsoft Office 365, the Azure portal, and thousands of other software as a service (SaaS) applications.
- **Internal resources** might include apps on your corporate network and intranet, along with any cloud apps developed by your own organization.

Azure AD provides services such as:

- Authentication. This includes verifying identity to access applications and resources, and providing functionality such as self-service password reset, multi-factor authentication (MFA), a custom banned password list, and smart lockout services.
- Single sign-on (SSO). Enables users to remember only one ID and one password to access multiple applications. A single identity is tied to a user, simplifying the security model. As users change roles or leave an organization, access modifications are tied to that identity, greatly reducing the effort needed to change or disable accounts.
- Application management. You can manage your cloud and on-premises apps using Azure AD Application Proxy, single sign-on, the My apps portal (also referred to as Access panel), and SaaS apps.
- Business to business (B2B) identity services. Manage your guest users and external partners while maintaining control over your own corporate data
- Business-to-customer (B2C) identity services. Customize and control how users sign up, sign in, and manage their profiles when using your apps with services.
- Device management. Manage how your cloud or on-premises devices access your corporate data.

Azure AD is intended for:

- IT administrators. Administrators can use Azure AD to control access to apps and their resources, based on your business requirements.
- App developers. Developers can use Azure AD to provide a standards-based approach for adding functionality to applications that you build, such as adding Single-Sign-On functionality to an app, or allowing an app to work with a user's pre-existing credentials and other functionality.
- Microsoft 365, Microsoft Office 365, Azure, or Microsoft Dynamics CRM Online subscribers. These subscribers are already using Azure AD. Each Microsoft 365, Office 365, Azure, and Dynamics CRM Online tenant is automatically an Azure AD tenant. You can immediately start to manage access to your integrated cloud apps using Azure AD.

Single sign-on with Azure Active Directory

By leveraging Azure AD for single sign-on you'll also have the ability to combine multiple data sources into an intelligent security graph. This security graph enables the ability to provide threat analysis and real-time identity protection to all accounts in Azure AD, including accounts that are synchronized from your on-premises AD. By using a centralized identity provider, you'll have centralized the security controls, reporting, alerting, and administration of your identity infrastructure.

### 3.2.C. describe Azure Multi-Factor Authentication

Azure Multi-Factor Authentication provides additional security for your identities by requiring two or more elements for full authentication.  
These elements fall into three categories:

- **Something you know** could be a password or the answer to a security question.
- **Something you possess** might be a mobile app that receives a notification, or a token-generating device.
- **Something you are** is typically some sort of biometric property, such as a fingerprint or face scan used on many mobile devices.

Multi-factor authentication (MFA) comes as part of the following Azure service offerings:

- **Azure Active Directory premium licenses**. These licenses provide full-featured use of Azure Multi-Factor Authentication Service (cloud) or Azure Multi-Factor Authentication Server (on-premises).
- **Multi-factor authentication for Office 365**. A subset of Azure Multi-Factor Authentication capabilities is available as a part of your Office 365 subscription.
- **Azure Active Directory global administrators**. Because global administrator accounts are highly sensitive, a subset of Azure Multi-Factor Authentication capabilities are available to protect these accounts.

## 3.3. Describe security tools and features of Azure

### 3.3.A. describe Azure Security Center (https://docs.microsoft.com/en-gb/azure/security-center/security-center-intro)

Azure Security Center

- is a monitoring service that provides threat protection across all of your services both in Azure, and on-premises.
- is a unified infrastructure security management system that strengthens the security posture of your data centers, and provides advanced threat protection across your hybrid workloads in the cloud - whether they're in Azure or not - as well as on premises.

Features

- Provide security recommendations based on your configurations, resources, and networks.
- Monitor security settings across on-premises and cloud workloads, and automatically apply required security to new services as they come online.
- Continuously monitor all your services and perform automatic security assessments to identify potential vulnerabilities before they can be exploited.
- Use machine learning to detect and block malware from being installed on your virtual machines and services. You can also define a list of allowed applications to ensure that only the apps you validate can execute.
- Analyze and identify potential inbound attacks and help to investigate threats and any post-breach activity that might have occurred.
- Provide just-in-time access control for ports, reducing your attack surface by ensuring the network only allows traffic that you require.

Azure Security Center is available in two tiers:

- **Free**. Available as part of your Azure subscription, this tier is limited to assessments and recommendations of Azure resources only.
- **Standard**. This tier provides a full suite of security-related services including continuous monitoring, threat detection, just-in-time access control for ports, and more.

Azure Security Center addresses the three most urgent security challenges:

- **Rapidly changing workloads** – It's both a strength and a challenge of the cloud. On the one hand, end users are empowered to do more. On the other, how do you make sure that the ever-changing services people are using and creating are up to your security standards and follow security best practices?
- **Increasingly sophisticated attacks** - Wherever you run your workloads, the attacks keep getting more sophisticated. You have to secure your public cloud workloads, which are, in effect, an Internet facing workload that can leave you even more vulnerable if you don't follow security best practices.
- **Security skills are in short supply** - The number of security alerts and alerting systems far outnumbers the number of administrators with the necessary background and experience to make sure your environments are protected. Staying up-to-date with the latest attacks is a constant challenge, making it impossible to stay in place while the world of security is an ever-changing front.

To help you protect yourself against these challenges, Security Center provides you with the tools to:

- **Strengthen security posture**: Security Center assesses your environment and enables you to understand the status of your resources, and whether they are secure.
- **Protect against threats**: Security Center assesses your workloads and raises threat prevention recommendations and security alerts.
- **Get secure faster**: In Security Center, everything is done in cloud speed. Because it is natively integrated, deployment of Security Center is easy, providing you with auto-provisioning and protection with Azure services.

### 3.3.B. describe Azure Security Center usage scenarios

#### Use Security Center for an incident response

Use Azure Security Center in different stages of an incident response. You can use Security Center during the detect, assess, and diagnose stages. Here are examples of how Security Center can be useful during the three initial incident response stages:

- **Detect** - Review the first indication of an event investigation. For example, use the Security Center dashboard to review the initial verification that a high-priority security alert was raised.
- **Assess** - Perform the initial assessment to obtain more information about the suspicious activity. For example, obtain more information about the security alert.
- **Diagnose** - Conduct a technical investigation and identify containment, mitigation, and workaround strategies. For example, follow the remediation steps described by Security Center in that particular security alert.

#### Use Security Center recommendations to enhance security

**Security policies and recommendations**

A security policy defines the set of controls that are recommended for resources within that specified subscription or resource group. In Security Center, you define policies according to your company's security requirements.

Security Center analyzes the security state of your Azure resources. When Security Center identifies potential security vulnerabilities, it creates recommendations based on the controls set in the security policy. The recommendations guide you through the process of configuring the needed security controls.

### 3.3.C. describe Key Vault (https://docs.microsoft.com/en-gb/azure/key-vault/general/overview)

Azure Key Vault is a centralized cloud service for storing your applications' secrets.

- Key Vault helps you control your applications' secrets by keeping them in a single, central location and by providing secure access, permissions control, and access logging capabilities.
- AWS: _Key Management Service (KMS), and CloudHSM_

Usage scenarios

- **Secrets Management** - Azure Key Vault can be used to Securely store and tightly control access to tokens, passwords, certificates, API keys, and other secrets
- **Key Management** - Azure Key Vault can also be used as a Key Management solution. Azure Key Vault makes it easy to create and control the encryption keys used to encrypt your data.
- **Certificate Management** - Azure Key Vault is also a service that lets you easily provision, manage, and deploy public and private Transport Layer Security/Secure Sockets Layer (TLS/SSL) certificates for use with Azure and your internal connected resources.
- **Store secrets backed by Hardware Security Modules** - The secrets and keys can be protected either by software or FIPS 140-2 Level 2 validated HSMs

Key Vault benefits

- **Centralized application secrets**. Centralizing storage for application secrets allows you to control their distribution and reduces the chances that secrets may be accidentally leaked.
- **Securely stored secrets and keys**. Azure uses industry-standard algorithms, key lengths, and HSMs, and access requires proper authentication and authorization.
- **Monitor access and use**. Using Key Vault, you can monitor and control access to company secrets.
- **Simplified administration of application secrets**. Key Vault makes it easier to enroll and renew certificates from public Certificate Authorities (CAs). You can also scale up and replicate content within regions and use standard certificate management tools.
- **Integrate with other Azure services**. You can integrate Key Vault with storage accounts, container registries, event hubs and many more Azure services.

### 3.3.D. describe Azure Information Protection (AIP) [ref-docs](https://docs.microsoft.com/en-us/azure/information-protection/what-is-information-protection)

Azure Information Protection is a cloud-based solution that helps organizations classify and (optionally) protect its documents and emails by applying labels.

Labels can be applied

- automatically (by administrators who define rules and conditions),
- manually (by users), or
- with a combination of both (where users are guided by recommendations).

### 3.3.E. describe Azure Advanced Threat Protection (ATP) [ref-docs](https://docs.microsoft.com/en-us/azure-advanced-threat-protection/what-is-atp)

Azure Advanced Threat Protection is a cloud-based security solution that identifies, detects, and helps you investigate advanced threats, compromised identities, and malicious insider actions directed at your organization.

- Azure ATP is capable of detecting known malicious attacks and techniques, security issues, and risks against your network.

Azure ATP consists of the following components:

- Azure ATP portal  
  The Azure ATP portal allows creation of your Azure ATP instance, displays the data received from Azure ATP sensors, and enables you to monitor, manage, and investigate threats in your network environment.

- Azure ATP sensor  
  Azure ATP sensors are installed directly on your domain controllers. The sensor directly monitors domain controller traffic, without the need for a dedicated server, or configuration of port mirroring.

- Azure ATP cloud service  
  Azure ATP cloud service runs on Azure infrastructure and is currently deployed in the US, Europe, and Asia. Azure ATP cloud service is connected to Microsoft's intelligent security graph.

Azure ATP enables SecOp analysts and security professionals struggling to detect advanced attacks in hybrid environments to:

- Monitor users, entity behavior, and activities with learning-based analytics
- Protect user identities and credentials stored in Active Directory
- Identify and investigate suspicious user activities and advanced attacks throughout the kill chain
- Provide clear incident information on a simple timeline for fast triage

## 3.4. Describe Azure governance methodologies

### 3.4.A. describe policies and initiatives with [Azure Policy](https://docs.microsoft.com/en-gb/azure/governance/policy/overview)

Azure Policy is a service in Azure that you use to create, assign, and, manage policies.

- These policies enforce different rules and effects over your resources, so those resources stay compliant with your corporate standards and service-level agreements (SLAs).
- Azure Policy does this by using policies and initiatives. It runs evaluations of your resources and scans for those not compliant with the policies you have created.
- Azure Policy comes with a number of built-in policy and initiative definitions that you can use, under categories such as Storage, Networking, Compute, Security Center, and Monitoring.
- Common use cases for Azure Policy include implementing governance for resource consistency, regulatory compliance, security, cost, and management.

Three steps to creating an implementing an Azure policy

- Create a policy definition
- Assign the definition to resource
- Review the evaluation results

#### [Policy Definition](https://docs.microsoft.com/en-gb/azure/governance/policy/overview#policy-definition)

- Azure Policy evaluates resources in Azure by comparing the properties of those resources to business rules.
- These business rules, described in JSON format, are known as **policy definitions**.
- To simplify management, several business rules can be grouped together to form a **policy initiative** (sometimes called a _policySet_).
- A **policy initiative** / an **initiative definition** is a set of policy definitions to help track your compliance state for a larger goal. Initiative assignments reduce the need to make several initiative definitions for each scope.

#### Assign the definition to resource | [Assignment](https://docs.microsoft.com/en-gb/azure/governance/policy/overview#assignments)

- An assignment is a policy definition or initiative that has been assigned to take place within a specific scope.
- This scope could range from a management group to an individual resource.
- The term scope refers to all the resources, resource groups, subscriptions, or management groups that the definition is assigned to.
- Policy assignments are inherited by all child resources.

#### Review the policy evaluation results

- When a condition is evaluated against your existing resources it is marked compliant or non-compliant.
- You can review the non-compliant policy results and take any action that is needed.
- Policy evaluation happens about once an hour.

#### Azure Policy and RBAC

There are a few key differences between Azure Policy and role-based access control (RBAC).

- Azure Policy evaluates state by examining properties on resources that are represented in Resource Manager and properties of some Resource Providers.
- Azure Policy doesn't restrict actions (also called operations).
- Azure Policy ensures that resource state is compliant to your business rules without concern for who made the change or who has permission to make a change.
- RBAC focuses on managing user actions at different scopes.
- If control of an action is required, then RBAC is the correct tool to use.
- Even if an individual has access to perform an action, if the result is a non-compliant resource, Azure Policy still blocks the create or update.

The combination of RBAC and Azure Policy provide full scope control in Azure.

### 3.4.B. describe Role-Based Access Control (RBAC) [ref-docs](https://docs.microsoft.com/en-us/azure/role-based-access-control/overview)

**Role-based access control** provides fine-grained access management for Azure resources, enabling you to grant users only the rights they need to perform their jobs.

- Azure RBAC helps you manage who has access to Azure resources, what they can do with those resources, and what areas they have access to.
- The way you control access to resources using Azure RBAC is to create role assignments.
- A role assignment consists of three elements: security principal, role definition, and scope.

#### Security principal

- A security principal is an object that represents a user, group, service principal, or managed identity that is requesting access to Azure resources.
- User - An individual who has a profile in Azure Active Directory. You can also assign roles to users in other tenants. For information about users in other organizations, see Azure Active Directory B2B.
- Group - A set of users created in Azure Active Directory. When you assign a role to a group, all users within that group have that role.
- Service principal - A security identity used by applications or services to access specific Azure resources. You can think of it as a user identity (username and password or certificate) for an application.
- Managed identity - An identity in Azure Active Directory that is automatically managed by Azure. You typically use managed identities when developing cloud applications to manage the credentials for authenticating to Azure services.

#### Role definition / Role

- A role definition / a role is a collection of permissions.
- A role definition lists the operations that can be performed, such as read, write, and delete.
- The following lists four fundamental built-in roles. The first three apply to all resource types.
  - Owner - Has full access to all resources including the right to delegate access to others.
  - Contributor - Can create and manage all types of Azure resources but can't grant access to others.
  - Reader - Can view existing Azure resources.
  - User Access Administrator - Lets you manage user access to Azure resources.

#### Scope

- Scope is the set of resources that the access applies to.
- You can specify a scope at multiple levels: management group, subscription, resource group, or resource.
- Scopes are structured in a parent-child relationship.

#### Role assignments

- A role assignment is the process of attaching a role definition to a user, group, service principal, or managed identity at a particular scope for the purpose of granting access.
- Access is granted by creating a role assignment, and access is revoked by removing a role assignment.
- Azure RBAC is an additive model, so your effective permissions are the sum of your role assignments.
- RBAC uses an allow model. This means that when you are assigned a role, RBAC _allows_ you to perform certain actions, such as read, write, or delete.

#### Deny assignments (https://docs.microsoft.com/en-us/azure/role-based-access-control/deny-assignments)

- Previously, Azure RBAC was an allow-only model with no deny, but now Azure RBAC supports deny assignments in a limited way.
- Similar to a role assignment, a deny assignment attaches a set of deny actions to a user, group, service principal, or managed identity at a particular scope for the purpose of denying access.
- **A role assignment** defines a set of actions that are allowed, while **a deny assignment** defines a set of actions that are not allowed.
- Azure Blueprints and Azure managed apps are the only way that deny assignments can be created. You can't directly create your own deny assignments.

> https://docs.microsoft.com/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles

### 3.4.C. describe Locks (https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/lock-resources)

- Resource locks help you prevent accidental deletion or modification of your Azure resources.
- You can set the lock level to CanNotDelete or ReadOnly.
- **CanNotDelete** (in Azure Portal: Delete) - means authorized users can still read and modify a resource, but they can't delete the resource.
- **ReadOnly** (in Azure Portal: Read-only) - means authorized users can read a resource, but they can't delete or update the resource.
  - Applying this lock is similar to restricting all authorized users to the permissions granted by the **Reader** role.

**How locks are applied** When you apply a lock at a parent scope, all resources within that scope inherit the same lock. Even resources you add later inherit the lock from the parent. The most restrictive lock in the inheritance takes precedence.

**Who can create or delete locks**? To create or delete management locks, you must have access to Microsoft.Authorization/_ or Microsoft.Authorization/locks/_ actions. Of the built-in roles, only Owner and User Access Administrator are granted those actions.

![azure lock](https://docs.microsoft.com/en-gb/learn/wwl-azure/describe-azure-governance-methodologie/media/resource-locks.png)

### 3.4.D. describe Azure Advisor security assistance

Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources. It integrates with Azure Security Center to bring you security recommendations. You can get security recommendations from the Security tab on the Advisor dashboard.

Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources. It periodically analyzes the security state of your Azure resources. When Security Center identifies potential security vulnerabilities, it creates recommendations. The recommendations guide you through the process of configuring the controls you need.

> https://docs.microsoft.com/en-us/azure/advisor/advisor-security-recommendations  
> https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations

### 3.4.E. describe Azure Blueprints (https://docs.microsoft.com/en-gb/azure/governance/blueprints/overview)

- Azure Blueprints enable cloud architects to define a repeatable set of Azure resources that implement and adhere to an organization's standards, patterns, and requirements.
- Azure Blueprint enables development teams to rapidly build and deploy new environments with the knowledge that they're building within organizational compliance with a set of built-in components that speed up development and delivery.
- is a declarative way to orchestrate the deployment of various resource templates and other artifacts, such as: Role assignments; Policy assignments; Azure Resource Manager templates; Resource groups.

The process of implementing Azure Blueprint consists of the following high-level steps:

- Create an Azure Blueprint.
- Assign the blueprint.
- Track the blueprint assignments.

With Azure Blueprint, the relationship between the blueprint definition (what should be deployed) and the blueprint assignment (what was deployed) is preserved. Maintaining relationships, in this way, improves auditing and tracking capabilities.

When Azure Resource Manager Templates deploy resources, they have no active relationship with the deployed resources (they exist in a local environment or in source control).

### 3.4.F. Subscription governance

There are mainly three aspects to consider in relation to creating and managing subscriptions: Billing, Access Control, and Subscription limits.

- **Billing**: Reports can be generated by subscriptions, if you have multiple internal departments and need to do "chargeback", a possible scenario is to create subscriptions by department or project.

- **Access Control**: A subscription is a deployment boundary for Azure resources and every subscription is associated with an Azure AD tenant that provides administrators the ability to set up role-based access control (RBAC).  
  When designing a subscription model, one should consider the deployment boundary factor, some customers have separate subscriptions for Development and Production, each one is isolated from each other from a resource perspective and managed using RBAC.

- **Subscription Limits**: Subscriptions are also bound to some hard limitations.  
  For example, the maximum number of Express Route circuits per subscription is 10. Those limits should be considered during the design phase, if there is a need to go over those limits in particular scenarios, then additional subscriptions may be needed. If you hit a hard limit, there is no flexibility.

## 3.5. Describe monitoring and reporting options in Azure

#### Tags (https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/tag-resources)

- You apply tags to your Azure resources giving metadata to logically organize them into a taxonomy.
- Each tag consists of a name and a value pair.
  - can retrieve all the resources in your subscription with that tag name and value.
  - to retrieve related resources from different resource groups.
  - organize resources for billing or management.
- You can use Azure Policy to enforce tagging values and rules on resources.'

**Tag limitations**

- Not all resource types support tags.
- Each resource or resource group can have a maximum of 50 tag name/value pairs.
  - Currently, storage accounts only support 15 tags, but that limit will be raised to 50 in a future release.
  - If you need to apply more tags than the maximum allowed number, use a JSON string for the tag value.
  - The JSON string can contain many values that are applied to a single tag name. A resource group can contain many resources that each have 50 tag name/value pairs.
- The tag name is limited to 512 characters, and the tag value is limited to 256 characters.
  - For storage accounts, the tag name is limited to 128 characters, and the tag value is limited to 256 characters.
- Virtual Machines and Virtual Machine Scale Sets are limited to a total of 2048 characters for all tag names and values.
- Tags applied to the resource group are not inherited by the resources in that resource group.

### 3.5.A. describe Azure Monitor (https://docs.microsoft.com/en-gb/azure/azure-monitor/overview)

Azure Monitor maximizes the availability and performance of your applications by delivering a comprehensive solution for collecting, analyzing, and acting on telemetry from your cloud and on-premises environments.

- AWS equivalent: CloudWatch; X-Ray; EC2 Systems Manager; CloudTrail
- Activity logs record when resources are created or modified.
- Metrics tell you how the resource is performing and the resources that it's consuming.

![azure monitor](https://docs.microsoft.com/en-gb/azure/azure-monitor/media/overview/overview.png)

Azure Monitor collects data from each of the following tiers:

- Application monitoring data: Data about the performance and functionality of the code you have written, regardless of its platform.
- Guest OS monitoring data: Data about the operating system on which your application is running. This could be running in Azure, another cloud, or on-premises.
- Azure resource monitoring data: Data about the operation of an Azure resource.
- Azure subscription monitoring data: Data about the operation and management of an Azure subscription, as well as data about the health and operation of Azure itself.
- Azure tenant monitoring data: Data about the operation of tenant-level Azure services, such as Azure Active Directory.

#### Insights

- **Application Insights**, monitors the availability, performance, and usage of your web applications whether they're hosted in the cloud or on-premises.
- **Azure Monitor for containers** is a feature designed to monitor the performance of container workloads deployed to managed Kubernetes clusters hosted on Azure Kubernetes Service (AKS).
  - It gives you performance visibility by collecting memory and processor metrics from controllers, nodes, and containers that are available in Kubernetes through the Metrics API.
- **Azure Monitor for VMs** monitors your Azure virtual machines (VM) at scale by analyzing the performance and health of your Windows and Linux VMs, including their different processes and interconnected dependencies on other resources and external processes.
- **Monitoring solutions** in Azure Monitor are packaged sets of logic that provide insights for a particular application or service. They include logic for collecting monitoring data for the application or service, queries to analyze that data, and views for visualization.

#### Visualize

- **Azure dashboards** allow you to combine different kinds of data, including both metrics and logs, into a single pane in the Azure portal. You can optionally share the dashboard with other Azure users.
- **Views** visually present log data in Azure Monitor. Each view includes a single tile that drills down to a combination of visualizations such as bar and line charts in addition to lists summarizing critical data.
- **Power BI** is a business analytics service that provides interactive visualizations across a variety of data sources and is an effective means of making data available to others within and outside your organization.
- **Azure Monitor Workbooks** provide a flexible canvas for data analysis and the creation of rich visual reports within the Azure portal.

### 3.5.B. describe Azure Service Health

Azure Service Health is a suite of experiences that provide personalized guidance and support when issues with Azure services affect you.

- It can notify you, help you understand the impact of issues, and keep you updated as the issue is resolved.
- Help you prepare for planned maintenance and changes that could affect the availability of your resources.

1. **Azure Status** provides a global view of the health state of Azure services. With Azure Status, you can get up-to-the-minute information on service availability.
2. **Service Health** provides you with a customizable dashboard that tracks the state of your Azure services in the regions where you use them.

   - You can track active events such as ongoing service issues, upcoming planned maintenance, or relevant Health advisories.
   - You can use the Service Health dashboard to create and manage service Health alerts, which notify you whenever there are service issues that affect you.

3. Resource Health helps you diagnose and obtain support when an Azure service issue affects your resources. It provides you details with about the current and past state of your resources.

### 3.5.C. describe the use cases and benefits of Azure Monitor and Azure Service Health

https://docs.microsoft.com/en-gb/azure/azure-monitor/monitor-reference  
https://docs.microsoft.com/en-gb/azure/azure-monitor/continuous-monitoring  
https://docs.microsoft.com/en-us/azure/service-health/overview

## 3.6. Describe privacy, compliance and data protection standards in Azure

### 3.6.A. describe industry compliance terms such as GDPR, ISO and NIST

#### General Data Protection Regulation (GDPR)

The European Union GDPR gives rights to people (known in the regulation as data subjects) to manage the personal data that has been collected by an employer or other type of agency or organization (known as the data controller or just controller).

- Personal data is defined very broadly under the GDPR as any data that relates to an identified or identifiable natural person.
- The GDPR gives data subjects specific rights to their personal data; these rights include
  - obtaining copies of personal data,
  - requesting corrections to it,
  - restricting the processing of it,
  - deleting it, or
  - receiving it in an electronic format so it can be moved to another controller.
- A formal request by a data subject to a controller to take an action on their personal data is called a Data Subject Request or DSR.

> https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr?view=o365-worldwide  
> https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr-arc-azure?view=o365-worldwide

> https://docs.microsoft.com/en-us/azure/compliance/  
> https://docs.microsoft.com/en-gb/microsoft-365/compliance/offering-home?view=o365-worldwide

#### International Organization of Standards/International Electrotechnical Commission (ISO/IEC) 27018.

Microsoft is the first cloud provider to have adopted the ISO/IEC 27018 code of practice, covering the processing of personal information by cloud service providers.

- ISO 20000-1:2011 Information Technology Service Management
- ISO 22301:2012 Business Continuity Management Standard
- ISO 27001:2013 Information Security Management Standards
- ISO 27017:2015 Code of Practice for Information Security Controls
- ISO 27018 Code of Practice for Protecting Personal Data in the Cloud
- ISO 27701 Privacy Information Management System (PIMS)
- ISO 9001:2015 Quality Management Systems Standards

#### NIST National Institute of Standards and Technology

- NIST Cybersecurity Framework (CSF) is a voluntary Framework that consists of standards, guidelines, and best practices to manage cybersecurity-related risks.

Microsoft cloud services have undergone independent, third-party Federal Risk and Authorization Management Program (FedRAMP) Moderate and High Baseline audits and are certified according to the FedRAMP standards. Additionally, through a validated assessment performed by the Health Information Trust Alliance (HITRUST), a leading security and privacy standards development and accreditation organization, Office 365 is certified to the objectives specified in the NIST CSF.

> https://www.microsoft.com/trustcenter/compliance/complianceofferings

### 3.6.B. describe the Microsoft Privacy Statement (https://privacy.microsoft.com/privacystatement)

The Microsoft privacy statement explains what personal data Microsoft processes, how Microsoft processes it, and for what purposes.

This privacy statement explains the personal data Microsoft processes, how Microsoft processes it, and for what purposes.

### 3.6.C. describe the Trust center (https://www.microsoft.com/en-sg/trust-center)

- The Trust Center is a website resource containing information and details about how Microsoft implements and supports security, privacy, compliance, and transparency in all Microsoft cloud products and services.
- The Trust Center is an important part of the Microsoft Trusted Cloud Initiative and provides support and resources for the legal and compliance community.

Provides:

- In-depth information about security, privacy, compliance offerings, policies, features, and practices across Microsoft cloud products.
- Recommended resources in the form of a curated list of the most applicable and widely used resources for each topic.
- Information specific to key organizational roles, including business managers, tenant admins or data security teams, risk assessment and privacy officers, and legal compliance teams.
- Cross-company document search, which is coming soon and will enable existing cloud service customers to search the Service Trust Portal.
- Direct guidance and support for when you can't find what you're looking for.

### 3.6.D. describe the Service Trust Portal

- Service Trust Portal (STP) hosts the Compliance Manager service, and
- is the Microsoft public site for publishing audit reports and other compliance-related information relevant to Microsoft’s cloud services.
- users can download audit reports produced by external auditors and gain insight from Microsoft-authored reports that provide details on how Microsoft builds and operates its cloud services.
- also includes information about how Microsoft online services can help your organization maintain and track compliance with standards, laws, and regulations, such as: ISO; SOC; NIST; FedRAMP

Service Trust Portal is a companion feature to the Trust Center, and allows you to:

- Access audit reports across Microsoft cloud services on a single page.
- Access compliance guides to help you understand how can you use Microsoft cloud service features to manage compliance with various regulations.
- Access trust documents to help you understand how Microsoft cloud services help protect your data.

To access some Service Trust Portal materials, you must sign in as an authenticated user with your Microsoft cloud services account (either an Azure AD organization account or a Microsoft account), and then review and accept the Microsoft Non-Disclosure Agreement for Compliance Materials.

### 3.6.E. describe Compliance Manager

- Compliance Manager is a workflow-based risk assessment dashboard within the Trust Portal that enables you to track, assign, and verify your organization's regulatory compliance activities related to Microsoft professional services and Microsoft cloud services such as Office 365, Dynamics 365, and Azure.
- Compliance Manager provides you with a dashboard view of standards and regulations and assessments that contain Microsoft's control implementation details and test results and customer control implementation guidance and tracking for your organization to enter.
- Compliance Manager provides certification assessment control definitions, guidance on implementation and testing of controls, risk-weighted scoring of controls, role-based access management, and an in-place control action assignment workflow to track control implementation, testing status and evidence management.
- Compliance Manager provides ongoing risk assessments with a risk-based scores reference displayed in a dashboard view for regulations and standards. Alternatively, you can create assessments for the regulations or standards that matter more to your organization.
- Provides a Compliance Score to help you track your progress and prioritize the auditing controls that will help reduce your organization's exposure to risk.

> https://docs.microsoft.com/en-us/microsoft-365/compliance/meet-data-protection-and-regulatory-reqs-using-microsoft-cloud?view=o365-worldwide  
> https://docs.microsoft.com/en-us/microsoft-365/compliance/compliance-manager-overview?view=o365-worldwide

### 3.6.F. determine if Azure is compliant for a business need

https://docs.microsoft.com/en-gb/microsoft-365/compliance/offering-home?view=o365-worldwide
https://azure.microsoft.com/en-us/resources/microsoft-azure-compliance-offerings/

> With the endorsement of cloud computing — including the use of public clouds — by the Monetary Authority of Singapore (MAS) and support from the Association of Banks in Singapore (ABS), Microsoft published the Microsoft response to MAS outsourcing guidelines and ABS guidance and a Compliance Checklist for financial institutions in Singapore. Together they demonstrate how financial firms can move data and workloads to the Microsoft Cloud with the confidence that they are complying with MAS guidelines and complete a self-assessment of their outsourcing arrangements against the new guidelines.
> https://docs.microsoft.com/en-gb/microsoft-365/compliance/offering-mas-abs-singapore?view=o365-worldwide

#### Service Organization Controls (SOC)

**SOC 1, 2, and 3 Reports overview**  
Rhe American Institute of Certified Public Accountants (AICPA) has developed the _Service Organization Controls (SOC) framework_, a standard for controls that safeguard the confidentiality and privacy of information stored and processed in the cloud.

- A SOC 1 audit, intended for CPA firms that audit financial statements, evaluates the effectiveness of a CSP's internal controls that affect the financial reports of a customer using the provider's cloud services.
- A SOC 2 audit gauges the effectiveness of a CSP's system based on the AICPA Trust Service Principles and Criteria.

#### HIPAA and the HITECH Act overview

The Health Insurance Portability and Accountability Act (HIPAA) is a US healthcare law that establishes requirements for the use, disclosure, and safeguarding of individually identifiable health information. It applies to covered entities — doctors' offices, hospitals, health insurers, and other healthcare companies — with access to patients' protected health information (PHI), as well as to business associates, such as cloud service and IT providers, that process PHI on their behalf. (Most covered entities do not carry out functions such as claims or data processing on their own; they rely on business associates to do so.)

HIPAA regulations require that covered entities and their business associates — in this case, Microsoft when it provides services, including cloud services, to covered entities — enter into contracts to ensure that those business associates will adequately protect PHI. These contracts, or BAAs, clarify and limit how the business associate can handle PHI, and set forth each party's adherence to the security and privacy provisions set forth in HIPAA and the HITECH Act. Once a BAA is in place, Microsoft customers — covered entities — can use its services to process and store PHI.

### 3.6.G. describe Azure Government cloud services (https://docs.microsoft.com/en-gb/azure/azure-government/documentation-government-welcome)

Azure Government is a separate instance of the Microsoft Azure service. It addresses the security and compliance needs of US federal agencies, state and local governments, and their solution providers.

- Azure Government offers physical isolation from non-US government deployments and provides screened US personnel.
- To provide the highest level of security and compliance, Azure Government uses physically isolated datacenters and networks (located only in the US).
- Azure Government customers (US federal, state, and local government or their partners) are subject to validation of eligibility.
- Most services are the same on both Azure Government and Public Azure. However, there are some differences that you should be aware of. Details are available at [Compare Azure Government and global Azure](https://docs.microsoft.com/en-us/azure/azure-government/compare-azure-government-global-azure).

### 3.6.H. describe Azure China cloud services (https://docs.microsoft.com/en-us/azure/china/)

Azure China 21Vianet is operated by 21Vianet is a physically separated instance of cloud services located in China, independently operated and transacted by Shanghai Blue Cloud Technology Co., Ltd. ("21Vianet"), a wholly owned subsidiary of Beijing 21Vianet Broadband Data Center Co., Ltd.

- The Azure services are based on the same Azure, Office 365, and Power BI technologies that make up the Microsoft global cloud service, with comparable service levels.
- Azure agreements and contracts in China, where applicable, are signed between customers and 21Vianet.
- Azure includes the core components of IaaS, PaaS, and SaaS. These components include network, storage, data management, identity management, and many other services.
- Azure China 21Vianet supports most of the same services that global Azure has, such as geosynchronous data replication and autoscaling. Even if you already use global Azure services, to operate in China you may need to rehost or refactor some or all your applications or services.

> https://support.azure.cn/en-us/support/faq/
