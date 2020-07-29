# 4. Describe Azure Pricing, Service Level Agreements, and Lifecycles (20-25%)

## 4.1. Describe Azure subscriptions

### 4.1.A. describe an Azure Subscription

An Azure subscription is a logical unit of Azure services that links to an Azure account, which is an identity in Azure Active Directory (Azure AD) or in a directory that an Azure AD trusts.

- An account can have one subscription or multiple subscriptions that have different billing models and to which you apply different access-management policies.
- Two types of **subscription boundaries** that you can use, including:
  1. **Billing boundary**. This subscription type determines how an Azure account is billed for using Azure. You can create multiple subscriptions for different types of billing requirements, and Azure will generate separate billing reports and invoices for each subscription so that you can organize and manage costs.
  2. **Access control boundary**. Azure will apply access-management policies at the subscription level, and you can create separate subscriptions to reflect different organizational structures. An example is that within a business, you have different departments to which you apply distinct Azure subscription policies. This allows you to manage and control access to the resources that users provision with specific subscriptions.

### 4.1.B. describe the uses and options with Azure subscriptions such access control and offer types

Create additional Azure subscriptions to separate:

- **Environments**: set up separate environments for development and testing, security, or to isolate data for compliance reasons.
- **Organizational structures**: You can create subscriptions to reflect different organizational structures. E.g. limit a team to lower-cost resources, while allowing the IT department a full range.
- **Billing**: You might want to also create additional subscriptions for billing purposes. E.g. subscription for your production workloads and another subscription for your development and testing workloads.
- **Subscription limits**: Subscriptions are bound to some hard limitations. For example, the maximum number of Express Route circuits per subscription is 10. Those limits should be considered as you create subscriptions on your account. If there is a need to go over those limits in particular scenarios, then you might need additional subscriptions.

#### Billing

- Billing account => Billing profile => Invoice section => Subscription
- Create a **billing profile** to group multiple invoices within the same billing account.
- Each billing profile has its own monthly invoice and payment method.
- Organize multiple subscriptions into invoice sections.
- Each invoice section is a line item on the invoice that shows the charges incurred that month.

![azure billing](https://docs.microsoft.com/en-us/learn/modules/create-an-azure-account/media/4-billing-structure-overview.png)

#### Offer types

- **A free account**. Get started with 12 months of popular free services, a credit to explore any Azure service for 30 days, and 25+ services that are always free.
- **Pay-As-You-Go**. This subscription allows you to pay for what you use by attaching a credit or debit card to your account. Organizations can apply to Microsoft for invoicing privileges.
- **Member offers**. Your existing membership to certain Microsoft products and services affords you credits for your Azure account and reduced rates on Azure services. For example, member offers are available to Microsoft Visual Studio subscribers, Microsoft Partner Network members, Microsoft BizSpark members, and Microsoft Imagine members.

### 4.1.C. describe subscription management using Management groups

The organizing structure for resources in Azure has four levels: management groups, subscriptions, resource groups, and resources.

![azure hierarchy-structure](https://docs.microsoft.com/en-gb/learn/wwl-azure/examine-azure-subscriptions/media/hierarchy.png)

Management group (https://docs.microsoft.com/en-us/azure/governance/management-groups/overview)

- Management groups: These are containers that help you manage access, policy, and compliance for multiple subscriptions. All subscriptions in a management group automatically inherit the conditions applied to the management group.

  - 10,000 management groups can be supported in a single directory.
  - A management group tree can support up to six levels of depth.
  - This limit doesn't include the Root level or the subscription level.
  - Each management group and subscription can only support one parent.
  - Each management group can have many children.

- Subscriptions: A subscription groups together user accounts and the resources that have been created by those user accounts. For each subscription, there are limits or quotas on the amount of resources you can create and use. Organizations can use subscriptions to manage costs and the resources that are created by users, teams, or projects.

- Resource groups: A resource group is a logical container into which Azure resources like web apps, databases, and storage accounts are deployed and managed.

- Resources: Resources are instances of services that you create, like virtual machines, storage, or SQL databases.

## 4.2. Describe planning and management of costs

https://docs.microsoft.com/en-us/azure/cost-management-billing/

### 4.2.A. describe options for purchasing Azure products and services

There are three main customer types on which the available purchasing options for Azure products and services is contingent, including:

- **Enterprise**. Enterprise customers sign an Enterprise Agreement with Azure that commits them to spending a negotiated amount on Azure services, which they typically pay annually. Enterprise customers also have access to customized Azure pricing.
- **Web direct**. Web direct customers pay public prices for Azure resources, and their monthly billing and payments occur through the Azure website.
- **Cloud Solution Provider**. Cloud Solution Provider (CSP) typically are Microsoft partner companies that a customer hires to build solutions on top of Azure. Payment and billing for Azure usage occurs through the customer's CSP.

> https://azure.microsoft.com/en-gb/pricing/purchase-options/

### 4.2.B. describe options around Azure Free account

An Azure free account provides subscribers with 12 months of our most popular services, a credit to explore any Azure service for 30 days, and over 25 services are free.

Do you pay anything to start with the Azure free account? No. Starting is free, plus you get a credit you can spend during the first 30 days.

What do you need to sign up for a free account? All you need is a phone number, a credit or debit card, and a GitHub account or Microsoft account username (formerly Windows Live ID).

What happens once you use my free credit or I’m at the end of 30 days? We’ll notify you so you can decide if you want to upgrade to pay-as-you-go pricing and remove the spending limit. If you do, you’ll have access to all the free products. If you don’t, your account and products will be disabled, and you'll need to upgrade to resume usage.

What happens at the end of the 12 months of free products? For 12 months after you upgrade your account, certain amounts of popular products for compute, networking, storage, and databases are free. After 12 months, any of these products you may be using will continue to run, and you’ll be billed at the standard pay-as-you-go rates.

### 4.2.C. describe the factors affecting costs such as resource types, services, locations, ingress and egress traffic

**Usage meters**
The meters track the resources' usage, and each meter generates a usage record that is used to calculate your bill.

- Resource type

  - Costs are resource-specific, so the usage that a meter tracks and the number of meters associated with a resource depend on the resource type.
  - Each meter tracks a specific type of usage. For example, a meter might track bandwidth usage (ingress or egress network traffic in bits-per-second), number of operations, size (storage capacity in bytes), or similar items.
  - The usage that a meter tracks correlates to a quantity of billable units.

- Services

  - Azure usage rates and billing periods can differ between Enterprise, Web Direct, and Cloud Solution Provider (CSP) customers.
  - Some subscription types also include usage allowances, which affect costs.
  - The Azure team develops and offers first-party products and services, while products and services from third-party vendors are available in the Azure Marketplace.
  - Different billing structures apply to each of these categories.

- Location

  - The Azure infrastructure is globally distributed, and usage costs might vary between locations that offer Azure products, services, and resources.

- Ingress and egress traffic
  - Inbound data transfers (i.e. data going into Azure data centers): Free
  - Outbound data transfers (i.e. data going out of Azure data centers; zones refer to source region): rates varies depending on zone
  - Outbound Data Transfers to Azure CDN from Microsoft are free of charge.
  - Reference: https://azure.microsoft.com/en-us/pricing/details/bandwidth/

#### What type data transfer is charged by Availability Zones data transfer meters?

Following Availability Zone data transfer is charged:

- Data transfer, ingress and egress, from a VNet resource deployed in an Availability Zone to another resource in different Availability Zone in the same VNET

Following Availability Zone data transfer is NOT charged:

- Data transfer between VNet resources located in same Availability Zone
- Data transfer between a VNet resource and a Public IP address in the same Azure Region
- Data transfer between VNet resources located in peered VNets across Availability Zones. This data transfer will be charges as per VNet peering rates.

#### Is data transfer between Azure services located within the same region charged?

No. For example, an Azure SQL database in the same region will not have any additional data transfer costs.

#### Is data transfer between Azure services located in two regions charged?

Yes. Outbound data transfer is charged at the normal rate and inbound data transfer is free.

### 4.2.D. describe Zones for billing purposes

A Zone is a geographical grouping of Azure Regions for billing purposes. the following Zones exist and include the sample regions as listed below:

- Zone 1 – West US, East US, Canada West, West Europe, France Central and others
- Zone 2 – Australia Central, Japan West, Central India, Korea South and others
- Zone 3 - Brazil South
- DE Zone 1 - Germany Central, Germany Northeast

The term **Zone** is for billing purposes only, and the full-term Availability Zone refers to the failure protection that Azure provides for datacenters.

### 4.2.E. describe the Pricing calculator (https://azure.microsoft.com/en-gb/pricing/calculator/)

- The Pricing Calculator is a tool that helps you estimate the cost of Azure products.
- It displays Azure products in categories, and you choose the Azure products you need and configure them according to your specific requirements.
- Azure then provides a detailed estimate of the costs associated with your selections and configurations.
- The Pricing Calculator provides estimates, not actual price quotes. Actual prices may vary depending upon the date of purchase, the payment currency you are using, and the type of Azure customer you are.

### 4.2.F. describe the Total Cost of Ownership (TCO) calculator (https://azure.microsoft.com/en-gb/pricing/tco/)

- Total Cost of Ownership Calculator is a tool that you use to estimate cost savings you can realize by migrating to Azure.
- TCO calculator generates a detailed report based on the details you enter and the adjustments you make.
- The report allows you to compare the costs of your on-premises infrastructure with the costs using Azure products and services to host your infrastructure in the cloud.

### 4.2.G. describe best practices for minimizing Azure costs such as performing cost analysis, creating spending limits and quotas, using tags to identify cost owners, using Azure reservations and using Azure Advisor recommendations

#### Perform cost analyses

- Plan your Azure solution wisely.
- Carefully consider the products, services, and resources you need, and read the relevant documentation to understand how each of your choices are metered and billed.
- Additionally, you should calculate your projected costs by using the Azure Pricing and Total Cost of Ownership (TCO) calculators, only adding the products, services, and resources you need.

#### Monitor usage with Azure Advisor

- Azure Advisor feature identifies unused or under-utilized resources, and you can implement its recommendations by removing unused resources and configuring your resources to match your actual demand.

#### Use spending limits

- Free trial customers and some credit-based Azure subscriptions can use the Spending Limits feature.
- If you have a credit-based subscription and you reach your configured spending limit, Azure suspends your subscription until a new billing period begins.
- The spending limit feature is not available for customers who aren't using credit-based subscriptions, such as Pay-As-You-Go subscribers.

> https://docs.microsoft.com/en-us/azure/billing/billing-spending-limit

#### Use Azure Reservations

- Azure Reservations offer discounted prices on certain Azure products and resources.
- You can pre-pay for one year or three years of use of Virtual Machines, SQL Database Compute Capacity, Azure Cosmos Database Throughput, and other Azure resources.
- You commit to reserved instances in one-year or three-year terms. Payment can be made in full for the entire commitment period, or the commitment can be billed monthly.
- Azure Reservations are only available to Enterprise or CSP customers and for Pay-As-You-Go subscriptions.

Example: If you have virtual machine workloads that are static and predictable, using reserved instances is a fantastic way to potentially save up to 70 to 80 percent off the pay-as-you-go cost.

#### Choose low-cost locations and regions

- The cost of Azure products, services, and resources can vary across locations and regions, and if possible, you should use them in those locations and regions where they cost less.

#### Research available cost-saving offers

- Keep up-to-date with the latest Azure customer and subscription offers, and switch to offers that provide the greatest cost-saving benefit.

#### Apply tags to identify cost owners

- Tags help you manage costs associated with the different groups of Azure products and resources.
- You can apply tags to groups of Azure products and resources to organize billing data.
- Tags make it easy to identify groups that generate the biggest Azure costs, so you can adjust your spending accordingly.

> Save on infrastructure costs https://docs.microsoft.com/en-us/learn/modules/predict-costs-and-optimize-spending/4-save-on-infrastructure-costs  
> Save on licensing costs https://docs.microsoft.com/en-us/learn/modules/predict-costs-and-optimize-spending/5-save-on-licensing-costs

### 4.2.H. describe Azure Cost Management (https://azure.microsoft.com/services/cost-management)

https://docs.microsoft.com/en-gb/azure/cost-management-billing/

Cost Management is an Azure product that provides a set of tools for monitoring, allocating, and optimizing your Azure costs.

The main features of the Azure Cost Management toolset include:

- **Reporting**. Generate reports using historical data to forecast future usage and expenditure.
- **Data enrichment**. Improve accountability by categorizing resources with tags that correspond to real-world business and organizational units.
- **Budgets**. Create and manage cost and usage budgets by monitoring resource demand trends, consumption rates, and cost patterns.
- **Alerting**. Get alerts based on your cost and usage budgets.
- **Recommendations**. Receive recommendations to eliminate idle resources and to optimize the Azure resources you provision.
- **Price**. Free to Azure customers.

## 4.3. Describe Azure Service Level Agreements (SLAs)

### 4.3.A. describe a Service Level Agreement (SLA) (https://azure.microsoft.com/en-gb/support/legal/sla/summary/)

- Service-Level Agreements (SLAs) capture the specific terms that define the performance standards that apply to Azure.
- SLAs describe Microsoft's commitment to providing Azure customers with certain performance standards.
- SLAs also specify what happens if a service or product fails to perform to a governing SLA's specification.
- There are SLAs for individual Azure products and services.
- A SLA defines performance targets for an Azure product or service. The performance targets that a SLA defines are specific to each Azure product and service.
- Azure does not provide SLAs for many services under the Free or Shared tiers. Also, free products such as Azure Advisor do not typically have a SLA.

#### Service Credits

- SLAs also describe how Microsoft will respond if an Azure product or service fails to perform to its governing SLA's specification.
- Customers may have a discount applied to their Azure bill, as compensation for an under-performing Azure product or service.

| Monthly uptime percentage | Service credit percentage |
| ------------------------- | ------------------------- |
| < 99.9                    | 10                        |
| < 99                      | 25                        |
| < 95                      | 100                       |

### 4.3.B. describe Composite SLAs

- When combining SLAs across different service offerings, the resultant SLA is a called a **Composite SLA**.
- The resulting composite SLA can provide higher or lower uptime values, depending on your application architecture.
- In general, the individual probability values for each service are independent.
- The combined probability of failure value is lower than the individual SLA values.

Example:

- Consider an App Service web app that writes to Azure SQL Database.
- App Service Web Apps is 99.95 percent; SQL Database is 99.99 percent.
- However, the composite SLA value for this application is: `99.95 percent × 99.99 percent = approx 99.94 percent`

### 4.3.C. describe how to determine an appropriate SLA for an application

https://docs.microsoft.com/en-gb/learn/modules/explore-azure-service-level-agreements/5-define-application-sla

#### Considerations for defining application SLAs

- If your application SLA defines four 9's (99.99%) performance targets, recovering from failures by manual intervention may not be enough to fulfill your SLA. Your Azure solution must be self-diagnosing and self-healing instead.
- It is difficult to respond to failures quickly enough to meet SLA performance targets above four 9's.
- Carefully consider the time window against which your application SLA performance targets are measured.
- The smaller the time window, the tighter the tolerances.
- If you define your application SLA as hourly or daily uptime, you need to understand these tighter tolerances might not allow for achievable performance targets.
- Performance targets about 99.99% are going to be very difficult to achieve.

## 4.4. Describe service lifecycle in Azure

### 4.4.A. describe Public and Private Preview features

- Preview feature: An Azure feature is available to _certain_ Azure customers for evaluation purposes.
- Public preview: An Azure feature is available to _all_ Azure customers for evaluation purposes.

Azure Previews

- Users can test pre-release features, products, services, software, and even regions.
- Providing feedback on the preview features helps Microsoft improve the Azure service.
- You may choose to use an Azure preview service in production. Remember, the preview feature or functionality may not yet be ready for production deployments. Make sure you're aware of any limitations around its use before deploying to production.

> https://preview.portal.azure.com/  
> or any service name which has (Preview)

### 4.4.B. describe the term General Availability (GA)

- A feature released to all Azure customers typically goes to General Availability or GA.
- It's common for features to move from Azure preview features to GA, based on customer evaluation and feedback.

> https://azure.microsoft.com/en-gb/blog/topics/announcements/

### 4.4.C. describe how to monitor feature updates and product changes

Azure updates page (https://azure.microsoft.com/updates) has information about the latest updates to Azure products, services, and features, as well as product roadmaps and announcements.

- View details about all Azure updates.
- See which updates are in general availability, Preview, or Development.
- Browse updates by product category or update type, by using the provided dropdown lists.
- Search for updates by keyword by entering search terms into a text-entry field.
- Subscribe to get Azure update notifications by RSS.
- Access the Microsoft Connect page to read Azure product news and announcements.
