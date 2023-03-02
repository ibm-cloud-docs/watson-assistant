---

copyright:
  years: 2022, 2023
lastupdated: "2023-03-03"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Tutorial: Customizing text elements based on the current page
{: #web-chat-develop-size-position}

This tutorial shows how you can dynamically customize the launcher or home screen text based on the page the user is currently viewing.
{: shortdesc}

For a complete, working version of the example described in this tutorial, see [Change launcher and home screen text for {{site.data.keyword.conversationshort}} web chat](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/webchat/examples/change-launcher-and-home-screen-text){: external}.
{: note}

The launcher text and home screen greet the user and suggest what the user might want to do. Rather than showing the same text all the time, you might want to customize this text based on the page on your website the user is currently viewing. For example, instead of a generic greeting, a customer viewing a page about credit cards might see text that is specific to credit card services.

Although this example shows how to adapt the text based on the current page, you can use the same basic approach to adapt the text based on any client condition (such as the time of day or the user's geographical location).
{: tip}

To change the launcher or home screen text elements based on the current page the user is viewing, follow these steps:

1. Determine what page the user is currently viewing. Depending on the design of your application, there are various ways to do this, but one simple mechanism is to check the value of a URL query parameter (in this example, `page`):

    ```javascript
    const page = new URLSearchParams(window.location.search).get('page');
    ```

1. When the web chat is loaded, check this value and conditionally set the text based on which page is being viewed. You can use any condition that makes sense for your application. In this example, we are simply checking the value of the `page` query parameter:

    ```javascript
    if (page === 'cards') {
      // Update the launcher and home screen with text that is
      // specific to credit cards.
      ...
    } else if (page === 'account') {
      // Update the launcher and home screen with text that is
      // specific to the user's account.
      ...
    }
    ```
    {: codeblock}

1. Change the launcher text using the [`updateLauncherGreetingMessage()`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateLauncherGreetingMessage){: external} instance method. This changes the text that is displayed on the launcher (by default  after 15 seconds).

    ```javascript
    instance.updateLauncherGreetingMessage("I see you're interested in credit     cards! Let me know if I can help.");
    ```

4. Change the home screen configuration using the [`updateHomeScreenConfig()`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#homescreen){: external} instance method:

    - Make sure the home screen is enabled.

    - Change the greeting based on the page the user is viewing.

    - Configure the buttons shown by the home screen so they offer options that are appropriate for the page the user is viewing.

    ```javascript
    instance.updateHomeScreenConfig({
      is_on: true,
      greeting: 'What can I tell you about credit cards?',
      starters: {
        is_on: true,
        buttons: [
          { label: 'Card interest rates' },
          { label: 'Cards with rewards' },
          { label: 'Business cards' }
        ]
      }
    });
    ```

For complete working code, see the [Change launcher and home screen text for {{site.data.keyword.conversationshort}} web chat](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/webchat/examples/change-launcher-and-home-screen-text){: external} example.

