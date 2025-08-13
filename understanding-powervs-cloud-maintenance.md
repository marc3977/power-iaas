---

copyright:
  years: 2018, 2024
lastupdated: "2025-08-15"

keywords: virtual machine (VM), vm, power, compute, virtual machines, planning, best practices, instances, virtual machines (VM), virtual machine (VM) instance, Power virtual machine (VM) , maintenance, IBM Power S922, IBM Power E980, IBM Power S1022, IBM Power S1122, S922, E980, S1022, S1122

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Understanding cloud maintenance operations
{: #about-cloud-maintenance}

## Types of maintenance operations that affect your virtual machine (VM) instances
{: #types-of-maintenance}

### Host and dedicated host maintenance
{: #types-of-maintenance-host}

{{site.data.keyword.cloud}} performs periodic maintenance on the server hosts and dedicated hosts that run virtual machines (VM), storage and network. This maintenance upgrades the software on the underlying hypervisor, update the firmware on the hosts, network insfrastructure, storage infrastructure, or other security and performance updates. In general, users don't experience any issues during these upgrades. Modifications that require host maintenance are applied with no or little impact to running services in most cases. Scenarios can occur where the user is involved during maintenance operations.

Most updates are done transparently to the host and the virtual machines (VM) that run on those hosts do not see any disruption. Nondisruptive changes can occur multiple times per week or even daily if necessary, all without impacting the user experience.

### Data center maintenance
{: #types-of-maintenance-data-center}

{{site.data.keyword.cloud}} also performs periodic data center maintenance upgrades. Users don't generally experience any issues during data center maintenance. Examples of this maintenance can be updates to the network, power infrastructure, or server hardware in a data center. Most maintenance is performed without impact to the user’s workloads. Some infrequent scenarios can occur where the user might need to be involved during those operations, which are discussed in the following section.

## Possible impacts to workloads during Control Plane maintenance operations
{: #control-plane-maintenance-impacts}

Maintenance to the Control Plane may affects activities such as provisioning (add/modify/remove resources).

Some changes can require a live partition migration(LPM) of a virtual machine (VM) to update the hypervisor or host. These changes can be a firmware update, an event where the hypervisor kernel cannot be live patched, or load balancing. The regular live migration process(LPM) is nondisruptive and the use of dedicated hosts and virtual machines (VM) is not interrupted.

When non-disruptive live partition migration occurs, the virtual machine (VM) experiences a brief pause of around 10 seconds, and in some cases up to 30 seconds. You are not notified in advance of nondisruptive migration. The virtual machine (VM) instance is not restarted as part of this process.

In cases where a disruptive migration is required, you are notified 30 days in advance of the scheduled migration. The virtual machine (VM) instance is restarted as part of this process.

In limited cases, a virtual machine (VM) restart might be required to complete the host or data center maintenance. This scenario can occur when specialized VMs are used or if the virtual machine (VM) encounters a migration problem. In this case, a scheduled maintenance event occurs.

{: note}

## Possible impacts to workloads during Data Plane maintenance operations
{: #date-plane-maintenance-impacts}

During Data Plane maintenance, some of the maintenance is transparent. In some cases, there will be loss of redundancy and may also affect provisioning.

### Network maintenance
There can be a brief period of loss to packets-in-flight between PowerVS to Cloud services via PER connectivity while traffic normalises between the redundant modules. This is expected and normal during convergence. Additionally, all customer traffic(connectivity to PowerVS instances) may face packet loss or brief network interruption during this activity.

### Storage maintenance

In the case of storage maintenance to storage controllers or SAN switches, there can be a loss of redudant path which will also be reported in the operating systems of the virtual machines (VM).

It is highly recommended to perform the following prior to the start of a maintenance window:
- Be sure to apply the most recent OS patches
- Verify the OS system health and correct any issues
- Ensure to have a current backup of the system and data
- Please check that all disk paths on virtual machines are configured and online
- Please ensure any provisioning activities are completed before the start of the maintenance, or re-scheduled until after the maintenance window.
- If a VM is part of a high availability cluster with disk heartbeating enabled (or equivalent disk monitoring feature), you may need to adjust the timeout values.

Post-Maintenance customer activity:
- Please check that all disk paths have recovered and are online after each a maintenance has concluded. In some cases, a new device scan may need to be performed to recover any offline paths.


{: note}



