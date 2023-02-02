---

copyright:
  years: 2022, 2023
lastupdated: "2023-02-02"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Tutorial: Customizing the size and position of the web chat
{: #web-chat-develop-size-position}

This tutorial shows how you can change the size and position of the web chat by rendering it in a custom element.
{: shortdesc}

For a complete, working version of the example described in this tutorial, see [Custom elements for {{site.data.keyword.conversationshort}} web chat](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/webchat/examples/custom-element){: external}.
{: note}

By default, the web chat interface on your website is rendered in a host `div` element that is styled to appear in a fixed location on the page. If you want to change the size or position of the web chat, you can specify a custom element as the host location for the web chat. This host element is used as the location for both the main web chat interface and for the web chat launcher (unless you are using a custom launcher).

When you use a custom element, you also take control of showing and hiding the web chat when it is opened or closed (such as when the customer clicks the launcher icon or the minimize button). This gives you the opportunity to apply additional effects, such as opening and closing animations. You can control showing and hiding the main window by using the [addClassName() and removeClassName()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#elements-get-main-window){: external} functions.

To use a custom element, follow these steps:

1. In your website code, define the custom element where you want the web chat to be rendered. There are many ways of doing this, depending on the framework you are using. A simple example is to define an empty HTML element with an ID:

    ```html
    <div id="WebChatContainer"></div>
    ```

1. Get a reference to your custom element so you can reference it in the web chat configuration. To get a reference, use whatever mechanism makes sense for the library you are using. For example, you can save the reference returned from `document.createElement()`, or you can use a query function to look up the element in the DOM. This example looks up the element using the ID we assigned to it:

    ```javascript
    const customElement = document.querySelector('#WebChatContainer');
    ```

1. In the web chat embed script, set the `element` property, specifying the reference to your custom element.

    ```javascript
    window.watsonAssistantChatOptions = {
      integrationID: "YOUR_INTEGRATION_ID",
      region: "YOUR_REGION",
      serviceInstanceID: "YOUR_SERVICE_INSTANCE_ID",
    
      // The important piece.
      element: customElement,
    
      onLoad: function(instance) {
        instance.render();
      }
    };
    ```

1. Make sure that the main web chat window is hidden by default. You can do this in the `onLoad` event handler, after `render` has been called. You must also add handlers to listen for the `window:open` and `window:close` events so the customer can open and close the web chat after the page loads. In our example, we are using a CSS class called `HideWebChat` to do this (see the [full example](https://github.com/watson-developer-cloud/assistant-toolkit/blob/master/integrations/webchat/examples/custom-element/client/javascript-animation/index.html){: example} for the definition of this class):

    ```javascript
    function onLoad(instance) {
      instance.render();
      instance.on({ type: 'window:close', handler: closeHandler });
      instance.on({ type: 'window:open', handler: openHandler });
      instance.elements.getMainWindow().addClassName('HideWebChat');
    }
    ```

1. Create handlers to hide and show the main web chat window in response to the `window:open` and `window:close`. This example simply shows and hides the element; the [full example](https://github.com/watson-developer-cloud/assistant-toolkit/blob/master/integrations/webchat/examples/custom-element/client/javascript-animation/index.html){: example} shows how you can add animation effects.

    ```javascript
    function closeHandler(event, instance) {
      instance.elements.getMainWindow().addClassName('HideWebChat');
    }
    
    function openHandler(event, instance) {
      instance.elements.getMainWindow().removeClassName('HideWebChat');
    }
    ```

For complete working code, see the [Custom elements for {{site.data.keyword.conversationshort}} web chat](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/webchat/examples/custom-element){: external} example.
