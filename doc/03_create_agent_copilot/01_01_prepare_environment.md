
# Task 01: Set up

### Introduction

Contoso has decided to adopt an AI-driven customer support solution to address increasing customer demands and reduce the workload on customer service representatives. To start implementing this solution, you first need to set up the required environment within the Power Platform. This task involves preparing the necessary foundational components such as Dataverse, enabling you to build the AI-powered agent effectively.

### Description

In this task, you’ll  configure the Power Platform environment by enabling Microsoft Dataverse and deploying sample apps and data. These components provide the essential foundation for creating and deploying intelligent agents with Microsoft Copilot Studio.

### Success criteria

- You navigated to the Power Platform admin center and signed in with the provided Microsoft 365 credentials.

- You selected the correct environment ("Contoso (default)") and enabled Dataverse with sample apps and data.

### Learning resources

## Key Tasks

===

### 01: Set up Power Platform

1.  On your desktop, open Microsoft Edge, then go to aka.ms/ppac
2.  Sign in with your lab credentials:

| Item         | Value                                               |
|--------------|-----------------------------------------------------|
| **Username** | `@lab.CloudCredential(M365).AdministrativeUsername` |
| **Password** | `@lab.CloudCredential(M365).AdministrativePassword` |

1.  On the left service menu, select **Environments**.
2.  Select the **Contoso (default)** environment.

    !IMAGE[v29z5ydm.jpg](instructions289215/v29z5ydm.jpg)

    {: .note }

>   This will retain your Microsoft 365 account identity and carry it over to Power Platform, which is the foundation on which Copilot Studio is built.

>   This is also where Copilot Studio will store data associated with your custom agent.

3.  Select **Add Dataverse** on the top bar.

    !IMAGE[oz23w4q7.jpg](instructions289215/oz23w4q7.jpg)

4.  Select the toggle for **Deploy sample apps and data?** to change to **Yes**, then select **Add** at the bottom.

    !IMAGE[ucvtkdmi.jpg](instructions289215/ucvtkdmi.jpg)

 {: .note }

> You don’t need to wait for this to finish deploying, as we won’t use it until a later exercise.

{: .important }

>   You can also create flows and actions that Copilot can leverage. You can even use Power Platform connectors for your agents to access outside data from customer apps, document sources, and their own databases.

===

### 02: Add on a trial of Copilot Studio

1.  Open a new tab, then go to copilotstudio.microsoft.com

 {: .warning } 
 
 > If prompted for the verification and account creation seen below, try closing the tab and going to the URL again.

  !IMAGE[kpiyl9i3.jpg](instructions289215/kpiyl9i3.jpg)

2.  Select your region, then select **Start free trial**.

  !IMAGE[zmhjr4oy.jpg](instructions289215/zmhjr4oy.jpg)

3.   **Contoso (default)** should already be set as the **Environment**, in the upper right.

  !IMAGE[qkvcytky.jpg](instructions289215/qkvcytky.jpg)

===

### 03: (Optional) Use Power Apps to upload a pre-built agent

 {: .warning } 
> You can **optionally** import an agent to use as a starting point for your lab exercises. This completes all the steps from **Exercise 01** to the end of **Exercise 04**. > You'll need to download and import a custom solution for this.

> If you import a custom solution, please observe all the following steps, regardless, to learn how everything is configured. Also follow along with the various tests of the agent.

1.  Open a new tab, then go to https://github.com/microsoft/TechExcel-Designing-your-own-copilot-using-copilot-studio/blob/main/TechExcel_1_0_0_1.zip
2.  Select the ellipsis near the upper right, then select **Download**.

     !IMAGE[5zn4j733.jpg](instructions289215/5zn4j733.jpg)

3.  Close the tab, open a new tab, then go to make.powerapps.com

 {: .note } 
 > Here you're able to use your new environment, build Power Apps, and inspect the components of your agents.

4.  To import the agent, select **Solutions** in the left menu.

    !IMAGE[kkyg7a31.jpg](instructions289215/kkyg7a31.jpg)

5.  Select **Import solution** on the top bar.

{: .warning } 

> You'll need to wait for the Dataverse database before importing the custom solution.

    !IMAGE[gxqca4j4.jpg](instructions289215/gxqca4j4.jpg)

6.  Select **Browse** in the new pane.
7.  Select the **Downloads** folder, select **TechExcel_1.0.0.1.zip**, then select **Open**.

    !IMAGE[gdzza62m.jpg](instructions289215/gdzza62m.jpg)

8.  Select **Next** at the bottom, then select **Import**.

    !IMAGE[u2a06xbw.jpg](instructions289215/u2a06xbw.jpg)

{: .warning } 

> It may take a few minutes to complete the import of the **TechExcel** agent. You'll see a warning that translated labels could not be imported for this lab environment, which can be ignored.

    !IMAGE[ert510ll.jpg](instructions289215/ert510ll.jpg)

{: .note }

>   This is the definition of the agent, not the running version.

9.  Select **TechExcel** to see the agent and some of the internal components.

