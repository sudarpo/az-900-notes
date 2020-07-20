# 2. Describe Core Azure Services (30-35%)

> https://docs.microsoft.com/en-gb/learn/modules/define-core-azure-services-products/  
> https://docs.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree

## 2.1. Describe the core Azure architectural components

### describe Regions

A region is a set of datacenters deployed within a latency-defined perimeter and connected through a dedicated regional low-latency network.

- Regions provide customers the flexibility and scale needed to bring applications closer to their users.
- Regions preserve data residency and offer comprehensive compliance and resiliency options for customers.

A geography is a discrete market, typically containing two or more regions, that preserves data residency and compliance boundaries.

**Special Azure regions**

- US DoD Central, US Gov Virginia, US Gov Iowa and more
- China East, China North and more: unique partnership between Microsoft and 21Vianet

#### Region Pairs

- Each Azure region is paired with another region within the same geography (such as US, Europe, or Asia) at least 300 miles away, which together make a region pair.
- **Physical isolation**. When possible, Azure prefers at least 300 miles of separation between datacenters in a regional pair, although this isn't practical or possible in all geographies.
- **Platform-provided replication**. Some services such as Geo-Redundant Storage provide automatic replication to the paired region.
- **Region recovery order**. In the event of a broad outage, recovery of one region is prioritized out of every pair. Applications that are deployed across paired regions are guaranteed to have one of the regions recovered with priority.
- **Sequential updates**. Planned Azure system updates are rolled out to paired regions sequentially (not at the same time) to minimize downtime, the effect of bugs, and logical failures in the rare event of a bad update.

Additional advantages of region pairs include:

- If there's an extensive Azure outage, one region out of every pair is prioritized to make sure at least one is restored as quick as possible for applications hosted in that region pair.
- Planned Azure updates are rolled out to paired regions one region at a time to minimize downtime and risk of application outage.
- Data continues to reside within the same geography as its pair (except for Brazil South) for tax and law enforcement jurisdiction purposes.

> https://docs.microsoft.com/en-us/learn/modules/discuss-core-azure-architectural-components/3-explore-region-pairs  
> https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions#what-are-paired-regions?azure-portal=true

### describe Availability Zones

![availability-options](https://docs.microsoft.com/en-us/learn/wwl-azure/discuss-core-azure-architectural-components/media/availability-options.png)

**Availability Zones** are physically separate locations within an Azure region.  
Each Availability Zone is made up of one or more datacenters equipped with independent power, cooling, and networking.

Availability Zone features

- Each availability zone is an isolation boundary containing one or more datacenters equipped with independent power, cooling, and networking.
- If one availability zone goes down, the other continues working.
- The availability zones are typically connected to each other through very fast, private fiber-optic networks.
- Availability zones allow customers to run mission-critical applications with high availability and low-latency replication.
- Availability zones are offered as a service within Azure, and to ensure resiliency, there’s a minimum of three separate zones in all enabled regions.

**Availability sets** are a way for you to ensure your application remains online if a high-impact maintenance event is required, or if a hardware failure occurs.

- Availability sets are made up of Update domains (UD) and Fault domains (FD).
- Update domains. When a maintenance event occurs (such as a performance update or critical security patch applied to the host), the update is sequenced through update domains.
  _Update domains_ are a logical section of the datacenter, and they are implemented with software and logic.
- Fault domains. Fault domains provide for the physical separation of your workload across different hardware in the datacenter. This includes power, cooling, and network hardware that supports the physical servers located in server racks. In the event the hardware that supports a server rack becomes unavailable, only that rack of servers would be affected by the outage.

### describe Resource Groups

- A resource group is a unit of management for your resources in Azure.
- A container that allows you to aggregate and manage all the resources required for your application in a single manageable unit.
- Allows you to manage the application collectively over its lifecycle.

Manage and apply the following resources at resource group level:

- Metering and billing
- Policies
- Monitoring and alerts
- Quotas
- Access control

### describe Azure Resource Manager

> https://docs.microsoft.com/en-us/learn/modules/discuss-core-azure-architectural-components/9-explore-azure-resource-manager  
> https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/overview

- Azure Resource Manager is a management layer in which resource groups and all the resources within it are created, configured, managed, and deleted.
- It provides a consistent management layer which allows you automate the deployment and configuration of resources using different automation and scripting tools, such as Microsoft Azure PowerShell, Azure Command-Line Interface (Azure CLI), Azure portal, REST API, and client SDKs.

With Azure Resource Manager, you can:

- **Deploy Application resources**. Update, manage, and delete all the resources for your solution in a single, coordinated operation.
- **Organize resources**. Manage your infrastructure through declarative templates rather than scripts. You can view which resources are linked by a dependency, and you can apply tags to resources to categorize them for management tasks, such as billing.
- **Control access and resources**. You can control who in your organization can perform actions on the resources. You manage permissions by defining roles, adding users or groups to the roles, and applying policies at resource group level. Examples of elements you may wish to control are: enforcing naming convention on resources, limiting which types and instances of resources can be deployed, or limiting which regions can host a type of resource.

#### The benefits of using Resource Manager

- Manage your infrastructure through declarative templates rather than scripts.
- Deploy, manage, and monitor all the resources for your solution as a group, rather than handling these resources individually.
- Redeploy your solution throughout the development lifecycle and have confidence your resources are deployed in a consistent state.
- Define the dependencies between resources so they're deployed in the correct order.
- Apply access control to all services because Role-Based Access Control (RBAC) is natively integrated into the management platform.
- Apply tags to resources to logically organize all the resources in your subscription.
- Clarify your organization's billing by viewing costs for a group of resources sharing the same tag.

### describe the benefits and usage of core Azure architectural components

## 2.2. Describe some of the core products available in Azure

### describe products available for Compute such as Virtual Machines, Virtual Machine Scale Sets, App Services, Azure Container Instances (ACI) and Azure Kubernetes Service (AKS)

**Azure Compute Services**

- Azure virtual machines: create and use virtual machines in the cloud.  
  _Similar to EC2 Instances (AWS)_
- Virtual machine scale sets: Azure compute resource that you can use to deploy and manage a set of identical VMs.  
  _Similar to Auto Scaling (in AWS)_
- App services: quickly build, deploy, and scale enterprise-grade web, mobile, and API apps running on any platform. A fully managed platform for building, deploying and scaling your web apps.  
  _Similar to Elastic Beanstalk and LightSail (in AWS)_
- Functions: are ideal when you're concerned only about the code running your service and not the underlying platform or infrastructure.  
  _Similar to AWS Lambda_
- Azure Container Instances (ACI).
  - Azure Container Instances offers the fastest and simplest way to run a container in Azure without having to manage any virtual machines or adopt any additional services.
  - It is a PaaS offering that allows you to upload your containers, which it will run for you.
  - _Similar to Elastic Container Service ECS, and Fargate (in AWS)_
- Azure Kubernetes Service (AKS). Azure Kubernetes Service (AKS) is a complete orchestration service for containers with distributed architectures and large volumes of containers. Orchestration is the task of automating and managing a large number of containers and how they interact.  
  _Similar to Elastic Kubernetes Service ECS (in AWS)_

### describe products available for Networking such as Virtual Network, Load Balancer, VPN Gateway, Application Gateway and Content Delivery Network

**Azure network services**

- Azure Virtual Network

  - Azure Virtual Network enables many types of Azure resources such as Azure VMs to securely communicate with each other, the internet, and on-premises networks.
  - A virtual network is scoped to a single region; however, multiple virtual networks from different regions can be connected using virtual network peering.
  - With Azure Virtual Network you can provide isolation, segmentation, communication with on-premises and cloud resources, routing and filtering of network traffic.
  - _Virtual Private Cloud (in AWS)_

- VPN gateway

  - Connects Azure virtual networks to other Azure virtual networks, or customer on-premises networks (Site To Site). Allows end users to connect to Azure services through VPN tunneling (Point To Site).

- Azure Application Gateway

  - Application Gateway is a layer 7 load balancer. It supports SSL termination, cookie-based session affinity, and round robin for load-balancing traffic.

  - _Application Load Balancer in AWS_

- Azure Load Balancer

  - Azure Load Balancer can provide scale for your applications and create high availability for your services.
  - Azure Load Balancer load-balances traffic at layer 4 (TCP or UDP).
  - Load Balancer supports inbound and outbound scenarios, provides low latency and high throughput, and scales up to millions of flows for all Transmission Control Protocol (TCP) and User Datagram Protocol (UDP) applications.
  - _Network Load Balancer (in AWS)_

- Content Delivery Network: A global content delivery network that delivers audio, video, applications, images, and other files.
  - It is a way to get content to users in their local region to minimize latency.
  - _CloudFront (AWS)_

### describe products available for Storage such as Blob Storage, Disk Storage, File Storage, and Archive Storage

> https://docs.microsoft.com/en-us/learn/modules/define-core-azure-services-products/9-define-azure-data-categories

**Azure Storage**

- Blob Storage

  - Azure Blob storage is Microsoft's object storage solution for the cloud. Blob storage is optimized for storing massive amounts of unstructured data, such as text or binary data.

  - [Azure storage offers different access tiers](https://docs.microsoft.com/en-gb/azure/storage/blobs/storage-blob-storage-tiers?tabs=azure-portal), which allow you to store blob object data in the most cost-effective manner. The available access tiers include:

    - Hot - Optimized for storing data that is accessed frequently.
    - Cool - Optimized for storing data that is infrequently accessed and stored for at least 30 days.
    - Archive - Optimized for storing data that is rarely accessed and stored for at least 180 days with flexible latency requirements (on the order of hours). (**Archive Storage**)

  - [Blob storage](https://docs.microsoft.com/en-gb/azure/storage/blobs/storage-blobs-introduction) offers three types of resources:

    - The storage account
      A storage account provides a unique namespace in Azure for your data. Every object that you store in Azure Storage has an address that includes your unique account name. The combination of the account name and the Azure Storage blob endpoint forms the base address for the objects in your storage account.

    - A container in the storage account
      A container organizes a set of blobs, similar to a directory in a file system. A storage account can include an unlimited number of containers, and a container can store an unlimited number of blobs.

    - A blob in a container
      Azure Storage supports three types of blobs:

      - Block blobs store text and binary data. Block blobs are made up of blocks of data that can be managed individually. Block blobs store up to about 4.75 TiB of data. Larger block blobs are available in preview, up to about 190.7 TiB
      - Append blobs are made up of blocks like block blobs, but are optimized for append operations. Append blobs are ideal for scenarios such as logging data from virtual machines.
      - Page blobs store random access files up to 8 TB in size. Page blobs store virtual hard drive (VHD) files and serve as disks for Azure virtual machines. For more information about page blobs, see Overview of Azure page blobs

- Disk Storage / [Azure Managed Disks](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/managed-disks-overview)

  - Disk storage provides disks for virtual machines, applications, and other services to access and use as they need, similar to how they would in on-premises scenarios.
  - Disk storage allows data to be persistently stored and accessed from an attached virtual hard disk.
  - [Disk types](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/disks-types):

| Detail         | Ultra disk                                                                                                                       | Premium SSD                                    | Standard SSD                                                   | Standard HDD                            |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- | -------------------------------------------------------------- | --------------------------------------- |
| Disk type      | SSD                                                                                                                              | SSD                                            | SSD                                                            | HDD                                     |
| Scenario       | IO-intensive workloads such as [SAP HANA], top tier databases (for example, SQL, Oracle), and other transaction-heavy workloads. | Production and performance sensitive workloads | Web servers, lightly used enterprise applications and dev/test | Backup, non-critical, infrequent access |
| Max disk size  | 65,536 gibibyte (GiB)                                                                                                            | 32,767 GiB                                     | 32,767 GiB                                                     | 32,767 GiB                              |
| Max throughput | 2,000 MB/s                                                                                                                       | 900 MB/s                                       | 750 MB/s                                                       | 500 MB/s                                |
| Max IOPS       | 160,000                                                                                                                          | 20,000                                         | 6,000                                                          | 2,000                                   |

- File Storage

  - Azure Files enables you to set up highly available network file shares that can be accessed by using the standard Server Message Block (SMB) protocol.
  - You can also read the files using the REST interface or the storage client libraries.

- Azure Queue service is used to store and retrieve messages. Queue messages can be up to 64 KB in size, and a queue can contain millions of messages. Queues are generally used to store lists of messages to be processed asynchronously.

- Azure Table storage stores large amounts of structured data.
  - The service is a NoSQL datastore which accepts authenticated calls from inside and outside the Azure cloud.
  - Azure Tables are ideal for storing structured, non-relational data.
  - You can use Table storage to store and query huge sets of structured, non-relational data, and your tables will scale as demand increases.

#### IF YOU WANT TO... USE THIS

- Get scalable and secure storage for your virtual machines: **Disk storage**
- Find massively scalable, secure storage for your unstructured data: **Blob storage**
- Get low-cost storage for rarely accessed data: **Archive Storage**
- Get secure cloud file shares: **File Storage**
- Get secure storage for message-based communication between apps: **Queue Storage**
- Appliances and solutions for data transfer to Azure and edge compute: **Data Box**
- Create powerful file shares for enterprise workloads, including open-source/Linux: **Azure NetApp Files**
- File caching for high-performance computing (HPC): **Azure HPC Cache**

### describe products available for Databases such as Cosmos DB, Azure SQL Database, Azure Database for MySQL, Azure Database for PostgreSQL, Azure Database Migration service

- Cosmos DB

  - Azure Cosmos DB is a fully managed NoSQL database service for modern app development with guaranteed single-digit millisecond response times and 99.999-per cent availability, backed by SLAs, automatic and instant scalability, and open-source APIs for MongoDB and Cassandra.
  - It supports schema-less data that lets you build highly responsive and Always On applications to support constantly changing data.

- Azure SQL Database

  - Azure SQL Database is a relational database as a service (DaaS) based on the latest stable version of Microsoft SQL Server database engine.
  - Options:
    - Single database (Hyperscale storage (up to 100TB), serverless compute, easy management);
    - Elastic pool (resource sharing for cost optimization, simplified performance management);
    - Database server (access management, backup management, business continuity management)

- Azure SQL Managed Instance

  - The broadest SQL Server compatibility on a fully managed service streamlines app modernisation with minimal code changes.
  - Lift and shift ready.
  - Native virtual network support
  - Fully managed service

- Azure SQL Server on Azure Virtual Machines

  - Best for migrations and applications requiring OS-level access.
  - Lift and shift ready.
  - Expansive SQL Server and OS version support
  - Automated manageability features for SQL Server

- Azure Database for MySQL

  - Fully managed database that supports the latest MySQL community editions.
  - Azure Database for MySQL is easy to set up, manage and scale.
  - It automates the management and maintenance of your infrastructure and database server, including routine updates, backups and security.
  - Deliver high availability and elastic scaling to open-source mobile and web apps with a managed community MySQL database service, or migrate MySQL workloads to the cloud.

- Azure Database for PostgreSQL

  - Build scalable, secure and fully managed enterprise-ready apps on open-source PostgreSQL, scale out single-node PostgreSQL with high performance or migrate PostgreSQL and Oracle workloads to the cloud.

- Azure Database for MariaDB

  - Deliver high availability and elastic scaling to open-source mobile and web apps with a managed community MariaDB database service

- [Azure Database Migration service](https://docs.microsoft.com/en-us/azure/dms/resource-scenario-status)

  - The Azure Database Migration Service is a fully managed service designed to enable seamless migrations from multiple database sources to Azure data platforms with minimal downtime (online migrations).
  - The service uses the Microsoft Data Migration Assistant to generate assessment reports that provide recommendations to help guide you through required changes prior to performing a migration.
  - [Supported sources](https://docs.microsoft.com/en-us/azure/dms/resource-scenario-status), e.g. SQL Server, RDS SQL, MongoDB, MySQL, RDS MySQL, PostgreSQL, RDS PostgreSQL, Oracle.

- Azure Cache for Redis: An in-memory–based, distributed caching service that provides a high-performance store typically used to offload nontransactional work from a database.

> More on Azure databases: https://azure.microsoft.com/en-gb/product-categories/databases/

### describe the Azure Marketplace and its usage scenarios

Azure Marketplace is a service on Azure that helps connect end users with Microsoft partners, independent software vendors (ISVs), and start-ups that are offering their solutions and services, which are optimized to run on Azure.

Azure Marketplace allows customers—mostly IT professionals and cloud developers—to find, try, purchase, and provision applications and services from hundreds of leading service providers, all certified to run on Azure.

Using Azure Marketplace, you can provision end-to-end solutions quickly and reliably, hosted in your own Azure environment. At the time of writing, this includes over 8,000 listings.

## 2.3. Describe some of the solutions available on Azure

### describe Internet of Things (IoT) and products that are available for IoT on Azure such as IoT Hub and IoT Central

### describe Big Data and Analytics and products that are available for Big Data and Analytics such as Azure Synapse Analytics, HDInsight, and Azure Databricks

### describe Artificial Intelligence (AI) and products that are available for AI such as Azure Machine Learning Service and Studio

### describe Serverless computing and Azure products that are available for serverless computing such as Azure Functions, Logic Apps, and Event Grid

### describe DevOps solutions available on Azure such as Azure DevOps and Azure DevTest Labs

### describe the benefits and outcomes of using Azure solutions

## 2.4. Describe Azure management tools

### describe Azure tools such as Azure Portal, Azure PowerShell, Azure CLI and Cloud Shell

### describe Azure Advisor
