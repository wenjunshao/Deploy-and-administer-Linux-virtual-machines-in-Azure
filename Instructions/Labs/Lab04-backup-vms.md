
# Exercise 0: Create Azure Linux virtual machines

## Lab requirements    

This lab requires an Azure subscription. Your subscription type may affect the availability of features in this lab. You may change the regions, but the steps were tested using the **West US 3** region.


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

    >In this first lab you will use the Azure portal to create the virtual machine. This will give you a good overview of the configuration settings. 

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
    | password | `Adminuser&123` |
    | Public inbound ports |**None** |

    >Did you know [virtual machine sizes](https://learn.microsoft.com/azure/virtual-machines/sizes/overview) are categorized into different families and types, each optimized for specific purposes. For example, compute optimized VM sizes have a high CPU-to-memory ratio. Good for medium traffic web servers, network appliances, batch processes, and application servers.

1. Click **Review + Create**.

1. After the validation passes, click **Create**.

1. Wait for the deployment to complete, then select **Go to resource**. This will take a couple of minutes. 

1. From the **Overview** blade, ensure the virtual machine **Status** is **Running**. 

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


## Key takeaways

Congratulations on completing the exercise. Here are the main takeaways:

+ A Recovery Services vault stores your backup data and minimizes management overhead.


