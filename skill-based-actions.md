---

copyright:
  years: 2025
lastupdated: "2025-01-03"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Creating skill-based actions
{: #skill-based-actions}

Skill-based actions, also known as conversational skill actions, allow assistants to connect and start tasks from third party applications and services. The assistant then can report the status of the task and interact with the user to complete the given task. For more information about skills, see [Overview of apps and skills](https://www.ibm.com/docs/en/watsonx/watson-orchestrate/current?topic=studio-overview-apps-skills) in the watsonx Orchestrate documentation.

Skill-based actions require a provider that connects to {{site.data.keyword.conversationshort}} and provides access to the external application's or service's features. In watsonx Orchestrate, you can find [Pre-built skills and apps](https://www.ibm.com/docs/en/watsonx/watson-orchestrate/current?topic=reference-prebuilt-apps-skills) that allow you to access the functionalities of many services, but you can't register your own application to use it as a skill provider.

In {{site.data.keyword.conversationshort}}, you can use your own application as a skill-based action provider and use them to enhance the user's experience with your assistant, providing access to functions that it would not be able to do otherwise.

## Before you begin

To create your own skill-based actions you must first complete the following requirements:

1. [Implement an API that complies with the API specifications for skill-based action providers](#implementing-api).
1. [Register a skill-based action provider in {{site.data.keyword.conversationshort}}](#registering-provider).

### Implementing the API for the skill-based action provider
{: #implementing-api}

For more information about the API specifications for skill providers, see [Conversational Skills: Masterdoc for API Endpoints to Implement by the Pro-Code Conversational Skill Client](https://github.com/watson-developer-cloud/assistant-toolkit/blob/master/conversational-skills/procode-endpoints.md).

You can also use Java SDK for conversational skills. For more information, see [Conversational Skills: Java-based conversational skill for {{site.data.keyword.conversationshort}}](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/conversational-skills/procode-skill-sdk-java).

### Registering a skill-based action provider
{: #registering-provider}

After you create the endpoints, you must register your skill-based action provider in {{site.data.keyword.conversationshort}}. For more information about how to accomplish that, see [Register a Conversational Skill Provider](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/conversational-skills#register-a-conversational-skill-provider).

If you need more examples of authentication in different schemas, see [Create a conversational skill provider](https://cloud.ibm.com/apidocs/assistant-v2?code=node#createprovider).

## Creating skill-based actions

There are two methods to create a skill-based action in {{site.data.keyword.conversationshort}}. You can create them by using the API or by using the {{site.data.keyword.conversationshort}} user interface. Choose the option that is most suitable to your needs.

### Creating skill-based actions by using the API

To create a skill-based action by using the API, you must first create an OpenAPI specification of the skill that references the endpoints of your skill provider.

You can use any OAS editor or the **watsonx Orchestrate OpenAPI Builder** to complete this task. For more information, see [Building OpenAPI specifications for skills](https://www.ibm.com/docs/en/watsonx/watson-orchestrate/current?topic=skills-building-openapi-specifications) in the watsonx Orchestrate documentation.

After that, you can import the skill by using the [Import skills](https://cloud.ibm.com/apidocs/assistant-v2?code=node#importskills) endpoint in the {{site.data.keyword.conversationshort}} API. When that's done, you can then use the skill in your assistant.

### Creating skills by using the UI

You can also use the {{site.data.keyword.conversationshort}} UI to create the skill-based action.

To create a skill based action from the UI, your skill provider's API must implement the [list conversational skills](https://github.com/watson-developer-cloud/assistant-toolkit/blob/master/conversational-skills/procode-endpoints.md#list-conversational-skills) endpoint.
{: important}

Actions from skills don't support getting input values from other actions or mapping output values to other actions.
{: note}

To create a skill-based action, complete the following steps:

1. In {{site.data.keyword.conversationshort}}, go to **Actions** > **New action** > **Skill-based action**. 

1. In the **Build an action from a skill** page, click the skill to which you want to link the action to, making the skill the foundation to your action. 

    You must connect to the app of the skill for it to appear as an option in this step. For more information, see [Managing connections and connecting to apps](https://www.ibm.com/docs/en/watsonx/watson-orchestrate/current?topic=administering-managing-connections-connecting-apps#connecting-to-apps).{: note} 

1. In the **Name your action** field, enter a name for your action.

1. In the **Add action conditions**, you can add or edit conditions for the action trigger. 

    For more information, see [Adding conditions to an action](https://www.ibm.com/docs/en/watsonx/watson-orchestrate/current?topic=actions-adding-conditions-action){: tip}
    
1. In the **Enter a phrase** field, enter the phrase that customers must type or ask to trigger the skill. For example, `I want to pay my electricity bills`.

1. You use the following options on the upper-right corner of the page to improve the assistant experience:

    - **Action response mode**

        Defines the response mode for your assistant such as **Clarifying** or **Confident**.

    - **Action notes** 

        Opens the **Action notes** window to add a description, documentation, comments, or any other annotations to help you track your work as you build an action.

    - **Action settings**

        Opens the **Action settings** window to enable or disable **Ask clarifying question** and **Change conversation topic** configurations in action.

1. Click the **Save** button to save the action.

Your assistant can now use the newly created action.

## Using skill-based actions

To test and use your skill-based actions, you can start a new conversation with your assistant and follow the conditions that you defined when you created the action. Once you meet the conditions, enter the phrase that triggers the action.

The assistant then attempts to turn that action into a conversation, where you can check the status of the task and interact with the assistant to complete the action successfully.
