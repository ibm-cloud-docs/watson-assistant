---

copyright:
  years: 2019, 2022
lastupdated: "2022-08-26"

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



# Adding the web chat to your mobile application
{: #web-chat-develop-mobile}

If you have a mobile application built on a mobile framework such as iOS, Android, or React Native, you can use a WebView with a JavaScript bridge to communicate between your app and the {{site.data.keyword.conversationshort}} web chat.
{: shortdesc}

Using WebViews with a JavaScript bridge is a common pattern with a similar implementation for all mobile frameworks.

## Including the web chat as a WebView
{: #web-chat-develop-mobile-webview}

You can include the web chat interface as part of a page of your mobile app, or as a separate panel that your app opens. In either case, you must host an HTML page that includes the web chat embed script, and then include that page as a WebView in your app.

In the embed script, use the `showLauncher` option to hide the web chat launcher icon, and the `openChatByDefault` option to open the web chat automatically when the page loads. In most cases, you will also want to use the `hideCloseButton` option and use the native controls of your app to control how the web chat page or panel closes. For more information about the configuration options you can specify in the embed script, see the [Web chat API reference](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration){: external}.

The following example shows an embed script that includes these configuration options:

```html
<html>
  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1" />
  </head>
  <body>
    <script>
      window.watsonAssistantChatOptions = {
        // A UUID like '1d7e34d5-3952-4b86-90eb-7c7232b9b540' included in the embed code provided in Watson Assistant.
        integrationID: "YOUR_INTEGRATION_ID",
        // Your assistants region e.g. 'us-south', 'us-east', 'jp-tok' 'au-syd', 'eu-gb', 'eu-de', etc.
        region: "YOUR_REGION",
        // A UUID like '6435434b-b3e1-4f70-8eff-7149d43d938b' included in the embed code provided in Watson Assistant.
        serviceInstanceID: "YOUR_SERVICE_INSTANCE_ID",
        // The callback function that is called after the widget instance has been created.
        onLoad: function(instance) {
          instance.render();
        },
        showLauncher: false, // Hide the web chat launcher, you will open the WebView from your mobile application
        openChatByDefault: true, // When the web chat WebView is opened, the web chat will already be open and ready to go.
        hideCloseButton: true // And the web chat will not show a close button, instead relying on the controls to close the WebView
      };
      setTimeout(function(){const t=document.createElement('script');t.src="https://web-chat.global.assistant.watson.appdomain.cloud/versions/" + (window.watsonAssistantChatOptions.clientVersion || 'latest') + "/WatsonAssistantChatEntry.js";document.head.appendChild(t);});
    </script>
  </body>
</html>
```

In your app, make sure you include logic to hide your web chat launching mechanism when the device is offline. If the device goes offline in the middle of a conversation, appropriate error messages and retries occur.
{: note}

## Using a JavaScript bridge
{: #web-chat-develop-mobile-bridge}

In some situations, your mobile application might need to communicate with the {{site.data.keyword.conversationshort}} web chat. For example, you might need to set initial context data (such as a user ID or account information) or use the web chat security feature. To do this, you can use a JavaScript bridge.

A JavaScript bridge is a common pattern that can be used on all mobile platforms. Implementation details differ from one mobile application framework to another; you can find specific examples on how to implement a JavaScript bridge for the framework you are using. However, the core concept of sending events back and forth between the mobile app and the web chat apply to all frameworks.

With a JavaScript bridge, events are sent between the mobile app and the WebView, and event listeners exist on both sides of the bridge to handle those events. Each event carries a message payload; because this payload is text-only, you must stringify and parse JSON objects to pass data back and forth.

If your mobile application needs to call a web chat instance method, you must call the method by sending an event from the app to the WebView using the JavaScript bridge. Similarly, if you need to run code in your mobile application in response to behavior in the web chat, you can send an event through the JavaScript bridge from the web chat to your mobile application.

You can make use of the `user_defined` response type and the `customResponse` event to drive behavior on your mobile application. However, you must strip the `event.data.element` property from the event before you pass it through the JavaScript bridge. Removing this property is necessary because it contains an HTML element, which cannot be stringified. Any use of the `user_defined` response type to write new views into the web chat must be written in HTML and JavaScript and handled inside the WebView. (For more information about the `customResponse` event, see the [Web chat API reference](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#customresponse){: external}.)

