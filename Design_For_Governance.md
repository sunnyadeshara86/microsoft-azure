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

#### Recommend a strategy for resource tegging

Tags logically organize the resources. They consist of a name-value pair and help retrieve related resources from different resource groups. Resource tagging is helpful when users need to organize resources for billing.

Limitations of tags:

* Each resource or resource group can have a maximum of 50 tag name-value pairs.
* The tag name has a limit of 512 characters, and the tag value has a limit of 256 characters.
* For storage accounts, the tag name is limited to 128 characters and value to 256 characters.
* Not all resource types support tags.
* Tag applied to resource groups are not inherited by the resources in that resource group.
* Tags can be enforced with the help of policy.

Enforcing tags with policy:

| Policy                                                               | Description                                                                                           |
|----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| Apply tag and its default value                                      | * Appends a specified tag name and value, if that tag is not provided <br/> * Specify the tag name and value to apply                                                                                                                                                                                                     |
| Billing tags policy initiative                                       | * Requires specified tag values for cost center and product name <br /> * Uses built in policies to apply and enforce required tags <br /> * Specify the required values for the tags                                                                                                                                     |
| Enforce tag and its value                                            | * Requires a specified tag name and value <br /> * Specify the tag name and value to enforce          |
| Enforce tag name and its value on resource groups                    | * Requires a specified tag name and value on a resource group <br /> * Specify the required tag name and value                                                                                                                                                                                                            |
#### Recommend a solution for using Azure policy

Azure policy helps enforce organizational standards and asses compliance at scale.

* The compliance dashboard offers a consodilated view to asses the environment's overall status, allowing detailed analysis at the resource and policy levels.
* It includes implementing governance for resource consistency, regulatory compliance, security, cost, and management.

Example: Users can create only a certain SKU size of virtual machines in your environment.

Bebefits of Azure policies:

* Enforcement and compliance: Turn on policies for resources and get real-time policy evaluation and enforcement.
* Apply policies at scale: Apply multiple policies and aggregate policiy states with the policy initiative.
* Remediation: It provides real-time remediation.

Steps to implement Azure policies:

* Browse policy definitions
  * A policy definition defines under what condition a policy is enforced and what effect to take.
  * Example: Users could prevent VMs from being deployed if they are exposed to a public IP address.
  * Users can import policies from GitHub.
  * Policy definitions have a specific JSON format.
* Create initiative definitions
  * Group policy definitions.
  * Include one or more policies.
  * Manage planning.
* Scope the initiative definition
  * The scope determines what resources or group of resources the policy is enforced on.
  * Assign the definition to a scope.
  * Select the subscription and optionally the resource group.
  * An initiative definition can have up to 100 policies.
* View policy evaluation results
  * Determine compliance
    * Non-compliant initiatives
      * Non-compliant policies: It is the number of policy assignments with at least one non-compliat resource.
      * Non-compliant resources: Once a condition is evaluated against the existing resources and found to be true, the resources are marked as non-compliant with the policy.
  * Policy effects
    * The policy creates a list of all assignments that apply to the resource and then evaluates the resource.
    * Azure policy evaluates the requests to create or update a resource through the Azure resource manager.
    * Policy processes several of the effects before handling the request to the appropriate resource provider to avoid violating policy.
      * Deny: The resource creation / updation fails due to policy.
      * Disabled: The policy rule is ignored (Disabled), often used for testing.
      * Append: Adds additional parameters / fields to the requested resource during cration or updation. A common example is adding tags on resources such as Cost Center or specifying allowed IPs for a storage resource.
      * Audit, AuditIfNotExists: Creates a warning event in the activity log when evaluating a non-compliant resource, but it doesn't stop the request.
      * DeployIfNotExists: Executes a template deployment when the condition is met. Example: Evaluates SQL Server databases to determine whether transparentDataEncryption is enabled. If not, then a deployment to enable is executed.

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

## Design for Azure RBAC

It is a fundamental Azure service that enables fine-grained access control for Azure resources. It follows the principle of granting permissions based on roles, ensuring the reight people have the right access.

Designing effective RBAC in Azure:

* Identify roles
* Define scope
* Assign roles

Benefits of RBAC:

* Improved security: Only authorized individuals can carry out specific actions on Azure resources, minimizing the risk of security breaches.
* Granular control: It enablesdetailed management of permissions, advocating a least privilege access model.
* Compliance: It helps in meeting regulatory requirements by providing access controls and audit trails.
* Efficiency: It streamlines resource management by delegating responsibilities to the right roles.

RBAC Use Cases:

* Project-Based Access: Assign roles based on project teams, limiting access to relevant resources.
* Compliance and Audit: Implement RBAC for compliance requirements and auditing needs.
* Resource Group Level Control: Use RBAC to control access at the resource group level for a more organized approach.
* External Collaborators: Grant restricted access to external collaborators by using custom roles.

RBAC Best practices:

* Regular Review: Periodically review and update RBAC assignments to align with changing roles and responsibilities.
* Custom Roles: Create custom roles when predefined Azure roles don't match with organization's requirements.
* Role Segregation: Avoid over-assigning broad permissions. Segregate duties by assigning minimal necessary permissions.

Combining Azure Policy and RBAC:

![Combining Azure RBAC and Azure Policy](https://github.com/sunnyadeshara86/microsoft-azure/blob/master/Images/rbac-azure-policy.jpeg)
