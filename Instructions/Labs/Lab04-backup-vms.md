---
lab:
  title: 'Exercise 04: Back up Azure Linux virtual machines'
  module: 'Guided Project: Deploy and administer Linux virtual machines'
  description: Create a Linux virtual machine and configure backups. 
  duration: 30 minutes
  level: 300
  islab: true
  primarytopics:
    - Azure
    - Virtual Machines
    - Backup
---

# Exercise 04: Back up Azure Linux virtual machines

## Lab requirements    

This lab requires an Azure virtual machine. If you don't have a virtual machine, there are instructions to create one. 

This lab requires an Azure subscription. Your subscription type may affect the availability of features in this lab. You may change the regions, but the steps were tested using the **(US) East** region.

### Estimated timing: 30 minutes

## Lab scenario

Your organization is evaluating how to backup Azure virtual machines. Backup will protect the virtual machines from accidental or malicious data loss. You plan to explore using the Azure Backup Center.

## Job skills

+ Skill 0: Create a virtual machine. 
+ Skill 1: Create and configure a Recovery Services vault.
+ Skill 2: Configure Azure virtual machine-level backup.

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
    | Virtual machine names | `VM1` |
    | Region | **(US) East US** |
    | Availability options | **No infrastructure redundancy required** |
    | Security type | **Standard** (review your other choices) |
    | Image | **Ubuntu Server 24.04 LTS - x64 Gen2** (use the drop-down to view other options) |
    | Size | **Standard_D2s_v3** (use **See all sizes** to view the CPU and memory) |
    | Authentication type | **SSH public key** (notice you could use a password) |
    | Username | `adminuser` |
    | SSH public key source | **Generate new key pair** (notice your choices to use an existing key) |
    | SSH Key Type | **RSA SSH Format** |
    | Key pair name | `VM1_key` |
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
    | Region | **East US** |

    >Make sure you use the same region as the virtual machines.

1. Click **Review + Create**, ensure that the validation passes and then click **Create**.

    >Wait for the deployment to complete. The deployment should take a couple of minutes. 

1. When the deployment is completed, click **Go to Resource**.

1. In the **Protected items** section select **Backup items**. Notice the vault does not yet contain any backups. 

**Check your learning**
 + Can you create and configure a Recovery Service vault?
 + Can you determine which protected items are in the vault?


## Skill 2: Configure Azure virtual machine-level backup

In this task, you will implement Azure virtual machine level backup. As part of a VM backup, you will define a backup and retention policy.

1. Continue working on the Recovery Services vault, click **Overview**, then click **+ Backup**.

    >When you [enable a virtual machine backup](https://learn.microsoft.com/azure/backup/quick-backup-vm-portal#enable-backup-on-a-vm) you can configure a backup schedule and retention range. 

1. On the **Backup Goal** blade, specify the following settings:

    | Settings | Value |
    | --- | --- |
    | Where is your workload running? | **Azure** (notice your other options) |
    | What do you want to backup? | **Virtual machine** (notice your other options |

1. Select **Backup**.

1. Notice there a two **Policy sub types**: **Enhanced** and **Standard**. Review the choices and select **Enhanced**. 

1. In **Backup policy**, select **Create a new policy**.

1. Define a new backup policy with the following settings (leave others with their default values):

    | Setting | Value |
    | ---- | ---- |
    | Policy name | `vmbackup` |
    | Frequency | **Daily** |
    | Time | **12:00 AM** |
    | Timezone | the name of your local time zone |
    | Retain instant recovery snapshot(s) for | **2** Days(s) |

1. Click **OK** to create the policy and then, in the **Virtual Machines** section, select **Add**.

    >You can create multiple backup policies or reuse a single backup policy on multiple virtual machines. 

1. On the **Select virtual machines** blade, select **VM4**, click **OK**.

1. On the **Backup** blade, click **Enable backup**.

    >Wait for the backup to be enabled. This should take approximately 2 minutes.

1. In the **Protected items** section, click **Backup items**, and then click the **Azure virtual machine** entry.

1. Select the **View details** link for **VM4** and review the values of the **Backup Pre-Check** and **Last Backup Status** entries.

    >Notice the backup is *initial backup pending*.
    
1. Select **Backup now**, accept the default value in the **Retain Backup Till** drop-down list, and click **OK**. Do not wait for the backup to finish.

**Check your learning**
 + Do you know the difference between an Enhanced and Standard backup policy?
 + Can you configure backup policy retention settings?
 + Can you review the backup job details and status?


## Learn more with self-paced training

+ [Introduction to Azure Backup](https://learn.microsoft.com/training/modules/intro-to-azure-backup/). Describe how the features of Azure Backup work to provide backup solutions for your needs.
+ [Protect your virtual machines by using Azure Backup](https://learn.microsoft.com/training/modules/protect-virtual-machines-with-azure-backup/). Use Azure Backup to help protect on-premises servers, virtual machines, SQL Server, Azure file shares, and other workloads.

## Key takeaways

Congratulations on completing the exercise. Here are the main takeaways:

+ A Recovery Services vault stores your backup data and minimizes management overhead.
+ Azure Backup service provides simple, secure, and cost-effective solutions to back up and recover your data.
+ Azure Backup can protect on-premises and cloud resources including virtual machines and file shares.
+ Azure Backup policies configure the frequency of backups and the retention period for recovery points. 






