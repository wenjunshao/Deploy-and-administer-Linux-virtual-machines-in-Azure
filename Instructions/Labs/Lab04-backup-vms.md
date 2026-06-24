
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

## Key takeaways

Congratulations on completing the exercise. Here are the main takeaways:

+ A Recovery Services vault stores your backup data and minimizes management overhead.


