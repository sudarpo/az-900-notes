# 1. Describe Cloud Concepts (15-20%)

## 1.1. Describe the benefits and considerations of using cloud services

### 1.1.A. describe terms such as High Availability, Scalability, Elasticity, Agility, Fault Tolerance, and Disaster Recovery

**High availability**. The ability to keep services up and running for long periods of time, with very little downtime, depending on the service in question.

**Scalability**. The ability to increase or decrease resources for any given workload. You can add additional resources to service a workload (known as scaling out), or add additional capabilities to manage an increase in demand to the existing resource (known as scaling up). Scalability doesn't have to be done automatically

**Elasticity**. The ability to automatically or dynamically increase or decrease resources as needed. Elastic resources match the current needs, and resources are added or removed automatically to meet future needs when it’s needed, and from the most advantageous geographic location. A distinction between scalability and elasticity is that elasticity is done automatically

**Agility**. The ability to react quickly. Cloud services can allocate and deallocate resources quickly. They are provided on-demand via self-service, so vast amounts of computing resources can be provisioned in minutes. There is no manual intervention in provisioning or deprovisioning services.

**Fault tolerance**. The ability to remain up and running even in the event of a component or service no longer functioning. Typically, redundancy is built into cloud services architecture so if one component fails, a backup component takes its place. The type of service is said to be tolerant of faults.

**Disaster recovery**. The ability to recover from an event which has taken down a cloud service. Cloud services disaster recovery can happen very quickly with automation and services being readily available to use.

**Global reach**. The ability reach audiences around the globe. Cloud services can have presence in various regions across the globe which you can access, giving you a presence in those regions even though you may not have any infrastructure in that region.

**Customer latency capabilities**. If customers are experiencing slowness with a particular cloud service, they are said to be experiencing some latency. Even though modern fiber optics are fast, it can still take time for services to react to customer actions if the service is not local to the customer. Cloud services have the ability deploy resources in datacenters around the globe, thus addressing customer latency issues.

**Predictive cost considerations.** The ability for users to predict what costs they will incur for a particular cloud service. Costs for individual services are made available, and tools are provided to allow you predict what costs a service will incur. You can also perform analysis based on future growth.

**Technical skill requirements and considerations**. Cloud services can provide and manage hardware and software for workloads. Therefore, getting a workload up and running with cloud services demands less technical resources than having IT teams build and maintain physical infrastructure for handling the same workload. A user can be expert in the application they want to run without having to need skills to build and maintain the underlying hardware and software infrastructure.

**Increased productivity**. On-site datacenters typically require a lot of hardware setup (otherwise known as racking and stacking), software patching, and other time-consuming IT management chores. Cloud computing eliminates the need for many of these tasks, so IT teams can spend time on achieving more important business goals.

**Security**. Cloud providers offer a broad set of policies, technologies, controls, and expert technology skills that can provide better security than most organizations can otherwise achieve. The result is strengthened security, which helps to protect data, apps, and infrastructure from potential threats.

### 1.1.B. describe the principles of economies of scale

The concept of economies of scale is the ability to reduce costs and gain efficiency when operating at a larger scale in comparison to operating at a smaller scale.

Cloud providers are large businesses, and are able to leverage the benefits of economies of scale, and then pass those benefits on to their customers.

This is apparent to end users in a number of ways, one of which is the ability to acquire hardware at a lower cost than if a single user or smaller business were purchasing it.

### 1.1.C. describe the differences between Capital Expenditure (CapEx) and Operational Expenditure (OpEx)

**Capital Expenditure (CapEx)**: This is the up front spending of money on physical infrastructure, and then deducting that up front expense over time. The up front cost from CapEx has a value that reduces over time.

- Server costs
- Storage costs
- Network costs
- Backup and archive costs
- Organization continuity and disaster recovery costs
- Datacenter infrastructure costs
- Technical personnel

Benefits of CapEx  
With capital expenditures, you plan your expenses at the start of a project or budget period. Your costs are fixed, meaning you know exactly how much is being spent. This is appealing when you need to predict the expenses before a project starts due to a limited budget.

**Operational Expenditure (OpEx)**: This is spending money on services or products now and being billed for them now. You can deduct this expense in the same year you spend it. There is no up front cost, as you pay for a service or product as you use it.

- Leasing software and customized features
- Scaling charges based on usage/demand instead of fixed hardware or capacity
- Billing at the user or organization level

Benefits of OpEx  
Demand and growth can be unpredictable and can outpace expectation, which is a challenge for the CapEx model as shown in the following graph.

### 1.1.D. describe the consumption-based model

- only pay for the resources that they use

has many benefits, including:

- No upfront costs.
- No need to purchase and manage costly infrastructure that they may or may not use to its fullest.
- The ability to pay for additional resources when they are needed.
- The ability to stop paying for resources that are no longer needed.

## 1.2. Describe the differences between Infrastructure-as-a-Service (IaaS), Platform-as-a-Service (PaaS) and Software-as-a-Service (SaaS)

**IaaS** requires the most user management of all the cloud services. The user is responsible for managing the operating systems, data, and applications.
**PaaS** requires less user management. The cloud provider manages the operating systems, and the user is responsible for the applications and data they run and store.
**SaaS** requires the least amount of management. The cloud provider is responsible for managing everything, and the end user just uses the software.

![Cloud](https://docs.microsoft.com/en-us/learn/wwl-azure/explore-types-cloud-services/media/shared-responsibility.png)

### 1.2.A. describe Infrastructure-as-a-Service (IaaS),

- Rent IT infrastructure servers and virtual machines (VMs), storage, networks, and operating systems

IaaS characteristics

- Upfront costs. IaaS has no upfront costs. Users pay only for what they consume.
- User ownership. The user is responsible for the purchase, installation, configuration, and management of their own software operating systems, middleware, and applications.
- Cloud provider ownership. The cloud provider is responsible for ensuring that the underlying cloud infrastructure (such as virtual machines, storage and networking) is available for the user.

### 1.2.B. describe Platform-as-a-Service (PaaS)

PaaS characteristics

- Upfront costs. There are no upfront costs, and users pay only for what they consume.
- User ownership. The user is responsible for the development of their own applications. However, they are not responsible for managing the server or infrastructure. This allows the user to focus on the application or workload they want to run.
- Cloud provider ownership. The cloud provider is responsible for operating system management, and network and service configuration. Cloud providers are typically responsible for everything apart from the application that a user wants to run. They provide a complete managed platform on which to run an application.

### 1.2.C. describe Software-as-a-Service (SaaS)

SaaS characteristics

- Upfront costs. Users have no upfront costs; they pay a subscription, typically on a monthly or annual basis.
- User ownership. Users just use the application software; they are not responsible for any maintenance or management of that software.
- Cloud provider ownership. The cloud provider is responsible for the provision, management, and maintenance of the application software.

### 1.2.D. compare and contrast the three different service types

#### IaaS

IaaS is the most flexible category of cloud services. It aims to give you complete control over the hardware that runs your application. Instead of buying hardware, with IaaS, you rent it.

Advantages:

- No CapEx. Users have no upfront costs.
- Agility. Applications can be made accessible quickly, and deprovisioned whenever needed.
- Consumption-based model. Organizations pay only for what they use and operate under an OpEx model.
- Skills. No deep technical skills are required to deploy, use, and gain the benefits of a public cloud. Organizations can leverage the skills and expertise of the cloud provider to ensure workloads are secure, safe, and highly available.
- Cloud benefits. Organizations can leverage the skills and expertise of the cloud provider to ensure workloads are made secure and highly available.
- Flexibility: IaaS is the most flexible cloud service as you have control to configure and manage the hardware running your application.

Disadvantages:

- Management. The shared responsibility model applies; the user manages and maintains the services they have provisioned, and the cloud provider manages and maintains the cloud infrastructure.

#### PaaS

PaaS provides the same benefits and considerations as IaaS, but there some additional benefits.

Advantages:

- No CapEx. Users have no upfront costs.
- Agility. PaaS is more agile than IaaS, and users do not need to configure servers for running applications.
- Consumption-based model. Users pay only for what they use, and operate on an OpEx model.
- Skills. No deep technical skills are required to deploy, use, and gain the benefits of PaaS.
- Cloud benefits. Users can leverage the skills and expertise of the cloud provider to ensure their workloads are made secure and highly available. In addition, users can gain access to more cutting-edge development tools and toolsets. They then can apply these tools and toolsets across an application's lifecycle.
- Productivity. Users can focus on application development only, as all platform management is handled by the cloud provider. Working with distributed teams as services is easier, as the platform is accessed over the internet and can be made globally available more easily.

Disadvantages:

- Platform limitations. There may be some limitations to a cloud platform that could affect how an application runs. Any limitations should be taken into consideration when considering which PaaS platform is best suited for a workload.

#### SaaS

SaaS is software that is centrally hosted and managed for the end customer. It is usually based on an architecture where one version of the application is used for all customers, and licensed through a monthly or annual subscription

SaaS provides the same benefits as IaaS, but again there some additional benefits.

Advantages:

- No CapEx. Users don’t have any upfront costs.
- Agility. Users can provide staff with access to the latest software quickly and easily.
- Pay-as-you-go pricing model: Users pay for the software they use on a subscription model, typically monthly or yearly, regardless of how much they use the software.
- Flexibility. Users can access the same application data from anywhere.

Disadvantages

- Software limitations. There may be some limitations to a software application that might affect how users work. Any limitations should be taken into consideration when considering which PaaS platform is best suited for a workload.

## 1.3. Describe the differences between Public, Private and Hybrid cloud models

### 1.3.A. describe Public cloud

A public cloud is owned by the cloud services provider (also known as a hosting provider). It provides resources and services to multiple organizations and users, who connect to the cloud service via a secure network connection, typically over the internet.

Public cloud models have the following characteristics:

- Ownership - Ownership refers to the resources that an organization or end user uses. Examples include storage and processing power. Resources do not belong to the organization that is utilizing them, but rather they are owned and operated by a third party, such as the cloud service provider.
- Multiple end users - Public cloud modes may make their resources available to multiple organizations.
- Public access - Public access allows the public to access the desired cloud services.
- Availability - Availability is the most common cloud-type deployment model.
- Connectivity - Users and organizations are typically connected to the public cloud over the internet using a web browser.
- Skills - Public clouds do not require deep technical knowledge to set up and use its resources.

### 1.3.B. describe Private cloud

A private cloud is owned and operated by the organization that uses the resources from that cloud. They create a cloud environment in their own datacenter and provide self-service access to compute resources to users within their organization. The organization remains the owner, entirely responsible for the operation of the services they provide.

Private cloud models have the following characteristics:

- Ownership. The owner and user of the cloud services are the same.
- Hardware. The owner is entirely responsible for the purchase, maintenance, and management of the cloud hardware.
- Users. A private cloud operates only within one organization and cloud computing resources are used exclusively by a single business or organization.
- Connectivity. A connection to a private cloud is typically made over a private network that is highly secure.
- Public access. Does not provide access to the public.
- Skills. Requires deep technical knowledge to set up, manage, and maintain.

### 1.3.C. describe Hybrid cloud

A hybrid cloud combines both public and private clouds, allowing you to run your applications in the most appropriate location.

Hybrid cloud models have the following characteristics:

- Resource location. Specific resources run or are used in a public cloud, and others run or are used in a private cloud.
- Cost and efficiency. Hybrid cloud models allow an organization to leverage some of the benefits of cost, efficiency, and scale that are available with a public cloud model.
- Control. Organizations retain management control in private clouds.
- Skills. Technical skills are still required to maintain the private cloud and ensure both cloud models can operate together.

### 1.3.D. compare and contrast the [three different cloud models](https://docs.microsoft.com/en-us/learn/modules/distinguish-types-cloud-models/5-compare-cloud-models)

#### Public Cloud

Advantages:

- No CapEx. You don’t have to buy a new server in order to scale.
- Agility. Applications can be made accessible quickly, and deprovisioned whenever needed.
  Consumption-based model. Organizations pay only for what they use, and operate under an OpEx model.
- Maintenance. Organizations have no responsibility for hardware maintenance or updates.
- Skills. No deep technical skills are required to deploy, use, and gain the benefits of a public cloud. Organizations can leverage the skills and expertise of the cloud provider to ensure workloads are secure, safe, and highly available.

Disadvantages:

- Security. There may be specific security requirements that cannot be met by using public cloud.
- Compliance. There may be government policies, industry standards, or legal requirements which public clouds cannot meet.
- Ownership. Organizations don't own the hardware or services and cannot manage them as they may wish.
- Specific scenarios. If organizations have a unique business requirement, such as having to maintain a legacy application, it may be hard to meet that requirement with public cloud services.

#### Private Cloud

Advantages:

- Control. Organizations have complete control over the resources.
- Security. Organizations have complete control over security.
- Compliance. If organizations have very strict security, compliance, or legal requirements, a private cloud may be the only viable option.
- Specific scenarios. If an organization has a specific scenario not easily supported by a public cloud provider (such as having to maintain a legacy application), it may be preferable to run the application locally.

Disadvantages:

- Upfront CapEx. Hardware must be purchased for start-up and maintenance.
- Agility. Private clouds are not as agile as public clouds, because you need to purchase and set up all the underlying infrastructure before they can be leveraged.
- Maintenance. Organizations have the responsibility for hardware maintenance and updates.
- Skills. Private clouds require in-house IT skills and expertise that may be hard to get or be costly.

#### Hybrid cloud

Advantages:

- Flexibility. The most flexible scenario: with a hybrid cloud setup, an organization can decide to run their applications either in a private cloud or in a public cloud.
- Costs. Organizations can take advantage of economies of scale from public cloud providers for services and resources as they wish. This allows them to access cheaper storage than they can provide themselves.
- Control. Organizations can still access resources over which they have total control.
- Security. Organizations can still access resources for which they are responsible for security.
- Compliance. Organizations maintain the ability to comply with strict security, compliance, or legal requirements as needed.
- Specific scenarios. Organizations maintain the ability to support specific scenarios not easily supported by a public cloud provider, such as running legacy applications. In this case, they can keep the old system running locally, and connect it to the public cloud for authorization or storage. Additionally, they could host a website in the public cloud, and link it to a highly secure database hosted in their private cloud.

Disadvantages:

- Upfront CapEx. Upfront CapEx is still required before organizations can leverage a private cloud.
- Costs. Purchasing and maintaining a private cloud to use alongside the public cloud can be more expensive than selecting a single deployment model.
- Skills. Deep technical skills are still required to be able to set up a private cloud.
- Ease of management. Organizations need to ensure there are clear guidelines to avoid confusion, complications or misuse.
