---
lab:
  title: 'Exercise 04: Back up Azure Linux virtual machines'
  module: 'Guided Project: Deploy and administer Linux virtual machines'
  description: Create a Linux virtual machine. 
  duration: 30 minutes
  level: 300
  islab: true
  primarytopics:
    - Azure
    - Virtual Machines
---

# Exercise 04: Create Azure Linux virtual machines

## Lab requirements    

This lab requires an Azure subscription. Your subscription type may affect the availability of features in this lab. You may change the regions, but the steps were tested using the **West US 3** region.

### Estimated timing: 30 minutes

## Job skills

+ Skill 0: Use the Azure portal to create a virtual machine. 
+ Skill 1: Create and configure a Recovery Services vault.

### Estimated timing: 30 minutes

## Architecture diagram

![Diagram for lab 04 architecture.](./media/lab04.png)

## Azure Virtual Machines Architecture Diagram

![Diagram of the lab 01 architecture](./media/lab01.png)

## Skill 0: Use the Azure portal to create a virtual machine

In this task, you will create and deploy a Linux virtual machine using the portal. 

1. Sign in to the Azure portal - `https://portal.azure.com`.

    >In this first lab you will use the Azure portal to create the virtual machine. This will give you a good overview of the configuration settings. In a later lab you will use the Azure CLI to create a virtual machine. 

1. **Cancel** the **Welcome to Microsoft Azure** splash screen. 

1. Use the top search box to search for and select `Virtual machines`.

1. Click **+ Create**, and then select in the drop-down **Virtual machine**. Notice your other choices.

1. On the Basics tab, continue completing the configuration:

    >Use the Informational icons to learn about each parameter. If a value isn't specified, use the default value. 

    | Setting | Value |
    | --- | --- |
    | Subscription | the name of your Azure subscription |
    | Resource group |  **RG1** (If necessary, click **Create new**) |
    | Virtual machine names | `vm-rg1` |
    | Region | **West US 3** |
    | Availability options | **No infrastructure redundancy required** |
    | Security type | **Standard** (review your other choices) |
    | Image | **Ubuntu Server 24.04 LTS - x64 Gen2** (use the drop-down to view other options) |
    | Size | **Standard DS15 v2** (use **See all sizes** to view the CPU and memory) |
    | Authentication type | **password**  |
    | Username | `adminuser` |
    | password | `adminuser` |
    | Public inbound ports |**None** |

    >Did you know [virtual machine sizes](https://learn.microsoft.com/azure/virtual-machines/sizes/overview) are categorized into different families and types, each optimized for specific purposes. For example, compute optimized VM sizes have a high CPU-to-memory ratio. Good for medium traffic web servers, network appliances, batch processes, and application servers.

1. Click **Next: Disks >** , specify the following settings (leave others with their default values):

    | Setting | Value |
    | --- | --- |
    | OS disk size | **Image default (30 GiB)** |
    | OS disk type | **Premium SSD (locally redundant storage** |
    | Delete with VM | **checked** (default) |
    | Enable Ultra Disk compatibility | **Unchecked** |

    >Notice you can add a data disk to the virtual machine. We will do this in a later exercise. 

1. Click **Next: Networking >** and make a few changes. 

    | Setting | Value |
    | --- | --- |
    | Delete public IP and NIC when VM is deleted | **Checked** |
    | Load balancing options | **None** |


1. Click **Next: Management >** and check the following settings (leave others with their default values):

    | Setting | Value |
    | --- | --- |
    | Enable auto-shutdown | **unchecked** |
    | Patch orchestration options | **Image default** |  

    >Patch orchestration options allow you to control how patches will be applied to your virtual machine. 

1. Click **Next: Monitoring >** and specify the following settings (leave others with their default values):

    | Setting | Value |
    | --- | --- |
    | Boot diagnostics | **Disable** |

    >We will review monitoring in another exercise. 

1. Click **Next: Advanced >** and notice the **Custom data** textbox. This is where you would pass a cloud-init script, configuration file, or other data into the virtual machine while it is being provisioned. Do not make any changes.

1. Click **Review + Create**.

1. After the validation passes, click **Create**.

1. When prompted, select **Download private key and create resource**. 

    >If you receive a message, *Can not download private key*, just click the download button again. 

1. Wait for the deployment to complete, then select **Go to resource**. This will take a couple of minutes. 

1. From the **Overview** blade, ensure the virtual machine **Status** is **Running**. 

**Check your learning.** 
 + Can you access the Azure portal?
 + Can you use the Azure portal to create a Linux virtual machine?
 + Can you select the correct the Linux image and virtual machine size?


## Skill 1: Create and configure a Recovery Services vault

In this task, you will create a Recovery Services vault. 

1. In the Azure portal, search for and select `Recovery Services vaults`.

    >A [Recovery Services vault](https://learn.microsoft.com/azure/backup/backup-azure-recovery-services-vault-overview)  is a storage entity in Azure that houses data. The data is typically copies of data, or configuration information for virtual machines, workloads, servers, or workstations. 

1. On the **Recovery Services vaults** blade, click **+ Create**.

1. On the **Create Recovery Services vault** blade, specify the following settings:

    | Settings | Value |
    | --- | --- |
    | Subscription | the name of your Azure subscription |
    | Resource group | `RG1`  |
    | Vault Name | `RSV1` |
    | Region | **West US 3** |

    >Make sure you use the same region as the virtual machines.

1. Click **Review + Create**, ensure that the validation passes and then click **Create**.

    >Wait for the deployment to complete. The deployment should take a couple of minutes. 

1. When the deployment is completed, click **Go to Resource**.

**Check your learning**
 + Can you create and configure a Recovery Service vault?
 + Can you determine which protected items are in the vault?

## Key takeaways

Congratulations on completing the exercise. Here are the main takeaways:

+ A Recovery Services vault stores your backup data and minimizes management overhead.


