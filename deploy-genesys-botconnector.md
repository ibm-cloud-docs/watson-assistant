---

copyright:
  years: 2023
lastupdated: "2023-11-30"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}


# Integrating with Genesys Bot Connector
{: #deploy-genesys-botconnector}

[IBM Cloud]{: tag-ibm-cloud}

Use the Genesys Bot Connector integration to connect your assistant with Genesys.
{: shortdesc}

The Genesys Bot Connector enables Genesys Architect Flow designers to integrate their messaging and conversation flows with any third-party virtual assistant.

## Before you begin
{: #deploy-botconnector-genesys-setup}

You need to create a new account or log in to an existing Genesys Cloud account with access to Genesys Architect and the correct region at the [Genesys Cloud portal](https://login.mypurecloud.com/){: external}.

## Set up Bot Connector in Genesys
{: #deploy-botconnector-genesys-setup}

1. Go to the Genesys Admin page.
1. Under **Integrations**, click **Integrations**.
1. On the Integrations page, click **+Integrations**.
1. Search for Genesys Bot Connector, and click **Install**.

1. In the Details tab, enter a name and any notes for your Bot Connector.

1. Click **Copy the Integration ID**, and save. You need the **Integration ID** to create the {{site.data.keyword.conversationshort}} Genesys Bot Connector integration.

1. In the Configuration tab, under Properties, enter a placeholder **Bot Connector Handle Utterance URI**. You need to come back and update this URI after a {{site.data.keyword.conversationshort}} Genesys Bot Connector integration is created.

1. In the Credentials tab, use **Configure** to create a credential field with **Field Name** as **x-watson-genesys-verification-token** and with **Value** as the secret you set in {{site.data.keyword.conversationshort}}. 
    You need this **value** to create the {{site.data.keyword.conversationshort}} Genesys Bot Connector integration. Copy and keep the **token** and **value**, so you can paste them into the **Verification Token** field when you integrate with {{site.data.keyword.conversationshort}}.

    You **cannot** see these credentials again after clicking Save.
    {: note}

1. Click OK and Save. 

Keep the Genesys web page open in a web browser tab so you can refer to and complete fields as setup progresses.

## Integrate {{site.data.keyword.conversationshort}} with Genesys
{: #deploy-botconnector-assistant-setup}

### Create the Bot Connector integration

1. Go to the {{site.data.keyword.conversationshort}} **Integrations** page by clicking the integrations icon (![Integrations icon](images/integrations-icon.png)) in the left menu.

1. Click **Add** on the **Genesys Bot Connector** tile.

1. Click **Confirm**.

### Connect {{site.data.keyword.conversationshort}} to Genesys

1. From the Genesys site, you need your Genesys OAuth credentials.

    OAuth credentials are on the Genesys Admin page under Integrations > OAuth. You need credentials with Grant Type **Client Credentials** and a role that has BotConnector permissions.

    Copy and keep the following values, so you can paste them into the *Genesys Bot Connector* integration setup page.

    - **Client ID**
    - **Client Secret**

1. Return to the {{site.data.keyword.conversationshort}} *Genesys Bot Connector* integration setup page, and then click **Next**.

1. Enter the required fields, and then click **Next**.

    - **Client ID**
    - **Client Secret**
    - **Verification Token** (token and value from Genesys Bot Connector setup)
    - **Integration ID**
    - **API URI** (the Genesys API server for your region e.g., `https://api.regionxyz.mypurecloud.com`)

For security reasons, the authentication fields are removed from view after initial setup. 
{: note}

### Configure your Genesys Bot Connector 

1. Copy the value generated in the **Webhook URI** field.

1. Go to the Genesys Bot Connector Configuration tab you left open. Under Properties, replace the placeholder *Bot Connector Handle Utterance URI* you entered previously with this **Webhook URI** value.

1. Click **Finish**. 

If a field required for authentication is changed, then all entries in related fields must be filled and validated again.
{: note}

## Chat with the assistant
{: #deploy-botconnector-chat}

To start a chat with the assistant, complete the following steps:

1. Open Genesys Architect, and create an **Inbound Message Flow**.
1. In the Toolbox, click **Bot**, and then **Call Bot Connector**.
1. Select the values:
    - Bot Integration: <Name of the Bot Connector you created earlier>
    - Bot Name: IBM {{site.data.keyword.conversationshort}} Bot Connector
    - Bot Version: 1.0
1. Enter session variables you want to be passed to and from {{site.data.keyword.conversationshort}}. For more information, see [Context Sharing through Session Variables](#deploy-botconnector-branching).
1. Output of the Bot Connector is `Success` or `Failure`. You should branch your Genesys flow upon exit from the Bot Connector according to the output **Intent of the Bot Connector**. For more information, see [Conditioning and Output Branching](#deploy-botconnector-session-variables).

## Context-sharing through session variables
{: #deploy-botconnector-session-variables}

From the Bot Connector node in the Genesys Architect flow, you can specify session variables that can be used to pass information to {{site.data.keyword.conversationshort}}. You can specify both Input and Output parameters. For the integration, both of these parameters are merged into a single object under the `context` object.

Both Input and Output parameters are available in the {{site.data.keyword.conversationshort}} `context`, and the information is shared on each turn. For example, the `context` made available in {{site.data.keyword.conversationshort}} is:

```
{
  "context": {
    "integrations": {
      "genesys_bot_connector": {
        "user_id": "<SENT FROM GENESYS>",
        "some_variable": "<SET_FROM_WATSON_ASSISTANT>"
      }
    }
  }
}
```
For Input parameters, you can access the session variable in {{site.data.keyword.conversationshort}} with `$integrations.genesys_bot_connector.user_id`.

For Output parameters, you can assign the session variables to a state variable in Genesys (e.g., `State.some_variable` and access them later on in your flow).

Variables can be read and set from both Dialog and Action skills.

## Set slot parameters by the {{site.data.keyword.conversationshort}} Bot Connector
{: #deploy-botconnector-slot-parameters}

{{site.data.keyword.conversationshort}} Bot Connector sets the following output parameter based on the last conversation turn when the conversation ends.

| Parameter | Description |
| ---- | ---- |
| `Intent` | {{site.data.keyword.conversationshort}} is set to the recognized intent by Dialog skill as the slot value for the Success intent. |

## Conditioning and output branching
{: #deploy-botconnector-branching}

From Genesys Architect, you can use `Logical` functions to branch out your flow based on the context shared back from {{site.data.keyword.conversationshort}}. For example, {{site.data.keyword.conversationshort}} returns an `Intent` parameter that is saved to `State.Intent`. 

In architect, you can add a `Switch` action to branch out to different scenarios. For example, you can configure a case where `State.Intent == "connect_to_agent"`, and then branch out.

## Ending the Genesys Bot Connector flow
{: #deploy-botconnector-end-flow}

When the conversation reaches the Bot Connector node in Architect, Genesys proxies messages between the user and {{site.data.keyword.conversationshort}}, and continues until the conversation ends. To pass the conversation back to Genesys, you need to use the `connect_to_agent` response type or the `end_session` response type.

```
{
  "output": {
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
}
```

```
{
  "output": {
    "generic": [
      {
        "response_type": "text",
        "values": [
          {
            "text": "Connecting you to an agent."
          }
        ]
      },
      {
        "response_type": "connect_to_agent"
      }
    ]
  }
}
```

## User-defined response type
{: #deploy-botconnector-user-defined}

The `user_defined` response type allows you to pass a custom response back to Genesys. For example, this can be used to pass `Cards` and `Carousels` back to Genesys which do not have a {site.data.keyword.conversationshort} equivalent response type. An example of sending back a `Card` back to Genesys is:

```
{
  "output": {
    "generic": [
      {
        "user_defined": {
          "replyMessages": [
            {
              "type": "Structured",
              "content": [
                {
                  "contentType": "Card",
                  "card": {
                    "title": "Card title",
                    "description": "Card description",
                    "image": "http://www.samplesite.com/photo/1234.jpg",
                    "actions": [
                      {
                        "type": "Link",
                        "text": "Link display text",
                        "url": "http://www.samplesite.com"
                      },
                      {
                        "type": "Postback",
                        "text": "Postback display text",
                        "payload": "Postback text"
                      }
                    ]
                  }
                }
              ]
            }
          ]
        },
        "response_type": "user_defined"
      }
    ]
  }
}
```

## Response types
{: #deploy-botconnector-response-types}

These [response types](/docs/watson-assistant?topic=watson-assistant-response-types-reference) are supported and displayed as expected when your assistant is deployed for the Genesys Bot Connector channel.

- connect_to_agent
- end_session
- option
- text
- user_defined
