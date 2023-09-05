---

copyright:
  years: 2022, 2023
lastupdated: "2023-09-05"

keywords: web chat interaction, custom responses

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Tutorial: Interacting with the host web page
{: #web-chat-develop-page-interaction}

You can use custom responses and events to enable the web chat to interact with the web page where it appears.
{: shortdesc}

For example, customers might use your assistant to find information they need to complete a form. Rather than expecting the customer to then copy this information manually to the form, you can have the web chat automatically complete the information.

For a complete, working version of the example in this tutorial, see [Page interactions for {{site.data.keyword.conversationshort}} web chat](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/webchat/examples/page-interaction){: external}.
{: note}

This example uses a custom response to render a button in the web chat that populates a form field with the customer's account number:

1. Create a handler for the [`customResponse`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#customresponse){: external} event. This handler renders a custom button and creates a click handler for it. The click handler uses the `Document.querySelector()` method to interact with the DOM and complete a form field with the customer's account number.

    This example uses the hardcoded account number `1234567`. In a typical production assistant, your assistant would retrieve this value from a session variable or query it from an external system.
    {: note}

    ```javascript
    function customResponseHandler(event) {
      const { element } = event.data;

      const button = document.createElement('button');
      button.type = 'button';
      button.innerHTML = 'Enter account number';
      button.addEventListener('click', () => {
        // Look for the account number element in the document, and enter the account number.
        document.querySelector('#account-number').value = '1234567';
      });

      element.appendChild(button);
    }
    ```

1. In your `onLoad` event handler, use the [`on()`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#on){: external} instance method to subscribe to the `customResponse` event, registering the handler as the callback. This enables the assistant to send a custom response that displays the button for filling in the account number.

    ```javascript
    instance.on({
      type: 'customResponse',
      handler: (event, instance) => {
        const { message } = event.data;
        if (message.user_defined && 
            message.user_defined.user_defined_type === 'fill_account_number') {
              accountNumberResponseHandler(event, instance);
            }
      },
    });
    ```

    In this example, we are checking the custom `user_defined_type` property of the custom response and calling the `accountNumberResponseHandler()` function only if the specified type is `fill_account_number`. This is an optional check that shows how you might use a custom property to define multiple different custom responses (each with a different value for `user_defined_type`).
    {: note}

For complete working code, see the [Page interactions for {{site.data.keyword.conversationshort}} web chat](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/webchat/examples/page-interaction){: external} example.

