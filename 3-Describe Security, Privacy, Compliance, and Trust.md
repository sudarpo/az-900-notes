# 3. Describe Security, Privacy, Compliance, and Trust (25-30%)

## 3.1. Describe securing network connectivity in Azure

### describe Network Security Groups (NSG) [ref-docs](https://docs.microsoft.com/en-us/azure/virtual-network/security-overview)

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

### describe Application Security Groups (ASG) [ref-docs](https://docs.microsoft.com/en-us/azure/virtual-network/application-security-groups)

Application security groups enable you to configure network security as a natural extension of an application's structure, allowing you to group virtual machines and define network security policies based on those groups.

- This feature allows you to reuse your security policy at scale without manual maintenance of explicit IP addresses. The platform handles the complexity of explicit IP addresses and multiple rule sets, allowing you to focus on your business logic.
- Application Security Groups help simplify how you can filter and control network traffic coming into your organization and how that network traffic is allowed to move. They allow you to isolate multiple workloads and provide additional levels of protection for your virtual network in a more easily manageable way.

![ASG](https://docs.microsoft.com/en-us/learn/wwl-azure/secure-network-connectivity/media/application-security-group-2.png)

> https://docs.microsoft.com/en-us/learn/modules/secure-network-connectivity/7-define-application-security-groups

### describe User Defined ~~Rules~~ Routes (UDR)

**User-defined**

- You can create custom, or user-defined(static), routes in Azure to override Azure's default system routes, or to add additional routes to a subnet's route table.
- In Azure, you create a route table, then associate the route table to zero or more virtual network subnets. Each subnet can have zero or one route table associated to it.

> https://docs.microsoft.com/en-gb/azure/virtual-network/virtual-networks-udr-overview#custom-routes

### describe Azure Firewall

[Azure Firewall](https://azure.microsoft.com/services/azure-firewall) is a managed, cloud-based, network security service that protects your Azure Virtual Network resources. It is a fully stateful firewall as a service with built-in high availability and unrestricted cloud scalability.

- You can create, enforce, and log, application and network connectivity policies across subscriptions, and virtual networks, centrally.
- Azure Firewall uses a static public IP address for your virtual network resources, which allows outside firewalls to identify traffic originating from your virtual network.
- The service is fully integrated with Azure Monitor for logging and analytics.

### describe Azure DDoS Protection (https://docs.microsoft.com/en-us/azure/virtual-network/ddos-protection-overview)

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

### choose an appropriate Azure security solution (https://docs.microsoft.com/en-us/learn/modules/secure-network-connectivity/8-choose-azure-security-solutions)

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

### describe the difference between authentication and authorization

- **Authentication**. Authentication is the process of _establishing the identity_ of a person or service looking to access a resource. It involves the act of challenging a party for legitimate credentials and provides the basis for creating a security principal for identity and access control use. It establishes if they are who they say they are.

- **Authorization**. Authorization is the process of _establishing what level of access_ an authenticated person or service has. It specifies what data they're allowed to access and what they can do with it.

### describe Azure Active Directory

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

### describe Azure Multi-Factor Authentication

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

### describe Azure Security Center (https://docs.microsoft.com/en-gb/azure/security-center/security-center-intro)

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

### describe Azure Security Center usage scenarios

#### Use Security Center for an incident response

Use Azure Security Center in different stages of an incident response. You can use Security Center during the detect, assess, and diagnose stages. Here are examples of how Security Center can be useful during the three initial incident response stages:

- **Detect** - Review the first indication of an event investigation. For example, use the Security Center dashboard to review the initial verification that a high-priority security alert was raised.
- **Assess** - Perform the initial assessment to obtain more information about the suspicious activity. For example, obtain more information about the security alert.
- **Diagnose** - Conduct a technical investigation and identify containment, mitigation, and workaround strategies. For example, follow the remediation steps described by Security Center in that particular security alert.

#### Use Security Center recommendations to enhance security

**Security policies and recommendations**

A security policy defines the set of controls that are recommended for resources within that specified subscription or resource group. In Security Center, you define policies according to your company's security requirements.

Security Center analyzes the security state of your Azure resources. When Security Center identifies potential security vulnerabilities, it creates recommendations based on the controls set in the security policy. The recommendations guide you through the process of configuring the needed security controls.

### describe Key Vault (https://docs.microsoft.com/en-gb/azure/key-vault/general/overview)

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

### describe Azure Information Protection (AIP) [ref-docs](https://docs.microsoft.com/en-us/azure/information-protection/what-is-information-protection)

Azure Information Protection is a cloud-based solution that helps organizations classify and (optionally) protect its documents and emails by applying labels.

Labels can be applied

- automatically (by administrators who define rules and conditions),
- manually (by users), or
- with a combination of both (where users are guided by recommendations).

### describe Azure Advanced Threat Protection (ATP) [ref-docs](https://docs.microsoft.com/en-us/azure-advanced-threat-protection/what-is-atp)

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

### describe policies and initiatives with Azure Policy

### describe Role-Based Access Control (RBAC)

### describe Locks

### describe Azure Advisor security assistance

### describe Azure Blueprints

## 3.5. Describe monitoring and reporting options in Azure

### describe Azure Monitor

### describe Azure Service Health

### describe the use cases and benefits of Azure Monitor and Azure Service Health

## 3.6. Describe privacy, compliance and data protection standards in Azure

### describe industry compliance terms such as GDPR, ISO and NIST

### describe the Microsoft Privacy Statement

### describe the Trust center

### describe the Service Trust Portal

### describe Compliance Manager

### determine if Azure is compliant for a business need

### describe Azure Government cloud services

### describe Azure China cloud services
