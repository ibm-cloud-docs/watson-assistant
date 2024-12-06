---

copyright:
  years: 2023
lastupdated: "2024-12-04"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Integrating with Genesys Audio Connector
{: #deploy-genesys-audioconnector}

[IBM Cloud]{: tag-ibm-cloud}

You can integrate the Genesys Audio Connector with your assistant to stream the conversation audio between the assistant and Genesys Cloud.
{: shortdesc}

## Before you begin
{: #deploy-audioconnector-genesys-setup}

You must have the following prerequisites before you start integrating your assistant with Genesys Audio Connector: 

- A new account or log in to an existing Genesys Cloud account with access to Genesys Architect and the correct region at the [Genesys Cloud portal](https://login.mypurecloud.com/){: external}.
- The `Admin` role in the Genesys Cloud organization.
For more information on Genesys Cloud roles and permissions see, [Roles and permissions overview](https://help.mypurecloud.com/articles/about-roles-permissions/).{: external}

## Create the Audio Connector integration in your assistant
{: #integrate-audio-connector}

1. Go to the **Integrations** page by clicking the integrations icon (![Integrations icon](images/integrations-icon.png)) in the left menu.

Store the credentials because you cannot see them after you click **Save**. You require these credentials to set up the Genesys Audio Connector.{: important}
    
1. Click **Add** on the **Phone** tile.
1. Click **Genesys Audio Connector** tile.
1. In the **Credentials** section, copy and store the automatically generated credentials in the following fields:

    - **API key**
    - **Client secret**
    - **Genesys audio connect URI**
    - **Bot Connector ID**
      
1.  Click **Save and Exit**.

## Set up Audio Connector to integrate assistant
{: #set-up-audio-connector}

To set up Genesys Audio Connector, complete the steps in the [Configure and activate Audio Connector in Genesys Cloud](https://rcstaging.wpengine.com/articles/configure-and-activate-audio-connector-in-genesys-cloud/) topic.

In the Genesys **Admin** page, go to **Integrations** > **Configuration** to add the **Genesys audio connect URI** value that you copied while [creating the Audio Connector integration in your assistant](#integrate-audio-connector).
{: important}

In the Genesys **Admin** page, go to **Integrations** > **Credentials** to add the credentials for the **API key** and **Client secret** fields that you copied while [creating the Audio Connector integration in your assistant](#integrate-audio-connector). 
{: important}


### Call Flow

Use the **Call Audio Connector** action in Genesys to activate the Audio Connector integration in your assistant. 

For more information, see [Call Audio Connector action](https://help.mypurecloud.com/articles/call-audio-connector-action/). 

After getting the Genesys audio connect URI from the **Credentials** section, do the following:

1.  Go to the Genesys Admin page.
1.  Under Architect, click **Architect**, and create an **Inbound Call Flow**.
1.  In the Toolbox, click **Bot**, and then **Call Audio Connector**.
1.  Enter a name for your Call Flow.
1.  Choose your Audio Connector integration from the **Integration** drop-down menu.
1.  You must copy the stored **Bot Connector ID** field of the **Credentials** section and paste it into the **Connector ID** field. `<instance-id>/connect?version=<api-version>`
1.  Enter session variables that you want to be passed to and from {{site.data.keyword.conversationshort}}. For more information, see [Context Sharing through session variables](#deploy-audioconnector-session-variables). 
1.  Click at the bottom of the Flow Diagram to create a Terminating Action. For example, `Disconnect`.
1.  Click **Save** and **Publish**.

### Call Routing

Create a call routing to direct incoming calls to your Genesys Call Flow.

1. Go to the Genesys Admin page.
1. Go to **Call Routing** to create a call routing.
1. Enter a name for your call routing.
1. Choose **Division**.
1. Choose the call flow that you configured in the previous step from the **Route to** drop-down menu.
1. In the call flow, assign the telephone number to which you want to route the call.
1. Click **Create**.
  
## Context-sharing through session variables
{: #deploy-audioconnector-session-variables}

From the Audio Connector node in the Genesys Architect flow, you can specify session variables that can be used to pass information to {{site.data.keyword.conversationshort}}. You can specify both Input and Output parameters. For the integration, both of these parameters are merged into a single object under the  `context`  object.

Both Input and Output parameters are available in the {{site.data.keyword.conversationshort}} `context`, and the information is shared on each turn. For example, the  `context`  made available in {{site.data.keyword.conversationshort}} is:

```json
{
  "context": {
    "integrations": {
      "genesys_audio_connector": {
        "user_id": "<SENT FROM GENESYS>",
        "some_variable": "<SET_FROM_WATSON_ASSISTANT>"
      }
    }
  }
}
```

Access the input parameters in your {{site.data.keyword.conversationshort}} with the ${system_integrations.genesys_audio_connector.user_id} session variable.

To set output parameters, use an expression such as ${system_integrations.genesys_audio_connector.some_variable}, which you can access later in your flow.



Do the following steps to set an output variable:

1. Go to the {{site.data.keyword.conversationshort}}’s actions step, where you want to define the variable.

2. Click **Set new variable** and select **Expression**.

3. Enter the following expression:



${system_integrations.genesys_audio_connector.<variable_name>} = "<variable_value>"



Example:



${system_integrations.genesys_audio_connector.some_variable} = "this is an output variable"



In this example, the variable name is `some_variable`, with the value set to "this is an output variable".




   

## Ending the Genesys Audio Connector flow
{: #deploy-audioconnector-end-flow}

After receiving the audio conversation from the user, the Audio Connector node in Genesys Architect facilitates exchange of messages between the user and assistant until the end of conversation. To send the audio conversation back to Genesys, you must use the  `end_session` response type.

```json
{
  "generic": [
    {
      "response_type": "text",
      "values": [
        {
          "text": "You have ended the call."
        }
      ]
    },
    {
      "response_type": "end_session"
    }
  ]
}
```

## Response types
{: #deploy-audioconnector-response-types}

After integrating your {{site.data.keyword.conversationshort}} with Genesys Audio Connector, you can use the following [response types](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-response-types-reference) in the assistant:

-  text
-  option
-  end_session
-  speech_to_text
-  text_to_speech
-  start_activities
-  stop_activities
-  dtmf
-  user_defined
-  connect_to_agent
-  image
-  audio
