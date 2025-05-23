
Student Guide for L200 Copilot Studio

Learning Objectives:

-   Gain HOK (Hands on keyboard) exposure to Copilot Studio.
-   Learn introductory concepts about Copilot Studio and Power Platform.
-   Apply these concepts to a customer scenario.
-   Understand how a Custom Engine Copilot created with Copilot Studio can increase productivity and provide “human-like” functionality.
-   Learn to demonstrate the benefits of RAD tools with AI solutions.
-   (Optional) Demonstrate how AI can be used in a secure way[DM1.1].

===

# Working in the lab environment

---

**The Type Text icon**  
!IMAGE[hut7bsbc.jpg](instructions274352/hut7bsbc.jpg)

The **Type Text** feature used in this lab will send the specified text string to the active window in the virtual machine. Always compare the text in the lab document with the typed text in the virtual machine and verify that the expected text displays.

For larger code blocks, consider using the **Copy** button and then pasting the text by right-clicking or using **CTRL+V** in the virtual machine.

!IMAGE[q1n1yy18.jpg](instructions274352/q1n1yy18.jpg)

---

**Lab credentials**  
The credentials required for accessing the virtual environment and the lab-supplied Microsoft 365 tenant are available at the top of the instructions pane under the **Resources** tab. You can leverage the **Type Text** feature to automatically send the specified username and password to the active window in the virtual machine. Ensure that the credentials are entered correctly by comparing them with the values in the **Resources** tab.

---

**Saving Your progress**  
To save your progress, select **Exit Lab** in the upper-right corner of the screen, then select **Save Progress and Exit**. This will ensure that your work is preserved for future sessions.

>[!alert] Selecting **End Lab** will terminate the lab instance. Don't select this option until you've completed the entire lab.

---

**Note on diagrams**  
All diagrams in the lab instructions are **clickable**. By selecting any diagram, you can open a zoomed view in a separate window for better clarity and analysis.

---

**Split Window feature**  
If you're equipped with multiple screens, you can use the **Split Window** feature to place the lab instructions on a separate screen, making better use of your screen real estate. 

To enable this feature:  
1. Go to the **cogwheel** icon in the upper-right corner.  
2. Select **Split Windows** at the bottom of the **Settings** pane.

This will help you keep the virtual machine and instructions visible simultaneously for a more efficient workflow.

===

## Connection instructions 

1. [] Sign in to the virtual machine with the following credentials:

    | Item | Value |
    |----------|---------|
    | **Username** | Admin |
    | **Password** | +++@lab.VirtualMachine(Win11).Password+++ |

    >[!hint] Select the **+++Type Text+++** icon to enter the associated text into the virtual machine. 

=== 


# Exercise 00: Set up environment and import agentic solution

**Duration**: 20 min

### Task: Create a Copilot Studio sandbox

1. [] Watch the video **TechExcel_CDX_Setup.mp4** and follow the instructions.

    !VIDEO[TechExcel_CDX_Setup_compressed.mp4](instructions294087/TechExcel_CDX_Setup_compressed.mp4)

1. [] Open a browser, go to +++**https://copilotstudio.microsoft.com**+++,  and sign in with the following credentials:

    | Item | Value |
    |----------|---------|
    | **Username** | +++**@lab.CloudCredential(M365).AdministrativeUsername**+++ |
    | **Password** | +++@lab.CloudCredential(M365).AdministrativePassword+++ |

1. [] On the left pane, select the ellipses and then select **Solutions**.

    !IMAGE[solutions.jpg](instructions294087/solutions.jpg)

1. [] On the solutions page, near the top of the page, select **Import solution**.

1. [] On the **Import a solution** flyout, select **Browse**, go to +++**C:\LabFiles**+++, upload the **Bookings_1_0_0_3.zip** and select **Next**.

1. [] Review the details and select **Next**.

1. [] Select **Import**.

    !IMAGE[Import.jpg](instructions294087/Import.jpg)

    >[!alert] If you get an error, use **C:\LabFiles\Fix Bookings Solution.docx**.

1. [] On the solutions page, near the top of the page, select **Publish all customizations**.

    !IMAGE[publishAll.jpg](instructions294087/publishAll.jpg)


===

# Exercise 01: Explore the existing customer app

## Introduction
Before extending the system with AI, Contoso’s team must understand how the current model‑driven app supports property listings and manual bookings. This baseline helps pinpoint the gaps an agentic solution needs to fill.


**Duration**: 15 min

## Task 01: Understand the customer scenario (optional)

## Introduction
Contoso stakeholders need shared context on their booking challenges before proposing technical changes.

## Description
You will read the case study document to capture business drivers, user personas, and success metrics.

## Success criteria
•	Key pain points (busy phone lines, lost bookings) are listed in your notes.
•	Desired business outcomes (shorter wait times, online self service) are articulated.

## Learning resources
 - [Create a customer journey map](https://learn.microsoft.com/en-us/training/modules/create-customer-journey-map/)
 - [Customer Insights](https://learn.microsoft.com/en-us/power-platform/guidance/customer-insights/)

## Key steps

### 01: Read the Case study

1. [] Read the [Case Study for TB Copilot Studio.docx](instructions294087/Case Study for TB Copilot Studio.docx).

    >[!note] Selecting the link above will open the document in a new browser tab outside of the virtual environment.

<br>
<br>
<br>

## Task 02: Examine the present state of the app

## Introduction
Contoso Real Estate has already invested in Microsoft platforms including **M365** and **Power Platform** to rapidly build their app. Their solution includes these components:

-   Model-driven app that can create records for properties and bookings
-   Manual data entry and phone or personal interactions, with much transcription

Contoso reviews its existing Dataverse app to spot manual steps that slow sales reps.

## Description
You will open the Bookings solution, run the model driven app, and create two sample property records.

## Success criteria
•	The Bookings solution opens and the model driven app launches successfully.
•	Two properties (North Offices and South Condo) are saved and visible in the Properties view.
•	You can navigate app tables and confirm data is stored in Dataverse.

## Learning resources 
- [Microsoft Learn: Introduction to model-driven apps](https://learn.microsoft.com/en-us/training/modules/model-driven-apps/)
- [Microsoft Power Platform: Dataverse](https://learn.microsoft.com/en-us/power-platform/admin/dataverse)


## Key steps

### 01:

1. [] Once the customizations are published successfully, select **Bookings**.

    !IMAGE[bookings.jpg](instructions294087/bookings.jpg)

1. [] Explore the existing app contents.

    !IMAGE[qa5r584n.jpg](instructions294087/qa5r584n.jpg)

    >[!hint] 
    >
    <Details><summary>Expand here for help</summary>
    >
    >If you aren’t in **Solutions**, navigate there by going to **Home** \> **Agents** and then select the **Bookings** solution.
    !IMAGE[a9dp32yo.jpg](instructions294087/a9dp32yo.jpg)
    >
    >
    >
    !IMAGE[mutvn8t9.jpg](instructions294087/mutvn8t9.jpg)
    </Details>

1. [] On the left, on the **Objects** pane, select **Apps**.

    <!-- !IMAGE[jgghcwud.jpg](instructions294087/jgghcwud.jpg) -->

1. [] Select the **Command** ellipses and then select **Play** to open the app.

    !IMAGE[play2.jpg](instructions294087/play2.jpg)


    >[!knowledge] The app will open in a Power Apps tab. Your app will only have blank Dataverse tables that you can explore using the left navigation once populated. This will be used by the Sales Representatives.

1. [] Add a real estate property by selecting **+New**, then create an entry with the following information:

    | Default | Value |
    |:---------|:---------|
    | Property Name   | +++**North Offices**+++  |
    | Owner   | If necessary, add your user   |
    | Asking Price   | +++**$200,000.00**+++   |
    | Street   | +++**321 Bellevue Drive**+++   |   
    | City   | +++**Redmond**+++   |
    | Bedrooms   | **3** |  
    | Bathrooms   | **5**   |

    !IMAGE[wx55kaml.jpg](instructions294087/wx55kaml.jpg)
    
1. [] Select **Save & Close**.

1. [] Add another real estate property by selecting **+New**, then create another entry with the following information:

    | Default | Value |
    |:---------|:---------|
    | Property Name   | +++**South Condo**+++  |
    | Owner   | If necessary, add your user   |
    | Asking Price   | +++**$100,000.00**+++   |
    | Street   | +++**123 Sesame Street**+++   |    
    | City   | +++**New York**+++   |
    | Bedrooms   | **2** |  
    | Bathrooms   | **4**   |

    !IMAGE[57rk1sb9.jpg](instructions294087/57rk1sb9.jpg)

1. [] Select **Save & Close**.

!IMAGE[entries.jpg](instructions294087/entries.jpg)

===

# Exercise 02: Explore an agentic solution

## Introduction
Contoso wants to validate that a conversational agent can capture booking requests 24/7, reduce call volume, and integrate with existing data. This exercise lets the team experience and dissect such an agent.

## Objectives
After you complete this exercise, you'll be able to:
•	Demonstrate how a Copilot agent guides customers through booking.
•	Test agent behaviour and trace topic transitions.
•	Map agent logic to underlying Dataverse tables.


**Duration** : 30 min

## Task 01: See how an agent can provide “human-like” customer assistance

## Introduction
Contoso evaluates whether a chatbot can deliver the friendly, on demand service their phone lines cannot.

## Description
Watch a snippet of **AI Skills Fest** to see how a pre-built agent engages with customers, gathers information, identifies real estate properties, and books a viewing appointment.

## Success criteria
•	Video is played end to end.
•	You can summarize how the agent greets, gathers requirements, and confirms a booking.

## Learning resources
- [Microsoft Learn: Introduction to Power Virtual Agents](https://learn.microsoft.com/en-us/training/modules/introduction-power-virtual-agents/)


## Key steps

### 01: Watch the video

!VIDEO[AI_Skills_Fest-Copilot_Studio(condensed).mp4](instructions294087/AI_Skills_Fest-Copilot_Studio(condensed).mp4)

>[!knowledge]Want to see the full session? Watch the complete AI Skills Fest video here !VIDEO[AI_Skills_Fest_-_Copilot_Studio_compressed.mp4](instructions294087/AI_Skills_Fest_-_Copilot_Studio_compressed.mp4)

<br>
<br>
<br>

## Task 02: Explore how an agent works

## Introduction
Contoso’s tech leads inspect agent behaviour to gauge configurability and reliability.

## Description
You will open the Real Estate Copilot in test mode, enable topic tracking, and walk through a booking scenario.

## Success criteria
•	Agent responds to Hello with a welcome message.
•	When prompted with criteria (e.g., 2 bedroom house), the agent returns a matching property.
•	Booking confirmation dialogue completes and appears in the test pane transcript.

## Learning resources
- [Microsoft Learn: Test and publish your bot](https://learn.microsoft.com/en-us/training/modules/test-publish-bot/)


## Key steps

### 01: Test the agent


1. [] Return to the browser tab that is signed into Copilot Studio Solutions.

1. [] On the left, on the **Objects** pane, select **Agents**. 

1. [] Select the **Real Estate Copilot** agent.

    !IMAGE[realEstateCopilot.jpg](instructions294087/realEstateCopilot.jpg)

1. [] On the upper right of the Real Estate Copilot page, select **Test**.

    !IMAGE[test1.jpg](instructions294087/test1.jpg) 

1. [] On the **Test your agent** flyout, select the **More** ellipses and then enable **Track between topics**.

    !IMAGE[trackTopics.jpg](instructions294087/trackTopics.jpg)

    >[!knowledge] Turning on tracking allows you to see how the agent uses different topics based on your keywords.

1. [] In the **Test your agent** prompt, enter the following: 

    ```Prompt
    Hello
    ```

1. [] Observe the response and then enter the following:

    ```Prompt
    Book a real estate showing
    ```

    >**Example Output:**
    >
    !IMAGE[sx1je5s1.jpg](instructions294087/sx1je5s1.jpg)

1. [] Respond to the prompts with your name and email address and then select **Yes** to confirm the details.

    <!-- Enter your *name* and *email address*, then confirm by selecting **yes**
!IMAGE[u6xx9mry.jpg](instructions294087/u6xx9mry.jpg) -->

1. [] Select **House** for the property type and enter +++**2**+++ for the number of bedrooms.
    <!-- !IMAGE[pkywz69w.jpg](instructions294087/pkywz69w.jpg) -->

    >[!note]The agent will search the properties in the back-end Dataverse tables and find one that matches.
    <!-- !IMAGE[lynx4w53.jpg](instructions294087/lynx4w53.jpg) -->

1. [] When asked, **What date and time do you want to see the property?**, enter the following:

    ```Prompt
    tomorrow at 2pm
    ```

    >[!note] After completing the booking, the agent will confirm the details, then ask if you're done and whether you're satisfied.

1. [] Enter **yes** to acknowledge the booking confirmation, but **don’t end the conversation**[DM2.1]. When prompted, select **No** to continue.

   ![oov4gs79.jpg](instructions294087/oov4gs79.jpg)

> [!hint]  
> Want to learn how this agent was created? Explore the [**Exercise – Create and manage topics**](https://learn.microsoft.com/en-us/training/modules/manage-power-virtual-agents-topics/) module on Microsoft Learn for a behind-the-scenes look.
    

<br>
<br>
<br>

## Task 03: Explore the mechanics of the agent
## Introduction
Contoso must ensure the agent’s data layer aligns with existing Dataverse schemas.
## Description
You will review Microsoft Learn content on creating custom tables and relate it to the agent’s property and booking entities.
## Success criteria
•	You identify which custom tables support property and booking data.
•	You can explain how the agent reads from and writes to these tables.


## Learning resources
- [Microsoft Learn: Create custom tables in Dataverse](https://learn.microsoft.com/en-us/training/modules/create-custom-tables-dataverse/)


## Key steps

### 01: Go to Microsoft Learn


1. [] Open the following exercise on Microsoft Learn:  
   [**Exercise – Create custom tables**](https://learn.microsoft.com/en-us/training/modules/create-bots-power-virtual-agents-copilot/exercise-create-tables) and review how custom tables are created and used to support the agent's functionality.

1. [] Proceed to Exercise 03.

===

# Exercise 03: Review how generative AI features complete the agentic solution

## Introduction
To scale personalised conversations, Contoso plans to enrich the agent with generative AI that crafts context aware responses from knowledge sources.

## Objectives
After you complete this exercise, you'll be able to:
•	Explain how generative answers are configured in Copilot Studio.
•	Identify content sources and security considerations for generative AI.
•	Evaluate the impact of generative responses on customer experience.


**Duration**: 15 minutes

# Task 01: Review generative AI configuration
## Introduction
Contoso wants to confirm that the agent’s answers stay accurate and on brand when powered by generative AI.
## Description
You will study the Microsoft Learn module on setting up generative AI and relate its steps to the Real Estate Copilot.
## Success criteria
•	You locate the Generative AI settings in the agent.
•	Knowledge sources are listed and their access permissions confirmed.
•	You can describe how the agent falls back to generative answers when no topic is triggered.

## Learning resources
- [Microsoft Learn: Set up generative AI in Power Virtual Agents](https://learn.microsoft.com/en-us/training/modules/set-up-generative-ai-power-virtual-agents/)



## Key steps

### 01: Go to Microsoft Learn

1. [] Explore the following Microsoft Learn resource:  
[**Exercise – Set up Generative AI**](https://learn.microsoft.com/en-us/training/modules/create-bots-power-virtual-agents-copilot/exercise-generative-ai)

Use this as a reference to understand how generative AI features were applied to improve the agent’s ability to deliver relevant, conversational responses.

<!-- !IMAGE[g2x9unbv.jpg](instructions294087/g2x9unbv.jpg) -->

===

# Congratulations! 