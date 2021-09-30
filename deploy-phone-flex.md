---

copyright:
  years: 2021
lastupdated: "2021-09-24"

subcollection: watson-assistant

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:deprecated: .deprecated}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:preview: .preview}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:video: .video}

{{site.data.content.classiclink}}

# Integrating with phone and Twilio Flex
{: #deploy-phone-flex}

You can use the phone integration to help your customers over the phone and transfer them to live agents inside of Twilio Flex. If, in the course of a conversation with your assistant, a customer asks to speak to a person, you can transfer the conversation directly to a Twilio Flex agent.

## Before you begin

To use this integration pattern, make sure you have the following:

- {{site.data.keyword.conversationshort}} Plus or Enterprise Plan (required for phone integration)
- A Twilio account with the following products:
    - Twilio Flex
    - Twilio Voice with Programmable Voice API
    - Twilio Studio

## Adding the {{site.data.keyword.conversationshort}} phone integration

If you have not already added the phone integration to your assistant, follow these steps:

1. From the Assistants page, click to open the assistant tile that you want to deploy.

1. From the Integrations section, click **Add integration**.

1. Click **Phone**.

1. Click **Create**.

1. Click **Close**.

For now, this is all you need to do. For more information about configuring the phone integration, see [Integrating with phone](/docs/watson-assistant?topic=watson-assistant-deploy-phone).

## Adding the Twilio Flex Project

If you don't already have a Twilio Flex project, you can create one by following these steps:

1. From the project drop-down menu, click **Create New Project**. Specify a name for the project and verify your account information.

1. On the welcome page, select Flex as the Twilio product for your new project. Fill out the questionnaire and then click **Get Started with Twilio**.

    After your Flex project has been provisioned, return to the [Twilio console](https://www.twilio.com/console){: external}. Make sure you have selected the correct project from the drop-down list.

1. In the navigation menu, click the **All Products & Services** icon.

1. Click **Twilio Programmable Voice > Settings > General**.

1. Under **Enhanced Programmable SIP Features**, toggle the switch to **Enabled**.

## Creating the call flow

After you have your phone integration and Twilio Flex project configured, you must create a call flow with Twilio Studio and provision (or port) the phone number you want your assistant to work with.

To create the call flow:

1. In the navigation menu, click the **All Products & Services** icon.

1. Click **Studio**.

1. Click **+** to create a new flow.

1. Name the new flow and then click **Next**.

1. Select **Start From Scratch** and then click **Next**.

1. Click the **Trigger** widget.

1. Make note of the value from the **WEBHOOK URL** field. You will need this value in a subsequent step.


## Configuring the phone number

1. In the navigation menu, click the **All Products & Services** icon.

1. Click **Phone Numbers**.

1. Under **Manage Numbers**, configure the phone number you want your assistant to use. Select **Buy a Number** to buy a new number, or **Port & Host** to port an existing phone number.

1. In the **Active Numbers** list, click the new phone number.

1. Under **Voice and Fax**, configure the following settings:

    - For **CONFIGURE WITH** field, select **Webhook, TwiML Bins, Functions, Studio, or Proxy**.

    - For **A CALL COMES IN**, select **Studio Flow**. Select your flow from the drop-down list.

    - For **PRIMARY HANDLER FAILS**, select **Studio Flow**. Select your flow from the drop-down list.

1. Go to the {{site.data.keyword.conversationshort}} user interface, open the phone integration settings for your assistant.

1. In the **Phone number** field, type the phone number you configured in Flex Studio.

1. Click **Save and exit**.

## Creating a Twilio function to handle incoming calls
{: #twilio-function-incoming-calls}

Now we need to configure the call flow to direct inbound calls to the assistant using a Twilio function. Follow these steps:

1. In the navigation menu, click the **All Products & Services** icon.

1. Click **Functions**.

1. Click **Create Service**. Specify a service name and then click **Next**.

1. Click **Add** > **Add Function** to add a new function to your service. Name the new function `/receive-call`.

1. Replace the template in your `/receive-call` function with the following code:

    ```javascript
    exports.handler = function(context, event, callback) {
      const VoiceResponse = require('twilio').twiml.VoiceResponse;  
      const response = new VoiceResponse();
      const dial = response.dial({
        answerOnBridge: "true",
        referUrl: "/refer-handler"
      });
      const calledPhoneNumber = event.Called;
      dial.sip(`sip:${calledPhoneNumber}@{sip_uri_hostname};secure=true`);  
      return callback(null, response);
    }
    ```

    Replace `{sip_uri_hostname}` with the hostname portion of your  assistant's phone integration SIP URI (everything that comes after `sips:`).. Note that Twilio does not support `SIPS` URIs, but does support secure SIP trunking by appending `;secure=true` to the SIP URI.

1. Click **Save**.

1. Click **Deploy All**.

1. Click the "Copy URL" link on the bottom-right to copy the Twilio Function URL, you will need this URL when setting up the Studio Flow in a later step.

## Creating a Twilio function to handle transfers from assistant

1. On the Twilio Functions page, click **Add** > **Add Function** to add another new function to your service. Name this new function `/refer-handler`.

1. Replace the template in your `/refer-handler` function with the following code:

    ```javascript
    exports.handler = function(context, event, callback) {
      const VoiceResponse = require('twilio').twiml.VoiceResponse;
      
      const STUDIO_WEBHOOK_URL = '{webhook_url}';
      
      let studioWebhookReturnUrl = `${STUDIO_WEBHOOK_URL}?FlowEvent=return`;
      
      const response = new VoiceResponse();
      console.log("ReferTransferTarget: " + event.ReferTransferTarget);
      
      const referToSipUriHeaders = event.ReferTransferTarget.split("?")[1];
      
      if (referToSipUriHeaders) {
        const sanitizedReferToSipUriHeaders = referToSipUriHeaders.replace(">", "");
        console.log("Custom Headers: " + sanitizedReferToSipUriHeaders);
        
        const sipHeadersList = sanitizedReferToSipUriHeaders.split("&");
        
        const sipHeaders = {};
        for (const sipHeaderSet of sipHeadersList) {
          const [name, value] = sipHeaderSet.split('=');
          sipHeaders[name] = value;
        }

        // Find session history key
        const HEADER_X_WATSON_ASSISTANT_SESSION_HISTORY_KEY = 'X-Watson-Assistant-Session-History-Key';

        const sessionHistoryKey = sipHeaders[HEADER_X_WATSON_ASSISTANT_SESSION_HISTORY_KEY];
        
        studioWebhookReturnUrl = `${studioWebhookReturnUrl}&SessionHistoryKey=${sessionHistoryKey}`;
      }

      response.redirect(
        { method: 'POST' },
        studioWebhookReturnUrl
      );

      // This callback is what is returned in response to this function being invoked.
      // It's really important! E.g. you might respond with TWiML here for a voice or SMS response.
      // Or you might return JSON data to a studio flow. Don't forget it!
      return callback(null, response);
    }
    ```

    Replace `{webhook_url}` with the **WEBHOOK URL** value you copied from the **Trigger** widget in your Studio Flow.

1. Click **Save**.

1. Click **Deploy All**.

## Modify your Twilio Studio Flow to redirect calls to {{site.data.keyword.conversationshort}}

Configure the Twilio Studio flow to redirect the call to your assistant:

1. In your Studio Flow, create a **TwiML Redirect** widget by dragging one onto your canvas from the widget library.

1. Click on your **TwiML Redirect** widget and configure the following settings:
   - For **WIDGET NAME**, type `redirect_to_watson`.
   - For **URL**, paste in the URL copied from your Twilio `/receive-call` function created in [Creating a Twilio function to handle incoming calls](#twilio-function-incoming-calls).

## Modify your Twilio Studio Flow to handle transfers from Assistant

Configure the call flow to handle calls being transferred from the assistant back to Twilio Flex, for cases when when customers ask to speak to an agent:

1. In Twilio Flex, create the appropriate task routing for handling your calls. For more information, see the Twilio Flex [documentation](https://www.twilio.com/docs/flex/quickstart/flex-routing-skills){: external}.

1. In your Studio Flow, create an **Enqueue Call** widget by dragging one onto your canvas from the widget library.

1. For your **Enqueue Call** widget, configure the following settings:

    - For **QUEUE OR TASKROUTER TASK**, select the task router you created.
    - For **TASK ROUTER WORKSPACE**, select the task router you created.
    - For **TASK ROUTER WORKFLOW**, select the routing location you want your assistant to transfer calls to.
    - For **TASK ATTRIBUTES (JSON)**, add the following JSON content that will pass along the SessionHistoryKey in order for agents to access the conversational history of the caller with Watson Assistant.

      ```json
      { "sessionHistoryKey":"{{widgets.redirect_to_watson.SessionHistoryKey}}"}
      ```
    You can leave the other fields blank for now.

1. Connect the Return point from your **TWIML REDIRECT** widget to your **ENQUEUE CALL** widget.

## Configuring the assistant to transfer calls to Twilio Flex

Now we need to configure the assistant to transfer calls to Twilio Flex when a customer asks to speak to an agent. Follow these steps:

1. In the {{site.data.keyword.conversationshort}} user interface, open the dialog skill of your assistant.

1. Add a node with the condition you want to trigger your assistant to transfer customers to an agent.

1. Add a *Connect To Agent* response, and specify the text you want your assistant to say to your customers before it transfers them to an agent.

1. Open the JSON editor for the response.

1. In the JSON editor, modify the `connect_to_agent` response type, specify a transfer target in `transfer_info.target` as `service_desk`, and add the following `sip` configuration items:

```json
{
  "output": {
    "generic": [
      {
          "response_type": "connect_to_agent",
          "transfer_info": {
            "target": {
              "service_desk": {
                "sip": {
                  "uri": "sip:queue@flex.twilio.com",
                  "transfer_headers_send_method": "refer_to_header"
                }
              }
            }
          },
          "agent_available": {
            "message": "Ok, I'm transferring you to an agent"
          },
          "agent_unavailable": {
            "message": ""
          }
      }
    ]
  }
}
```

## Test your assistant

Your assistant should now be able to answer phone calls to your phone number and transfer calls to an agent using Twilio Flex. To test your assistant:

1. In the Twilio console navigation menu, click the **All Products & Services** icon.

1. Click **Flex**.

1. On the Flex Overview page, click **Launch Flex**.

1. Set your agent status as **Available**.

    Your agent profile must be configured to include the required skills for the call to be routed from your assistant.
    {: note}

1. Call your phone number. When the assistant responds, ask for an agent.

1. In the Twilio Flex agent dashboard, accept the incoming call.
