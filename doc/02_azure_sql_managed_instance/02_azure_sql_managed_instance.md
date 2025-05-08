# Exercise 02: Create and manage an SQL Managed Instance in Azure

## Scenario

Adatum Corporation is a national retail chain headquartered in Atlanta, GA, with 1,500 stores across the United States. The company is dedicated to leveraging cutting-edge technology and AI-driven tools to improve customer interactions and streamline operations. Adatum Corporation recently launched an eBook store, Adatum Books. They are currently using an on-premises SQL VM to store their data and application. Concerned about business continuity and potential disruptions to their eBook shopping services, they seek to implement a solution that ensures high availability and disaster recovery.

This exercise is designed to provide you with hands-on experience in setting up and managing an SQL Managed Instance in Azure. Throughout this exercise, you'll explore various aspects of SQL Managed Instance, including its configuration, network connectivity, and data replication.

You'll work with Azure SQL Managed Instance, a fully managed SQL Server database engine that provides built-in high availability, automated backups, and scaling capabilities; SQL Server on Azure Virtual Machines (VMs), which offers full control over the SQL Server environment and integration with other Azure services; and SQL Server Management Studio (SSMS), a powerful tool for managing SQL Server instances, databases, and their components.

By the end of this exercise, you'll have a comprehensive understanding of how to set up, configure, and manage an SQL Managed Instance in Azure. You'll also gain practical experience in ensuring network connectivity, replicating data, and performing failovers, which are essential skills for managing SQL databases in a cloud environment.

## Objectives

After you complete this exercise, you'll be able to:

-   Set up, configure, and manage a SQL Managed Instance in Azure.
-   Replicate data between SQL Server and Azure SQL Managed Instance.
-   Perform failovers, ensuring high availability and disaster recovery.

## Duration

**Estimated time:** 60 minutes

===

# Sign to the lab VM

Before you begin, sign in to the VM environment you'll use for the duration of this lab.

- [] Sign in to the machine using the credentials provided here.

    | Item | Value |
    | --- | --- |
    | Username | +++@lab.VirtualMachine(Workstation1).Username+++ |
    | Password | +++@lab.VirtualMachine(Workstation1).Password+++ |

# Task 01: Prepare the environment

## Introduction

Establishing a Managed Instance link is crucial for Adatum Corporation to ensure high availability and disaster recovery for their eBook store, Adatum Books. This process involves creating an Azure SQL Managed Instance and verifying the deployment of an Azure SQL VM to enable replication between the on-premises SQL VM and the Azure SQL Managed Instance. This setup is essential for maintaining business continuity and preventing disruptions to their eBook shopping services.

## Description

In this task, you'll set up the environment for a Managed Instance link, enabling replication between SQL Server (on Windows or Linux) and an Azure SQL Managed Instance. You'll create an Azure SQL Managed Instance, verify the deployment of an Azure SQL VM, and access the virtual machine to configure SQL Server settings.

## Success criteria

-   You successfully created an Azure SQL Managed Instance.
-   You verified the deployment of an Azure SQL VM.
-   You accessed the virtual machine and configured SQL Server settings.
-   You enabled replication between the on-premises SQL VM and the Azure SQL Managed Instance.
-   You ensured the setup supported high availability and disaster recovery for Adatum Corporation's eBook store, Adatum Books.

## Learning resources

-   [Prepare your environment for a link - Azure SQL Managed Instance](https://learn.microsoft.com/en-us/azure/azure-sql/managed-instance/managed-instance-link-preparation?view=azuresql)
-   [Create an Azure SQL Managed Instance](https://learn.microsoft.com/en-us/azure/azure-sql/managed-instance/instance-create-quickstart?view=azuresql)
-   [Verify the deployment of an Azure SQL VM](https://learn.microsoft.com/en-us/shows/azure-sql-for-beginners/deploy-and-verify-azure-sql-13-of-61)
-   [SQL Server Configuration Manager](https://learn.microsoft.com/en-us/sql/relational-databases/sql-server-configuration-manager?view=sql-server-ver16)

===

## 01: Create the target SQL managed instance

1. [] Open Microsoft Edge, go to `https://portal.azure.com`, then sign in with your lab credentials:

    | Item | Value |
    |:--------|:--------|
    | Username   | `@lab.CloudPortalCredential(User1).Username`   |
    | Password  | `@lab.CloudPortalCredential(User1).Password`   |

1. [] In the top global search bar, enter and select **`Azure SQL`**.

    !IMAGE[1t89ypzp.jpg](instructions286351/1t89ypzp.jpg)

1. [] Select **Create** on the top command bar.

    !IMAGE[fc3d9nvq.jpg](instructions286351/fc3d9nvq.jpg)

1. [] Under **SQL managed instances**, select **Create**.

    !IMAGE[jxzwcllq.jpg](instructions286351/jxzwcllq.jpg)

1. [] In the **Want to try SQL MI for free?** banner, select **Apply free offer** to use the free trial.

    !IMAGE[8yyyxro8.jpg](instructions286351/8yyyxro8.jpg)

1. [] Use the following information to fill out the **Basics** tab:

    | Item | Value |
    | --- | --- |
    | Resource group | **`@lab.CloudResourceGroup(ResourceGroup1).Name`** |
    | Region | **@lab.CloudResourceGroup(ResourceGroup1).Location** |
    | Authentication method | **Use SQL authentication** |
    | Managed instance admin login | **`MILab`** |
    | Password | **`@lab.Variable(azurePw)`** |

    !IMAGE[tbwokju7.jpg](instructions286351/tbwokju7.jpg)

    >[!Hint]
    > | Region Code | Portal UI |
    > | --- | --- |
    > | eastus | (US) East US |
    > | eastus2 | (US) East US 2 |
    > | southcentralus | (US) South Central US |
    > | westus2 | (US) West US 2 |

1. [] Select **Next: Networking >** at the bottom.

1. [] Select the **Virtual network / subnet** dropdown, then select the existing subnet: **SQLMI-VNET/ManagedInstanceSubnet**.

    !IMAGE[6asoco1i.jpg](instructions286351/6asoco1i.jpg)

    >[!note] You're using the same virtual network as the VM that'll be the primary replica for the SQL database.

1. [] Next to **Public endpoint (data)**, select **Disable**.

    !IMAGE[rgm03pg2.jpg](instructions286351/rgm03pg2.jpg)

1. [] Select **Review + create** at the bottom to review the settings, but **do not create**.

    >[!alert] Do not create. A Managed Instance with these configurations is already being deployed. 

    >[!knowledge] A Managed Instance may take up to 6 hours to deploy, unless it meets the various requirements for [fast provisioning](https://learn.microsoft.com/en-us/azure/azure-sql/managed-instance/management-operations-overview?view=azuresql#fast-provisioning), which can take under 30 minutes.

===

## 02: Verify the Azure SQL VM deployment

At the start of this lab, an Azure VM with the resources you'll need for this exercise, began deployment. You'll need to verify its completion.

1. [] In the same tab, expand the portal menu by selecting the menu icon in the upper left, then select **Resource Groups**.

    !IMAGE[l3nuhru6.jpg](instructions286351/l3nuhru6.jpg)

1. [] Select **OK** to discard the unsaved edits.

1. [] Select **@lab.CloudResourceGroup(ResourceGroup1).Name**.

1. [] Next to **Deployments**, if it still shows **1 Deploying**, select it.

    !IMAGE[yiymkozz.jpg](instructions286351/yiymkozz.jpg)

1. [] Select the numbers listed under **Deployment name**.

    !IMAGE[7t2xdt5g.jpg](instructions286351/7t2xdt5g.jpg)

1. [] Under the **Resource** column, wait until **SQLVM1/CustomScriptExtension** shows a checkmark.

    !IMAGE[ydrq0qdp.jpg](instructions286351/ydrq0qdp.jpg)

    >[!alert] This may take 5-10 minutes to complete. You do **not** need to wait for the **SQL managed instance** deployment at this time. You’ll return to this tab at a later step to verify completion.

===

## 03: Access the Azure SQL VM

1. [] In the upper left, right-click the **ResourceGroup1 | Deployments** breadcrumb link, then select **Open link in new tab** to go to **@lab.CloudResourceGroup(ResourceGroup1).Name**.

    !IMAGE[f3sb7h59.jpg](instructions286351/f3sb7h59.jpg)

1. [] Under your **Resources**, copy and paste the name of your **SQL managed instance** in the text box below. 

    It will be formatted **free-sql-mi-[random]**. This value will continue to be referenced throughout this lab.

    @lab.TextBox(miName)

    !IMAGE[ojuj0fw6.jpg](instructions286351/ojuj0fw6.jpg)

    >[!note] Do not enter the value from the screenshot.

1. [] Select the **SQLVM1** Virtual machine.

    !IMAGE[rn273hvr.jpg](instructions286351/rn273hvr.jpg)

    >[!note] This is a Windows Server 2019 VM with SQL Server 2019.

1. [] On the left service menu, select **Connect**, then select **Connect**.

    !IMAGE[tutkv2eh.jpg](instructions286351/tutkv2eh.jpg)

1. [] In the **Native RDP** tile, select **Download RDP file**.

    !IMAGE[jmj461sj.jpg](instructions286351/jmj461sj.jpg)

1. [] Select the file from the Edge **Downloads** to open. You can access it again from the Windows 11 **Downloads** folder.

    !IMAGE[e8wadfmd.jpg](instructions286351/e8wadfmd.jpg)

1. [] Select the checkbox for **Don't ask me again...**, then select **Connect**.

    !IMAGE[got17pvb.jpg](instructions286351/got17pvb.jpg)

1. [] Enter the Azure VM credentials, then select **OK** to connect.

    | Item | Value |
    |:--------|:--------|
    | Username   | **VMLab**   |
    | Password  | **`@lab.Variable(azurePw)`**   |

1. [] On the warning dialog, select the **Don't ask me again...** checkbox, and select **Yes**.

    !IMAGE[qu2v80lo.jpg](instructions286351/qu2v80lo.jpg)

===

## 04: Create a database master key

You'll need to create a database master key as part of the requirements to setup the Managed Instance link.

1. [] On the **SQLVM1** desktop, open SQL Server Management Studio.

    !IMAGE[wcubqkcv.jpg](instructions286351/wcubqkcv.jpg)

1. [] Select the **Trust server certificate** checkbox, then select **Connect**.

    !IMAGE[pcmqoj6l.jpg](instructions286351/pcmqoj6l.jpg)

1. [] Select **New Query** on the toolbar.

    !IMAGE[gjb4s8j7.jpg](instructions286351/gjb4s8j7.jpg)

1. [] Create a database master key in the master database by pasting the following query:

    ```
    -- Run on SQL Server
    -- Create a master key
    USE master;
    GO
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '@lab.VirtualMachine(Workstation1).Password';
    ```

    >[!note] Selecting **Copy** on these code blocks and pasting will be much quicker than using **Type**.

1. [] Select **Execute** on the top toolbar.

    !IMAGE[w5ygxrzw.jpg](instructions286351/w5ygxrzw.jpg)

===

## 05: Enable availability groups

The Managed Instance link relies on the Always On Availability Groups feature of SQL Server, which is disabled by default. 

>[!knowledge] For more information, see [Enable the Always On availability groups feature](https://learn.microsoft.com/en-us/sql/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server?view=sql-server-ver16).

1. [] Select the Windows start menu, then enter and select **`SQL Server 2019 Configuration Manager`**.

    !IMAGE[tb7iex4t.jpg](instructions286351/tb7iex4t.jpg)

1. [] On the left menu, select **SQL Server Services**.

1. [] Right-click **SQL Server (MSSQLSERVER)**, then select **Properties**.

    !IMAGE[w2nh6uxs.jpg](instructions286351/w2nh6uxs.jpg)

1. [] Select the **Always On Availability Groups** tab.

1. [] Select the **Enable Always On Availability Groups** checkbox, then select **Apply**.

    !IMAGE[qdzkuhfb.jpg](instructions286351/qdzkuhfb.jpg)

1. [] Select **OK** on the **Warning** dialog. Keep the **Properties** window open.

===

## 06: Enable startup trace flags

To optimize the performance of your link, it's recommended to enable the following trace flags at startup:

- **-T1800**: This trace flag optimizes performance when the log files for the primary and secondary replicas in an availability group are hosted on disks with different sector sizes, such as 512 bytes and 4 KB. If both primary and secondary replicas have a disk sector size of 4 KB, this trace flag isn't required. 
    
    >[!knowledge] For more information, see [KB3009974](https://support.microsoft.com/en-us/topic/kb3009974-fix-slow-synchronization-when-disks-have-different-sector-sizes-for-primary-and-secondary-replica-log-files-in-sql-server-ag-and-logshipping-environments-ed181bf3-ce80-b6d0-f268-34135711043c).

- **-T9567**: This trace flag enables compression of the data stream for availability groups during automatic seeding. The compression increases the load on the processor but can significantly reduce transfer time during seeding.

---

1. [] Select the **Startup Parameters** tab.

1. [] Enter `-T1800`, then select **Add**.

1. [] Enter `-T9567`, then select **Add**.

    !IMAGE[glqpm6mq.jpg](instructions286351/glqpm6mq.jpg)

1. [] Select **OK**, then select **OK** on the **Warning** dialog.

1. [] Restart SQL Server by right-clicking **SQL Server (MSSQLSERVER)**, then select **Restart**.

    !IMAGE[k0a3eb1l.jpg](instructions286351/k0a3eb1l.jpg)

>[!knowledge] For more information, see the [syntax to enable trace flags](https://learn.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-traceon-transact-sql?view=sql-server-ver16).

===

## 07: Validate the configuration

1. [] Go back to your open **SQL Server Management Studio** window.

1. [] Replace your previous query for setting the master key with the following:

    ```
    -- Shows if the Always On availability groups feature is enabled
    SELECT SERVERPROPERTY ('IsHadrEnabled') as 'Always On enabled (1 true, 0 false)';
    GO
    -- Lists all trace flags enabled on SQL Server
    DBCC TRACESTATUS;
    ```

1. [] Select **Execute** on the top toolbar.

    !IMAGE[w29m4m3m.jpg](instructions286351/w29m4m3m.jpg)

    >[!note] **Always On enabled** should be **1**.
    > 
    >**1800** and **9567** should be listed.
    >
    > If not, restart SQL Server again from SQL Server Configuration Manager.

---

**Congratulations!** You've successfully completed this task.

===

## Task 02: Configure network connectivity

## Introduction

Ensuring robust network connectivity is essential for Adatum Corporation to maintain high availability and disaster recovery for their eBook store, Adatum Books. To prevent disruptions to their eBook shopping services, they seek to implement a solution that ensures seamless network connectivity between their on-premises SQL VM and Azure SQL Managed Instance.

## Description

In this task, you'll configure network security settings, open required firewall ports, and test connectivity between SQL Server and the Azure SQL Managed Instance.

The Azure SQL Server VM is within the same virtual network as the targeted Managed Instance in this scenario.

## Success criteria

-   You configured the network security settings and opened the required firewall ports.
-   You tested and confirmed connectivity between SQL Server and the Azure SQL Managed Instance.
-   You ensured the Azure SQL Server VM is within the same virtual network as the targeted Managed Instance.

## Learning resources

-   Configure network security settings
-   [Test connectivity between SQL Server and the Azure SQL Managed Instance](https://learn.microsoft.com/en-us/troubleshoot/sql/database-engine/connect/test-oledb-connectivity-use-udl-file)

***

**SQL Server on Azure Virtual Machines**

For the link to work, you must have network connectivity between SQL Server and Managed Instance. The network option that you choose depends on whether or not your SQL Server instance is on an Azure network.

Deploying SQL Server on Azure Virtual Machines in the same Azure virtual network that hosts SQL Managed Instance is the simplest method, because network connectivity will automatically exist between the two instances.

>   [!knowledge] For more information, see [Quickstart: Configure an Azure VM to connect to Azure SQL Managed Instance](https://learn.microsoft.com/en-us/azure/azure-sql/managed-instance/connect-vm-instance-configure?view=azuresql).

***

**Different virtual network**

If your SQL Server on Azure Virtual Machines instance is in a different virtual network from your managed instance, you need to make a connection between both virtual networks. The virtual networks don't have to be in the same subscription for this scenario to work.

There are two options for connecting virtual networks:

-   [Azure virtual network peering](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-peering-overview)
-   VNet-to-VNet VPN gateway ([Azure portal](https://learn.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal), [PowerShell](https://learn.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps), [Azure CLI](https://learn.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-cli))

Peering is preferable because it uses the Microsoft backbone network, so from the connectivity perspective, there's no noticeable difference in latency between virtual machines in a peered virtual network and in the same virtual network.

Virtual network peering is supported between networks in the same region. Global virtual network peering is supported for instances hosted in subnets created after September 22, 2020.

>   [!knowledge] For more information, see [Frequently asked questions (FAQ)](https://learn.microsoft.com/en-us/azure/azure-sql/managed-instance/frequently-asked-questions-faq?view=azuresql#does-sql-managed-instance-support-global-vnet-peering).

***

**SQL Server outside Azure**

If your SQL Server instance is hosted outside Azure, establish a VPN connection between SQL Server and SQL Managed Instance by using either of these options:

-   [Site-to-site VPN connection](https://learn.microsoft.com/en-us/microsoft-365/enterprise/connect-an-on-premises-network-to-a-microsoft-azure-virtual-network?view=o365-worldwide)
-   [Azure ExpressRoute connection](https://learn.microsoft.com/en-us/azure/expressroute/expressroute-introduction)

>   [!hint] ExpressRoute is recommended for the best network performance when you're replicating data. Provision a gateway with enough bandwidth for your use case.

===

## 01: Network ports between the environments

Regardless of the connectivity mechanism, there are requirements that must be met for the network traffic to flow between the environments. 

In this task, you'll open ports in Windows Firewall on the SQL VM, then configure ports on the Network Security Group (NSG) attached to the Managed Instance.

---

### Open ports on the Windows Firewall

1. [] On the Azure SQL VM, **SQLVM1**, select the Windows start menu, then enter and select **`Windows Powershell`**.

1. [] Enter the following to open the inbound and outbound ports needed, by creating new firewall rules:

    ```
    # Inbound rule: Allow TCP port 5022 (any source IP)
    New-NetFirewallRule -DisplayName "Allow TCP port 5022 inbound" -Direction Inbound -Profile Any -Action Allow -LocalPort 5022 -Protocol TCP

    # Outbound rule: Allow TCP port 5022 (any destination IP)
    New-NetFirewallRule -DisplayName "Allow TCP port 5022 outbound" -Direction Outbound -Profile Any -Action Allow -LocalPort 5022 -Protocol TCP

    # Outbound rule: Allow TCP port range 11000-11999 (any destination IP)
    New-NetFirewallRule -DisplayName "Allow TCP ports 11000-11999 outbound" -Direction Outbound -Profile Any -Action Allow -LocalPort 11000-11999 -Protocol TCP
    ```

    !IMAGE[9e03lkfr.jpg](instructions286351/9e03lkfr.jpg)

1. [] Select the minimize button on the VM's top control bar.

    !IMAGE[3nc97y5r.jpg](instructions286351/3nc97y5r.jpg)

---

### Open ports on the Managed Instance NSG

You'll now set up the inbound and outbound security rules for the network security group attached to the Managed Instance.

1. [] On the tab for **SQLVM1** in Azure, select the **ResourceGroup1** breadcrumb link in the upper left.

    !IMAGE[taoe8sif.jpg](instructions286351/taoe8sif.jpg)

1. [] Select the Managed Instance network security group, **SQLMI-@lab.Variable(miName)-NSG**.

    !IMAGE[4w4bnkpw.jpg](instructions286351/4w4bnkpw.jpg)

1. [] On the left service menu, select **Settings**, then select **Inbound security rules**.

    !IMAGE[yibazswq.jpg](instructions286351/yibazswq.jpg)

1. [] Select **Add** at the top.

    !IMAGE[66q0y9zm.jpg](instructions286351/66q0y9zm.jpg)

1. [] Use the following information on the **Add inbound security rule** pane:

    | Item | Value |
    |:--------|:--------|
    | Destination port ranges   | **`5022,11000-11999`**   |
    | Protocol   | **TCP**   |
    | Priority  | **`200`**   |
    | Name | **`AllowSqlLinkInbound`**  |

1. [] Select **Add** at the bottom of the pane.

    !IMAGE[djfuivef.jpg](instructions286351/djfuivef.jpg)

1. [] Select **Outbound security rules** on the left service menu.

1. [] Select **Add** at the top.

1. [] Use the following information on the **Add outbound security rule** pane:

    | Item | Value |
    |:--------|:--------|
    | Destination port ranges   | **`5022,11000-11999`**   |
	| Protocol   | **TCP**   |
    | Priority  | **`200`**   |
    | Name | **`AllowSqlLinkOutbound`**  |

1. [] Select **Add** at the bottom of the pane.

    !IMAGE[td7upgpk.jpg](instructions286351/td7upgpk.jpg)

---

>[!knowledge] #### Knowledge 
>- Ports need to be open in every firewall in the networking environment, including the host server, as well as any corporate firewalls or gateways on the network. In corporate environments, you might need to show your network administrator the information to help open additional ports in the networking layer.
>- While you can choose to customize the endpoint on the SQL Server side, the port numbers for a SQL Managed Instance cannot be changed or customized.
>- IP address ranges of subnets hosting Managed Instances and SQL Servers must not overlap.

===

## 02: Testing network connectivity using SSMS

Bidirectional network connectivity between SQL Server and SQL Managed Instance is necessary for the link to work. After you open ports on the SQL Server side and configure an NSG rule on the SQL Managed Instance side, you can test connectivity by using SQL Server Management Studio (SSMS). 

>[!knowledge] When you use **Network Checker** in SSMS, this automatically creates a temporary SQL Agent job on both SQL Server and the Managed Instance to check the connection. This job is then deleted after the test is finished. 
>
> You can alternatively use Transact-SQL, but you'd need to manually delete the SQL Agent job upon completion.

---

### Retrieve the host name of the Managed Instance from Azure

1. [] Switch to your other tab to check on the deployment of the Managed Instance.

    !IMAGE[72uhpvkx.jpg](instructions286351/72uhpvkx.jpg)

1. [] If completed, select **Go to resource group**.

    !IMAGE[o1lgvkqr.jpg](instructions286351/o1lgvkqr.jpg)

1. [] Select the **@lab.Variable(miName)** SQL managed instance.

    !IMAGE[sxiskt4t.jpg](instructions286351/sxiskt4t.jpg)

1. [] Under the **Essentials** section, copy and paste the value for **Host** in the text box below, for future use throughout this lab.

    @lab.TextBox(miHost)

    !IMAGE[eg5ce04u.jpg](instructions286351/eg5ce04u.jpg)

1. [] On the Windows task bar, reopen **SQLVM1** to return to the Azure VM.

1. [] If needed, sign back in using **+++@lab.Variable(azurePw)+++**.

---

### Test the connection

1. [] In SQL Server Management Studio's **Object Explorer** pane on the left, expand **Databases**.

1. [] Right-click the **Adatum** database, select **Azure SQL Managed Instance link**, then select **Test Connection...**

    !IMAGE[rezougbt.jpg](instructions286351/rezougbt.jpg)

1. [] On the Introduction page, select **Next**.

1. [] All **Prerequisites** should be met. Select **Next**.

1. [] Select **Login**, under **Login to SQL Managed Instance**.

1. [] Enter the following in the **Connect to Server** window:

    | Item | Value |
    |:--------|:--------|
    | Server name   | **`@lab.Variable(miHost)`**   |
    | Authentication   | **SQL Server Authentication**   |
    | Login  | **`MILab`**   |
    | Password  | **`@lab.Variable(azurePw)`**   |

1. [] Select the checkboxes for **Remember password** and **Trust server certificate**, then select **Connect**.

    !IMAGE[wycb8u01.jpg](instructions286351/wycb8u01.jpg)

    >[!alert] If you have issues connecting, the **Server name** value in the instructions is taken from the text box entry for the **Host** value retrieved from Azure. Correct the value in the text box in the earlier step, as it will continue to be referenced in the instructions.

1. [] Select **Next**.

    !IMAGE[c0dz4v6y.jpg](instructions286351/c0dz4v6y.jpg)

1. [] Enter **`SQLMIEndpoint`** for the **Endpoint name**, then select **Next**.

    !IMAGE[juzb99y0.jpg](instructions286351/juzb99y0.jpg)

1. [] On the **Summary** page, select **Finish** to run the test.

1. [] All tests should show **Success**. Select **Close**.

    !IMAGE[ha3y8ife.jpg](instructions286351/ha3y8ife.jpg)

---

**Congratulations!** You've successfully completed this task.

===

# Task 03: Configure link with SSMS

## Introduction

Now that your environment is set up and network connectivity is confirmed, the next step is to create a Managed Instance link. This is crucial for Adatum Corporation’s recently launched eBook store, Adatum Books, to ensure high availability and disaster recovery.

This setup will help Adatum Corporation maintain business continuity and prevent disruptions to their eBook shopping services, ensuring that Adatum Books remain operational even in the event of a failure.

## Description

In this task, you'll create a Managed Instance link. This involves preparing the database for replication, setting up the link using SQL Server Management Studio (SSMS), and verifying that the database is successfully synchronized.

## Success criteria

-   You prepared the database for replication.
-   You set up the Managed Instance link using SSMS.
-   You verified that the database was successfully synchronized.

## Learning resources

-   Tutorial: Prepare the database for replication
-   [Configure link with SSMS - Azure SQL Managed Instance](https://learn.microsoft.com/en-us/azure/azure-sql/managed-instance/managed-instance-link-configure-how-to-ssms?view=azuresql)
-   [Validate Replicated Data](https://learn.microsoft.com/en-us/sql/relational-databases/replication/validate-data-at-the-subscriber?view=sql-server-ver16)

===

## 01: Prepare your database

With SQL Server as your initial primary, you'll need to set its **Recovery Model** to **Full**, then run a full backup to meet requirements.

1. [] In SSMS's left **Object Explorer**, right-click the **Adatum** database, then select **Properties**

    !IMAGE[zso8bqcn.jpg](instructions286351/zso8bqcn.jpg)

1. [] In the new window, select **Options** on the left.

    !IMAGE[kludh74r.jpg](instructions286351/kludh74r.jpg)

1. [] Select the dropdown next to **Recovery model**, select **Full**, then select **OK**.

    !IMAGE[ebr4zi1z.jpg](instructions286351/ebr4zi1z.jpg)

1. [] Right-click the **Adatum** database again, select **Tasks**, then select **Back Up...**

    !IMAGE[kpik3f8o.jpg](instructions286351/kpik3f8o.jpg)

1. [] **Backup type** should be set to **Full**, then select **OK**.

    !IMAGE[66tcwb7x.jpg](instructions286351/66tcwb7x.jpg)

1. [] Select **OK** on the completion dialog.

>[!knowledge] The link supports replicating user databases only. Replication of system databases is not supported. To replicate instance-level objects (stored in **master** or **msdb**), script them out and run T-SQL scripts on the destination instance.

===

## 02: Create the link to replicate the Adatum database

In this task, you'll use the **New Managed Instance link** wizard in SSMS to create a link between your initial primary and your secondary replica.

1. [] Right-click the **Adatum** database again, select **Azure SQL Managed Instance link**, then select **New**.

    !IMAGE[46yxeysg.jpg](instructions286351/46yxeysg.jpg)

1. [] On the Introduction page, select **Next**.

1. [] Enter **`AdatumLink`** in the **Name** field, then select **Next**.

    !IMAGE[4m66njcw.jpg](instructions286351/4m66njcw.jpg)

1. [] On **SQL Server requirements**, everything under the **Server readiness** tab will be **Ready**.

    !IMAGE[5237fxun.jpg](instructions286351/5237fxun.jpg)

1. [] Select the **Availability group readiness** tab.

1. [] If you select the warnings under the **Result** column, you'll see that both will automatically be created, so these are safe to ignore.

    !IMAGE[7pp3jueg.jpg](instructions286351/7pp3jueg.jpg)

    !IMAGE[99jfcwd5.jpg](instructions286351/99jfcwd5.jpg)

1. [] Select **Next** to proceed.

1. [] Select the checkbox next to **Adatum**, then select **Next**.

    !IMAGE[b6mxrn43.jpg](instructions286351/b6mxrn43.jpg)

1. [] On **Specify Secondary Replica**, select **Add secondary replica...**

    !IMAGE[26ug48s7.jpg](instructions286351/26ug48s7.jpg)

1. [] Select **Sign In...**, then sign in with your lab's Azure credentials:

    | Item | Value |
    |:--------|:--------|
    | Username   | `@lab.CloudPortalCredential(User1).Username`   |
    | Password  | `@lab.CloudPortalCredential(User1).Password`   |

    > [+Alert] If Internet Explorer opens, change your default browser to Edge and try again. Select this box to expand for details.
    >
    >1. Select the Windows Start menu.
    >1. Enter and select **`Default apps`**.
    >1. Under **Web browser**, select **Internet Explorer**, then select **Microsoft Edge**.
    >
    >	!IMAGE[yashjp5m.jpg](instructions286351/yashjp5m.jpg)

1. [] Once authenticated, close the browser window.

1. [] SSMS should automatically select:
    
    - **@lab.CloudSubscription.Name**
    - **@lab.CloudResourceGroup(ResourceGroup1).Name**
    - **@lab.Variable(miName)**

    >[!alert] If it does not find the SQL Managed Instance, you may have to restart the Managed Instance from the Azure portal.

1. [] Select **Sign in...**, under **Sign in to selected SQL Managed Instance**.

1. [] Use the following on the **Connect to Server** window:

    | Item | Value |
    |:--------|:--------|
    | Authentication   | **SQL Server Authentication**   |
    | Login  | **`MILab`**   |
    | Password  | **`@lab.Variable(azurePw)`**   |

1. [] Select **Connect**.

    !IMAGE[bt2wk44c.jpg](instructions286351/bt2wk44c.jpg)

1. [] Select **OK** on the **Sign in** window to close it.

1. [] You'll leave the settings on the **Specify Secondary Replica** step as is. You can check the other tabs for **Endpoints**, **Backup**, and **Link Endpoint**, then select **Next** to proceed.

1. [] All validation results should show **Ready**. Select **Next**.

    !IMAGE[jgt7molx.jpg](instructions286351/jgt7molx.jpg)

    >[!alert] If you receive any errors, try selecting **Re-run validation** near the bottom right.

1. [] Select **Finish** to create the link.

1. [] All entries should show **Success**. Select **Close**.

    !IMAGE[dblw2klz.jpg](instructions286351/dblw2klz.jpg)

===

## 03: View the replicated database

After the link is created, your database is replicated to the secondary replica. Depending on database size and network speed, the database might initially be in a **Restoring...** state on the secondary replica. After initial seeding finishes, the database is restored to the secondary replica and ready for read-only workloads.

1. [] In SSMS's **Object Explorer**, select **SQLVM1**, then select the **refresh icon** on the top controls of that pane.

    !IMAGE[ss8rhzvg.jpg](instructions286351/ss8rhzvg.jpg)

1. [] In **Object Explorer**, expand **Databases**. The Adatum **database** will now be appended with **(Synchronized)**.

    !IMAGE[tzc9fnbe.jpg](instructions286351/tzc9fnbe.jpg)

1. [] In **Object Explorer**, expand **Always On High Availability**, then expand **Availability Groups** to view the distributed availability group for your link.

    !IMAGE[bww45t1b.jpg](instructions286351/bww45t1b.jpg)

1. [] Right-click **AdatumLink (Distributed)**, then select **Show Dashboard**.

    !IMAGE[llmne1go.jpg](instructions286351/llmne1go.jpg)

    !IMAGE[7b74z6ru.jpg](instructions286351/7b74z6ru.jpg)

    >[!knowledge] You can view the dashboard from either replica, which shows the status of the linked database in the distributed availability group.

1. [] Under **Availability replica** on the dashboard, the **Synchronization state** column should show:

    - **Synchronized** for **AG_Adatum**.
    - **Synchronizing** for **AG_Adatum_MI**.

    !IMAGE[yvmautkp.jpg](instructions286351/yvmautkp.jpg)

===

## 04: Transaction log backup

If SQL Server is your initial primary, it's important to take the first [transaction log backup](https://learn.microsoft.com/en-us/sql/relational-databases/backup-restore/back-up-a-transaction-log-sql-server?view=sql-server-ver16) on SQL Server after initial seeding completes, when the database is no longer in the **Restoring...** state on Azure SQL Managed Instance. 

You should take SQL Server transaction log backups regularly to minimize excessive log growth while SQL Server is in the primary role.

1. [] In **Object Explorer**, under **Databases**, right-click the **Adatum (Synchronized)** database, select **Tasks**, then select **Back Up...**.

1. [] In the new window, next to **Backup type**, select **Transaction Log** from the dropdown.

    !IMAGE[te5qxsb6.jpg](instructions286351/te5qxsb6.jpg)

1. [] Under **Destination**, select **Add...**.

    !IMAGE[gxr8jg0b.jpg](instructions286351/gxr8jg0b.jpg)

1. [] Select the ellipses for **File name**.

1. [] Enter **`initial_transaction_log`** for **File name**, then select **OK**.

    !IMAGE[3yu2fr5a.jpg](instructions286351/3yu2fr5a.jpg)

1. [] Select **OK** on the **Select Backup Destination** window.

1. [] Feel free to review the other pages for **Media Options** and **Backup Options** on the leftmost menu. You'll leave everything as default in this lab.

1. [] Select **OK** to run the backup.

    !IMAGE[zf9dz5lw.jpg](instructions286351/zf9dz5lw.jpg)

1. [] Select **OK** on the backup completion dialog.

---

**Congratulations!** You've successfully completed this task.

===

# Task 04: Data sync and cutover

## Introduction

This final task involves performing a planned failover to the Azure SQL Managed Instance. By performing a planned failover, you’ll help Adatum Corporation maintain business continuity and prevent disruptions to their eBook shopping services. This ensures that Adatum Books remains operational even in the event of a failure, providing a seamless experience for their customers.

## Description

In this final exercise, you'll perform a planned failover to the Azure SQL Managed Instance, breaking the link and making the Managed Instance the new primary database.

## Success criteria

-   You performed a planned failover to the Azure SQL Managed Instance.
-   You successfully broke the link and made the Managed Instance the new primary database.

## Learning resources

-   [Overview of the Managed Instance link](https://learn.microsoft.com/en-us/azure/azure-sql/managed-instance/managed-instance-link-feature-overview?view=azuresql)
-   [Configure link with SSMS - Azure SQL Managed Instance](https://learn.microsoft.com/en-us/azure/azure-sql/managed-instance/managed-instance-link-configure-how-to-ssms?view=azuresql)

---

In a production environment, you would typically want to follow these steps for the data migration during a maintenance window:

1.  Stop the workload on the primary SQL Server database so the secondary database on SQL Managed Instance catches up.
2.  Validate all data has made it over to the secondary database on SQL Managed Instance.
3.  Fail over the link to the secondary SQL managed instance by choosing **Planned failover**.
4.  Cut over the application to connect to the SQL managed instance endpoint.

===

## 01: Fail over the Adatum database using SSMS

1. [] In the SSMS **Object Explorer**, right-click on the **Adatum (Synchronized)** database, select **Azure SQL Managed Instance link**, then select **Failover...**.

    !IMAGE[bgnqn3l4.jpg](instructions286351/bgnqn3l4.jpg)

1. [] In the new windows Introduction page, select **Next**.

1. [] **Planned manual failover** will be selected for the failover type. Select **Next**.

1. [] If it launches a browser window, sign in with your lab credentials:

    | Item | Value |
    |:--------|:--------|
    | Username   | `@lab.CloudPortalCredential(User1).Username`   |
    | Password  | `@lab.CloudPortalCredential(User1).Password`   |

1. [] Close the browser window.

1. [] Select **Sign in...** under **Sign in to Managed Instance**.

    !IMAGE[qturpefh.jpg](instructions286351/qturpefh.jpg)

1. [] Use the following on the **Connect to Server** window:

    | Item | Value |
    |:--------|:--------|
    | Authentication   | **SQL Server Authentication**   |
    | Login  | **`MILab`**   |
    | Password  | **`@lab.Variable(azurePw)`**   |

1. [] Select **Connect**.

1. [] Select **Next**.

    !IMAGE[076o3frn.jpg](instructions286351/076o3frn.jpg)

1. [] Select the **I understand** checkbox under **Link removal**, then select **Next**.

    !IMAGE[62b4cmqu.jpg](instructions286351/62b4cmqu.jpg)

    >[!knowledge] Failing over to a SQL Managed Instance stops replication, breaks the link, and drops the distributed availability group.

1. [] On the **Summary** step, review the actions, then select **Finish** when you're ready to fail over the database.

    >[!knowledge] You can select **Script** to generate a script to easily fail over the database using the same link in the future. 

1. [] All entries on the **Results** should show **Success**.

    !IMAGE[6blq708k.jpg](instructions286351/6blq708k.jpg)

1. [] Select **Close** on the window. You'll see that the distributed availability group no longer exists.

    !IMAGE[d40dp3d0.jpg](instructions286351/d40dp3d0.jpg)

===

## 02: Cut over to the SQL Managed Instance

1. [] At the top of SSMS's **Object Explorer**, select **Connect**, then select **Database Engine**.

    !IMAGE[8u3ea1ut.jpg](instructions286351/8u3ea1ut.jpg)

1. [] If it's not already filled out, use the following on the **Connect to Server** window:

    | Item | Value |
    |:--------|:--------|
    | Server name   | **`@lab.Variable(miHost)`**   |
    | Authentication   | **SQL Server Authentication**   |
    | Login  | **`MILab`**   |
    | Password  | **`@lab.Variable(azurePw)`**   |

1. [] Select **Connect**.

1. [] Verify the state of the **Adatum** database in the Managed Instance.

    !IMAGE[gjd1yin0.jpg](instructions286351/gjd1yin0.jpg)

===

# Conclusion

**Congratulations!** You've successfully migrated a SQL Server database to an Azure SQL Managed Instance.

---

In a real-world scenario, after you successfully complete the migration stage, you should go through a series of post-migration tasks to ensure that everything is functioning efficiently.

This phase is crucial for reconciling any data accuracy issues, verifying completeness, and addressing performance issues with the workload.

For more details, review the [Post-migration](https://learn.microsoft.com/en-us/data-migration/sql-server/managed-instance/guide?view=azuresql#post-migration) section of the migration guide.

