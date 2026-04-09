
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

    {:.note}

>   This will retain your Microsoft 365 account identity and carry it over to Power Platform, which is the foundation on which Copilot Studio is built.

>   This is also where Copilot Studio will store data associated with your custom agent.

3.  Select **Add Dataverse** on the top bar.

    !IMAGE[oz23w4q7.jpg](instructions289215/oz23w4q7.jpg)

4.  Select the toggle for **Deploy sample apps and data?** to change to **Yes**, then select **Add** at the bottom.

    !IMAGE[ucvtkdmi.jpg](instructions289215/ucvtkdmi.jpg)

>   [!note] You don’t need to wait for this to finish deploying, as we won’t use it until a later exercise.

{: .important }

>   You can also create flows and actions that Copilot can leverage. You can even use Power Platform connectors for your agents to access outside data from customer apps, document sources, and their own databases.

===

### 02: Add on a trial of Copilot Studio

1.  Open a new tab, then go to copilotstudio.microsoft.com

>   [!alert] If prompted for the verification and account creation seen below, try closing the tab and going to the URL again.

>   !IMAGE[kpiyl9i3.jpg](instructions289215/kpiyl9i3.jpg)

2.  Select your region, then select **Start free trial**.

    !IMAGE[zmhjr4oy.jpg](instructions289215/zmhjr4oy.jpg)

3.   **Contoso (default)** should already be set as the **Environment**, in the upper right.

    !IMAGE[qkvcytky.jpg](instructions289215/qkvcytky.jpg)

===

### 03: (Optional) Use Power Apps to upload a pre-built agent

>   [!alert] You can **optionally** import an agent to use as a starting point for your lab exercises. This completes all the steps from **Exercise 01** to the end of **Exercise 04**. You'll need to download and import a custom solution for this.

>   If you import a custom solution, please observe all the following steps, regardless, to learn how everything is configured. Also follow along with the various tests of the agent.

1.  Open a new tab, then go to https://github.com/microsoft/TechExcel-Designing-your-own-copilot-using-copilot-studio/blob/main/TechExcel_1_0_0_1.zip
2.  Select the ellipsis near the upper right, then select **Download**.

    !IMAGE[5zn4j733.jpg](instructions289215/5zn4j733.jpg)

3.  Close the tab, open a new tab, then go to make.powerapps.com

>   [!note] Here you're able to use your new environment, build Power Apps, and inspect the components of your agents.

4.  To import the agent, select **Solutions** in the left menu.

    !IMAGE[kkyg7a31.jpg](instructions289215/kkyg7a31.jpg)

5.  Select **Import solution** on the top bar.

>   [!alert] You'll need to wait for the Dataverse database before importing the custom solution.

!IMAGE[gxqca4j4.jpg](instructions289215/gxqca4j4.jpg)

6.  Select **Browse** in the new pane.
7.  Select the **Downloads** folder, select **TechExcel_1.0.0.1.zip**, then select **Open**.

    !IMAGE[gdzza62m.jpg](instructions289215/gdzza62m.jpg)

8.  Select **Next** at the bottom, then select **Import**.

    !IMAGE[u2a06xbw.jpg](instructions289215/u2a06xbw.jpg)

>   [!alert] It may take a few minutes to complete the import of the **TechExcel** agent. You'll see a warning that translated labels could not be imported for this lab environment, which can be ignored.

!IMAGE[ert510ll.jpg](instructions289215/ert510ll.jpg)

{: .note }

>   This is the definition of the agent, not the running version.

9.  Select **TechExcel** to see the agent and some of the internal components.

===

# Task 02: Create an agent

## Introduction

With the Power Platform environment prepared, your next step is to create an AI-powered customer support agent for Contoso. This task involves defining the agent’s purpose, customizing its tone and limitations, and specifying external knowledge sources. Completing these steps ensures the agent is tailored to Contoso’s specific support scenarios and customer interactions.

## Description

In this task, you’ll use Microsoft Copilot Studio to define and create your first AI-driven agent. You’ll specify the agent's purpose, tone, conversational boundaries, and data sources, preparing it for initial testing.

## Success criteria

- An agent is created within Microsoft Copilot Studio.

- Agent’s purpose, tone, and boundaries are clearly defined.

- External knowledge sources are successfully integrated.

## Learning resources

## Key tasks

### 01: Create an agent

1.  In your Copilot Studio tab, in the text box at the top for **Describe your agent to create it**, enter the following prompt, then select **Enter**:

    `I want to create an agent for my customer support. It is an assistant for Contoso customers, helping to answer common questions and helping with common tasks, like checking order status.`

    !IMAGE[1dhwk23c.jpg](instructions289215/1dhwk23c.jpg)

    {: .note }

>   You'll be redirected to a conversational experience to further customize your agent.

{: .warning }

>   If prompted to wait before submitting your request, please wait a few moments and try again. If the issue persists, expand the dropdown menu below for additional instructions on manually creating your agent.

1.  On the leftmost pane, select **Create**.  
    ![Image](../../media/ue5muwz3.jpg)
    1.  On the **Create** page, select **New copilot**.  
        ![Image](../../media/w2iqhavl.jpg)
    2.  In the upper-right corner of the page , select **Create**.
    3.  In the upper-right corner of the page, select **Skip to configure**.  
        ![Image](../../media/19qclsql.jpg)
    4.  In the upper-right corner of the page, select **Create**.
    5.  In the upper-right corner of the page, select **Settings**.  
        ![Image](../../media/s7o1tl2a.jpg)
    6.  On the **Settings** pane, select **✨ Generative AI**.
    7.  Under **How should your copilot interact with people?**, select **Generative**, then select **Save**.  
        ![Image](../../media/2e5brk5b.jpg)
    8.  Proceed to the next task.
2.  In response to the agent name suggested, enter `OK` .

    !IMAGE[wkx9v9tu.jpg](instructions289215/wkx9v9tu.jpg)

>   [!alert] Note that the following steps may be in a different order for you, as the responses will vary. It may not even ask some of the questions. Be sure to answer all of the prompts, regardless of the order.

3.  If asked, confirm the agent's main purpose, or enter the following again:

    `It is an assistant for Contoso customers, helping to answer common questions and helping with common tasks, like checking order status.`

4.  Enter the following to set up the agent’s tone:

    `Playful tone, joyful, customer focused, but definitely professional.`

5. Enter the following to set up its boundaries and limitations:

    `We don't want to discuss other brands like Fabrikam. Never provide product comparisons with competitor technologies.`

6.  Enter the following prompt to set up publicly accessible data sources:

    `Information should come from https://learn.microsoft.com/en-us/microsoft-copilot-studio/ and from https://www.microsoft.com/en-us/microsoft-copilot/.`

7.  In the right pane, under **Get its knowledge**, select the checkboxes for confirming both URLs.

    !IMAGE[dbpeoa8h.jpg](instructions289215/dbpeoa8h.jpg)

8.  Select the ellipsis in the upper-right , then select **Edit advanced settings**.

    !IMAGE[88yefy53.jpg](instructions289215/88yefy53.jpg)

9.  In the **Advanced Settings** window, under **Schema Name**, enter `ContosoCopilot@lab.LabInstance.Id`, then select **Save**.

    !IMAGE[x087dj1y.jpg](instructions289215/x087dj1y.jpg)

    {: .important }

>   Contrary to the agent’s display name, the schema name is a technical property that can't be changed afterwards and must be unique.

10. Select **Create** in the upper-right corner of the window.

    !IMAGE[hliew081.jpg](instructions289215/hliew081.jpg)

{: .important }

>   You can also choose to avoid the conversational creation experience by selecting **Skip to configure**. You can set the agent’s primary language in the **Edit language** menu. For the lab, be sure to remain in English (en-US). It’s a best practice to always configure your agent in the context of your own solution and publisher, so that the agent is created with the desired publisher prefix, and so you can easily export the agent and deploy it to other environments.
