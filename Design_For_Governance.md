# Designing a governance solution using Microsoft Azure

## Learning objectives

We will learn following topics here:

* Grasp the principles and importance of design governance to ensire consistency and alignment with organizational objectives
* Apply effective design principles to organize and manage Auzre resources within management groups and subscriptions for optimal efficiency and control
* Evaliuate landing zones to establish a secure and well-architected foundation for Azure workloads
* Apply resource group design strategies to efficiently organize and manage Azure resources for streamlined administration and maintenance
* Asses and recommend a tagging strategy to categorize and organize Auzre resources, facilitating effective resource management and cost tracking
* Evaliuate and propose a soliution for implementing Azure policy to enforce compliance and governance standards within an Azure environment
* Apply RBAC (Role-Based Access Control) design principle to ensure secure access management and permissions for Azure resources

As a cloud architect, you are supposed to design a solution for develoipers that would grant them the ability to provision specific Azure resources as determined by the company. This will help enforce corporate standards and analize compliance at scale as an Azure architect.

To achieve all of the above, along with some additional features you will learn a few concepts here.

## Design governance

Governance in Azure is an aspect of Azure management.

* Azure management
  * It refers to the tasks and processes required to maintain business applications and the resources that support them.
  * Azure has many services and tools that work together to provide complete management.
  * The first step in designing a complete management environment is to acknowledge different tools and how they work together.

Following are the different areas of management required to maintain any application or resource:

* Protect
* Monitor
* Configure
* Govern
* Secure
* Migrate

Montor: It is the act of collecting and analyzing data to audit the performance, health and availability of resources.

Configure: It refers to the initial deployment and configuration of resources and ongoing maintenance.

Govern: It provides mechanism and processes to maintain control over applications and resources in Azure.

Secure: It manages the security of resources and data. It involves assessing threats, collecting an analyzing data, and ensuring the compliance of applications and resources.

Protect: It refers to keeping the applications and data available, even with outages that are beyond control.

Migrate: It refers to tranisioning workloads currently running on-premises to the Azure Cloud.

### Governance strategies

Governanvce strategies provides mechanisms and processes to maintain control over the applications and resources in Azure. It involves determinning the requirements, planning initiatives, and setting strategic priorities.

There two import governance tools:

* Azure policies
* Resource tags

Azure provides a hierarchical structure to apply governance strategies as shown below:


![Azure governance scope levels](https://github.com/sunnyadeshara86/microsoft-azure/blob/master/Images/scope-levels.png)

The tenant root group contains all the management groups and subscriptions.

As shown in the above image, Azure hierarchy has four levels:

* Management groups: It helps to manage acess, policy and compliance for multiple subscriptions
* Subscriptions: They are logical containers that serve as units of management and scale.
* Resource groups: These are logical containers into which Azure resources are deployed and managed.
* Resources: They are instances of services that users create.

### Management groups and subscriptions

#### Management groups

Management groups provide an efficient way to manage access, policies, and compliance across an enterprise. They provide access through a hierarchy of management groups and subscriptions. They are containers in which subscriptions can be organized.

* They provide a level of scope above subscriptions
* They are organizationally aligned through custom hierarchies and grouping.
* They provide enterprise-level management on a wide scale regardless of the subscription type.

The following diagram shows an example of creating a hierarchy for governance using management groups:

![Azure management groups organization](https://github.com/sunnyadeshara86/microsoft-azure/blob/master/Images/mg-org.png)

Source: https://learn.microsoft.com/en-us/azure/governance/management-groups/overview

#### Azure subscriptions and accounts

An Azure account is connected to a subscription, which is a logical unit of Azure services.

* Azure services are billed on a per-subscription basis.
* Subscriptions have accounts and are associated with Microsoft Entra ID.
* An account is an identity in Microsoft Entra ID or in a directory that is trusted by Microsoft Entra ID.
* The most common way to allow a user access to Azure services is to add them to the Microsoft Entra ID directory linked to the subscription.

There are different types of Azure subscriptions:

* Enterprise agreement: The customer makes an upfront monetory commitment to Azure.
* Reseller: It is an open licensing program.
* Microsoft partner: Find a partner that can design and implement a cloud solution.
* Free trial account: Customer can use a free Azure credit to try out different tiers and types of Azure services.

Azure subscriptions have service limits. These service limits are also called quotas. Below are some points regarding managing these limits:

* Some limits apply to the region level.
* The user can raise soft limits by raising an online customer support rquest at no charge.
* These limits keeps changing.

## Designing for landing zones

Landing zones provide an infrastructure environment for hosting your workloads. 

* They incorporate fundamental principles of governance, security, networking, management, and identity.
* They prepare the environment in advance using code.
* They are suiatable for both migration projects and new deployments. They allow a seamless transition of existing architectural designs.
* Landing zone is an integral component of the Cloud Adoption Framework's ready phase.

The following image shows the flows of the Azure landing zone:

![Azure Landing zones](https://github.com/sunnyadeshara86/microsoft-azure/blob/master/Images/landing-zones.png)

The significance of well-designed landing zones include:

* Security
* Scalability
* Efficiency
* Compliance

## Design for resource groups

### Resource manager

Resource manager is a service that manages and deploys Azure resources.

* It renders a consistent management layer.
* It facilitates collaboration with the resources as a group.
* Enables deployment, updation, or deletion using a single, coordinated operation.
* Provides security, auditing and tagging features.

### Resource group

It is a logical grouping of resources.

* It is a fundamental concept withing the Azure platform.
* It should be closely linked to the lifecycle of the resources.
* A resource must be created within a resource group.
* It must be allocated to each resource.
* Each resource must be in one, and only one resource group.
* It cannot be renamed.
* It can have a wide range of resources (services).
* It can have resources from various regions.
* Most resources can be moved between resource groups.
* Users can easily add, remove, and modify resources by scoping permissions to a resource group.

Resource group organization can be done in following ways:

* For authorization: Since resource groups fall under the scope of RBAC, users can organize resources by who wants to manage them.
* For lifecycle: Deleting a resource group deletes both the group and its contents, making it suitable for disposable resources in production environments.
* For billing: When a user places a resource in a particular resource group, it allows them to be grouped for billing reports.
