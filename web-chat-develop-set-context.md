---

copyright:
  years: 2022, 2023
lastupdated: "2023-06-07"

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



# Tutorial: Setting context variables for actions from the web chat
{: #web-chat-develop-set-context}

This tutorial shows how you can use the web chat to set the values of context variables that your actions can access.
{: shortdesc}

For a complete, working version of the example described in this tutorial, see [Setting context variables for {{site.data.keyword.conversationshort}} web chat](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/webchat/examples/set-context){: external}.
{: note}

You can use context variables to store information that the assistant uses throughout the conversation.

Context data is maintained throughout the session. The context is sent to the assistant as part of each message, and returned with each response, in an object called `context`. Context variables for actions skills are stored in the following location:

```json
"context": {
  "skills": {
    "action skill": {
      "skill_variables": {
        ...
      }
    }
  }
}
```

Any JSON data can be stored in the `skill_variables` object and read or modified by either the actions or the web chat.

This example shows how you can store the customer's name in a context variable, which you can then use to show a personalized greeting. You can use this same approach to store any other information that your assistant might use. Examples might include the customer's location, an account balance, or stored preferences.

To set the value of a context variable from the web chat, follow these steps:

1. Create a handler for the [`pre:send`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#presend){: external} event. This handler modifies the payload of outgoing message events to assign a value to a context variable called `User_Name`.

    We want to set the user name only once at the beginning of the conversation. This example assumes that the home screen is not enabled, which means that the web chat initiates each new conversation with an empty message to trigger a greeting from the assistant.

    For this example, we are using the hardcoded user name `Cade`. In a production assistant, you might retrieve the customer's name from a user profile on your website.

    ```javascript
    function preSendHandler(event) {
      // Only do this on messages that request the welcome message.
      if (event.data.input && event.data.input.text === '') {
        event.data.context.skills['actions skill'] = event.data.context.skills['actions skill'] || {};
        event.data.context.skills['actions skill'].skill_variables = event.data.context.skills['actions skill'].skill_variables || {};
        event.data.context.skills['actions skill'].skill_variables.User_Name = 'Cade';
      }
    }
    ```

1. In your `onLoad` event handler, use the [`on()`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#on){: external} instance method to subscribe to the `pre:send` event, registering the `preSendHandler()` function as the callback.

    ```javascript
    instance.on({ type: 'pre:send', handler: preSendHandler });
    ```

The assistant actions can now access the `User_Name` variable throughout the conversation.

For complete working code, see the [Setting context variables for {{site.data.keyword.conversationshort}} web chat](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/webchat/examples/set-context){: external} example.

