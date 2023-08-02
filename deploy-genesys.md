---

copyright:
  years: 2023
lastupdated: "2023-08-02"

subcollection: watson-assistant

---
{{site.data.keyword.attribute-definition-list}}


# Integrating with Genesys Messenger
{: #deploy-genesys}

[IBM Cloud]{: tag-ibm-cloud}

Integrate web chat with a Genesys Cloud service desk solution to provide help and personalize the customer service experience.
{: shortdesc}

Connect Genesys Messenger to your AI-powered assistant with a web chat integration, and customize options as needed. If, in the course of a chat with your assistant, a customer requests contact with someone, you can transfer the conversation directly to a live agent.

Genesys allows your team to assist customers in real time, which increases customer satisfaction. And satisfied customers are happier customers. To learn more about this service desk solution, see the [Genesys website](https://www.genesys.com/){: external}.

## Before you begin
{: #deploy-genesys-prereqs}

You need:

- A Genesys Cloud license, as listed in **Prerequisites** at [Getting started with web messaging](https://help.mypurecloud.com/articles/get-started-with-web-messaging)
- An OAuth provider if only allowing [authenticated users](#deploy-genesys-authenticate) (Optional)

The Watson Assistant web chat integration only supports Genesys Messenger, not the older Genesys web chat widget. 
{: note} 

## Setting up Genesys Messenger with your assistant
{: #deploy-genesys-setup}

Web chat has a built-in integration to Genesys Web Messenger and currently only supports client-side configuration. It is not configured from the {{site.data.keyword.conversationshort}} user interface (UI).

### Configure Messenger
{: #deploy-genesys-configuration}

To define the appearance and behavior of the chat window:

1. Set up a web messenger using the Genesys instructions at [Configure Messenger](https://help.mypurecloud.com/articles/configure-messenger){: external}.

   In **Messenger Configuration > Appearance**, select **Hide** for **Set your Launcher Button Visibility** and select **Off** for **User Interface**.

1. Set **Humanize your Conversation** to **On** if you want the name of the live agent displayed to users (Optional).

1. Enter the **name for your bot** shown to users in the **Bot Name** field, if you are using an architect flow to send messages before a live agent joins the conversation (Optional).

### Deploy Messenger 
{: #deploy-genesys-messenger}

To assign the configuration and generate a snippet to deploy the Messenger to your website, use the Genesys instructions at [Deploy Messenger](https://help.mypurecloud.com/articles/deploy-messenger/){: external}.

### Enable the integration in web chat 
{: #deploy-genesys-integration}

1. Have ready the **script URL, environment, and deployment ID**, all values found in the embed code provided by Genesys.

1. Use the script at [Enabling the integration](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=service-desks-genesys#enabling){: external}.

Your Genesys-powered service desk setup is complete, and customers can chat with your assistant and be connected to live agents. 

## Embed web chat inside Genesys Messenger
{: #deploy-genesys-assistant}

Live agents can better help customers and address their needs and concerns with details from the conversation history.

To embed web chat inside Genesys and give your live agents access to the conversation history, you need to set up an agent app and then create and integrate with an interaction widget (Optional).

### Configure the agent app
{: #deploy-genesys-app}

1. In the **OAuth settings** in Genesys, create a **new OAuth client**.

1. Set the **Grant Type** to **Token Implicit Grant**.

1. Add **https://web-chat.global.assistant.watson.appdomain.cloud/serviceDesks/genesysAgentApp.html?clientID=YOUR_CLIENT_ID&environment=YOUR_ENVIRONMENT** as a redirect URL.

1. Replace **YOUR_CLIENT_ID** with the **OAuth client ID**, and **YOUR_ENVIRONMENT** with the Genesys **environment value** from the embed code. Note that the client ID is unavailable when creating the OAuth client; you need to first create the client, and then add the redirect URL to it.

### Create an interaction widget integration
{: #deploy-genesys-service-desk}

1. Go to the **Integrations** page in Genesys, click the **+Integrations** button, select your integration, and then click **Install**. 

1. Set the **Application URL** to **https://web-chat.global.assistant.watson.appdomain.cloud/serviceDesks/genesysAgentApp.html?clientID=YOUR_CLIENT_ID&environment=YOUR_ENVIRONMENT&conversationID={{pcConversationId}}** 

1. Replace **YOUR_CLIENT_ID** with the **OAuth client ID**, and **YOUR_ENVIRONMENT** with the Genesys **environment value** from the embed code. Note that the **conversationID={{pcConversationId}}** value is correct as is, and Genesys will replace **{{pcConversationId}}** with the current conversation ID when a live agent opens the widget.

1. Assign the integration to the queue that your agents use and to a group that agents belong to. Note that the widget will be availabe to all queues if you don't assign one; and the integration widget will be unavailable to agents if you don't assign a group.

### Enable authenticated users
{: #deploy-genesys-authenticate}

To configure your integration to only allow authenticated users to use Genesys Messenger, see [Authenticated users](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=service-desks-genesys#authenticated-users){: external}.


