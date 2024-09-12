# Designing migration using Microsoft Azure

We will learn following topics here:

* Gain insights into Azure migrate to provide a simplified migration, mordenization, and optimization service for Azure.
* Identify the stages involved in Microsoft Cloud Adoption Framework for Azure to support users in driving Azure adoption across their organization.
* Use the Cloud Adoption Framework to asses, migrate, optimize, and monitor the Azure migration path.
* Gain insights into Azure Database Migration Service to enable online and offline migrations from multiple databases.
* Trace the workflow of AzCopy for copying blobs or files to or from a storage account.
* List the benefits of Azure File Sync to enable the centralization of the organization's file shares.

## Azure Migrate

It helps users migrate on-premise VMware VMs, Hyper-V VMs, physical servers, other virtualized machines, and private or public cloud instances to Azure.

Key features of Azure Migrate:

* Assessment and discovery
* Compatibility analysis
* Performance-based sizing
* Migration tools
* Cost estimation
* Integration with Azure resource mover
* Agentless discovery
* Dependency mapping
* Customizable assessments
* Security and assessments

Cloud migration in the Cloud Adoption Framework:

 The Microsoft Cloud Adoption Framework for Azure is available to support users in driving Azure adoption across their organizations. The key stages involved are:

 * Define strategy: Define the business case for adoption as well as the projected outcomes
 * Plan: Align actionable adoption plans with organizational goals
 * Ready: Prepare the cloud environment for the changes that will be implemented
 * Migrate: Migrate and modernize existing workloads
 * Innovate: Create innovative hybrid or cloud-native solutions
 * Govern: Ensure that the environment and workloads are well-managed
 * Manage: Supports cloud and hybrid solution operations management
 * Organize: Establishes teams and responsibilities to support cloud adoption activities

### VMWare Migration

VMware VMs can be migrated using Azure Migrate Server Migration with the following two options:

* Agentless migration: Allows migration of VMs without installing an agent on the source VMs
* Agent-based migration: Involves the installing of the Azure Site Recovery Mobility service agent on the source VMware VMs

Limitations of agentless migration:

* Limited application awareness can lead to issues with complex dependencies.
* High network bandwidth requirements can impact performance.
* Compatibility constraints may restrict usability.
* Lack of granular control limits customization.

Limitations of agent-based migration:

* Agent installation is required on source VMs.
* Maintenance overhead includes agent updates.
* Compatibility issues may arise with certain systems.

Deployment Tasks Comparison: Agentless vs. Agent-Based:

| Task                                            | Details                                                                        | Agentless          | Agent-based          |
|-------------------------------------------------|--------------------------------------------------------------------------------|--------------------|----------------------|
| Prepare VMware servers and VMs for migration    | Configure a number of settings on VMware servers and VMs                       | Required           | Required             |
| Add the server migration tool                   | Add the Azure Migrate Server Migration tool tothe Azure Migrate project        | Required           | Required             |
| Deploy the Azure Migrate appliance              | Set up a lightweight appliance on a VMware VM for VM discovery and assessment  | Required           | Not-required         |
| Install the mobility service on VMs             | Install the mobility service on each VM the user wants to replicate            | Not-required       | Required             |
| Deploy the Azure Migrate Server                 | Set up an appliance on a VMware VM to discover VMs, and bridge between the 
                                                    mobility service running on VMs and Azure Migrate Server Migration             | Not-required       | Required             |
| Enable VM replication                           | Configure replication settings and select VMs to replicate                     | Required           | Required             |
| Run a test migration                            | Run a test migration to make sure everything is working as expected            | Required           | Required             |
| Run a full migration                            | Migrate the VMs                                                                | Required           | Required             |
