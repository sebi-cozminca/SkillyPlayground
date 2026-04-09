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

5.  Enter the following to set up its boundaries and limitations:

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
