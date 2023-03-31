---

copyright:
  years: 2022, 2023
lastupdated: "2023-03-31"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Tutorial: Customizing the greeting action based on the current page
{: #web-chat-develop-custom-action-for-page}

This tutorial shows how you can dynamically customize the greeting action that is triggered by the web chat based on the page the user is currently viewing.
{: shortdesc}

For a complete, working version of the example described in this tutorial, see [Select greeting action for Watson Assistant web chat](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/webchat/examples/select-greeting-action){: external}.
{: note}

If you do not have the home screen enabled, the default behavior when the web chat opens is to send an empty message to the assistant to start the conversation. This empty message triggers the _Greet customer_ action, which typically sends a welcome message.

Rather than starting the conversation with a generic greeting, you might want your users to see a prompt that is specific to the page they are already viewing. For example, if a user has already navigated to a page about credit cards and then opens the web chat, you might want to start the conversation with a message that is specific to credit cards.

Although this example shows how to adapt the text based on the current page, you can use the same basic approach to adapt the text based on any client condition (such as the time of day or the user's geographical location).
{: tip}

To change the greeting action based on the current page the user is viewing, follow these steps:

1. Determine what page the user is currently viewing. Depending on the design of your application, there are various ways to do this, but one simple mechanism is to check the value of a URL query parameter (in this example, `page`):

    ```javascript
    const page = new URLSearchParams(window.location.search).get('page');
    ```

1. Create a handler for the [`pre:send`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#presend){: external} event, which is fired before a message is sent to the assistant. This handler starts by checking the [`is_welcome_request`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#messageextensions){: external} property to determine whether the message being sent is the empty message that starts the conversation by triggering the _Greet customer_ action.
    
    If it is, the handler then checks the currently displayed page, and it replaces the outgoing empty message with a message that will trigger an action that is specific to the page. (This example only shows setting the message to `Credit Cards`, but additional `if` conditions could customize the message for other pages.)

    ```javascript
    function preSendHandler(event) {
      if (event.data.history && event.data.history.is_welcome_request) {
        if (page === 'cards') {
          event.data.input.text = 'Credit Cards';
        }
      }
    }
    ```

1. In your `onLoad` event handler, use the [`once()`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#once){: external} instance method to subscribe to the `pre:send` event, registering the `preSendHandler()` function as the callback. (We can use `once()` instead of `on()` because this handler needs to be called only for the first message in the session.)

    ```javascript
    instance.once({ type: 'pre:send', handler: preSendHandler});
    ```

For complete working code, see the [Select greeting action for {{site.data.keyword.conversationshort}} web chat](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/webchat/examples/select-greeting-action){: external} example.

