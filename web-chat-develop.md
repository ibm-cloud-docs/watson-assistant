---

copyright:
  years: 2019, 2023
lastupdated: "2023-03-10"

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

# Web chat development overview
{: #web-chat-develop}

If you are comfortable with JavaScript code, you can customize and extend the web chat by using the web chat API. You can also use a WebView to embed the web chat in your mobile app.
{: shortdesc}

For detailed reference information about the web chat API, see the web chat [developer documentation](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=){: external}.
{: tip}

To add the web chat widget to your website or a WebView in your mobile app, all you need to do is embed a generated script element in your HTML source (for more information about the embed script, see [Embedding the web chat on your page](/docs/watson-assistant?topic=watson-assistant-deploy-web-chat)). Within this embed script, you can use the web chat API to customize or extend the web chat.

The web chat API consists of several components:

- **Configuration object**: The embed script defines a configuration object named `watsonAssistantChatOptions`, which specifies configuration objects for the web chat widget. By editing the configuration object, you can customize the appearance and behavior of the web chat before it is rendered. For more information about the available configuration options, see [Configuration options object](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#configurationobject){: external} in the web API reference.
- **Instance methods**: The web chat instance methods provide low-level control of the web chat widget. You can use the instance methods to implement custom behavior such as changing how the web chat widget opens, showing and hiding content, and setting identity information. For more information about the available instance methods, see [List of methods and properties](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#listofmethods){: external} in the web chat API reference.
- **Events**: The web chat event system makes it possible for your website to respond to web chat events (such as opening or closing the web chat window, sending or receiving messages). By subscribing to events, you can implement custom behavior or even intercept and modify message content. For more information about the event system, see [Events](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events){: external} in the web chat API reference.

If you want to use the web chat API to customize your web chat implementation, you don't have to start from scratch. Tutorials are available that show examples of common web chat customizations. For more information, see [Web chat development tutorials](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-tutorials).
{: tip}

## Development tasks
{: #web-chat-develop-tasks}

You can use the web chat API to customize and extend the web chat in the following ways.

Web chat style and content
:   - [Customizing the look of the web chat](#look)
    - [Customizing the home screen](#home-screen)
    - [Customizing strings](#strings)
    - [Supporting global audiences](#global-audiences)

Opening, closing, and rendering the web chat window
:   - [Replacing the default launcher](#replace-launcher)
    - [Keeping the web chat always open](#keep-open)
    - [Changing where the web chat renders](#custom-element)
    - [Adding the web chat to your mobile application](#mobile)

Customizing the conversation
:   - [Intercepting and modifying messages](#modify-messages)
    - [Rendering custom response types](#custom-response-types)
    - [Implementing a contact center integration](#contact-center)

Managing data
:   - [Managing user identity information](#user-id)

Security and administration
:   - [Securing the web chat](#secure-web-chat)
    - [Controlling the web chat version](#web-chat-version)

### Web chat style and content
{: #web-chat-develop-style}

Customizing the look of the web chat {: #look}
:   You can customize the style and appearance of the web chat beyond the options that are available from the **Style** tab in the web chat settings:

    - You can choose to use a different base Carbon Design theme. The supported base themes are color themes that are defined by [IBM Carbon Design](https://v10.carbondesignsystem.com/guidelines/color/usage/){: external}.

    - You can also set individual variables within the theme to customize specific UI elements. For example, the text that is displayed in the chat window uses the fonts `IBMPlexSans, Arial, Helvetica, sans-serif`. If you want to use a different font, you can specify it by using the [`updateCSSVariables()`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updatecssvariables){: external} method.

    ![development icon](images/development-icon.png) **Tutorial:** For a tutorial that shows how to choose and customize a theme, see [Carbon themes](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-carbon-themes){: external}.

Customizing the home screen {: #home-screen}
:   The home screen greets the customer and optionally shows a list of suggested conversation starters. You can customize the style and content of the home screen:

    - To add elements to the home screen, you can define custom HTML using the [`writeableElements.homeScreenAfterStartersElement`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#writeableelements){: external} theming variable.

    - To change the home screen style, use [CSS helper classes](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-render#helper_classes){: external}.

Customizing strings {: #strings}
:   You can customize the strings that define the various labels and hardcoded phrases displayed by the web chat. To customize strings, use the [`updateLanguagePack()`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updatelanguagepack){: external} instance method to replace strings in the current language pack. For more information, see [Languages](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#languages){: external}.

Supporting global audiences {: #global-audiences}
:   By default, the strings displayed by the web chat are in English. To change to a different language, use the [`updateLanguagePack()`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updatelanguagepack){: external} instance method to replace the current language pack with one of the available translated language packs. For more information, see [Supporting global audiences](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-global).

### Opening, closing, and rendering the web chat window
{: #web-chat-develop-open}

Replacing the default launcher {: #replace-launcher}
:   To better integrate with your website, you might want to replace the built-in launcher icon with a different mechanism for opening the web chat. To hide the default launcher, set the [`showLauncher`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#optionsshowLauncher){: external} configuration option to `false`. To open the web chat based on some other interaction, use the [`openWindow`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#openwindow){: external} instance method.

    ![development icon](images/development-icon.png) **Tutorial:** For a tutorial that shows you how to implement a custom launcher, see [Using a custom launcher](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-launcher){: external}.

Keeping the web chat always open {: #keep-open}
:    If you want to keep the web chat always open on your page, use the [`openChatByDefault`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#optionsopenChatByDefault){: external} configuration open to render the page with the chat window open, and the [`hideCloseButton`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#optionshideCloseButton){: external} option to prevent customers from closing it.

Changing where the web chat renders {: #custom-element}
:   Your website design might require that you change where and how the web chat window renders on your website. For example, you might want it to appear in a different position on the page, at a different size, or nested within another element on the page.

    To change the size of the web chat window, you can use the [updateCSSVariables()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updatecssvariables){: external} instance method to modify the CSS styling.

    If you need to change the position of the web chat window, or you need to change the size beyond the limits allowed in the CSS, you can use a custom DOM element to contain the web chat window. To do this, use the [`element`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#optionselement){: external} configuration option.

    ![development icon](images/development-icon.png) **Tutorial:** For a tutorial that shows how render the web chat in a custom element, see [Tutorial: Customizing the size and position of the web chat](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-size-position).

Adding the web chat to your mobile application {: #mobile}
:   You can use a WebView with a JavaScript bridge to add the web chat to your mobile application. For more information, see [Adding the web chat to your mobile application](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-mobile).

### Customizing the conversation
{: #web-chat-develop-conversation}

Intercepting and modifying messages {: #modify-messages}
:   By [subscribing to events](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#summary){: external}, your code can intercept messages that are sent and received between the customer and the assistant, and even modify their content.

    Subscribe to the [`pre:receive`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#prereceive){: external} event if you want to intercept a customer's message before it is sent to the assistant. For example, you might want to remove personally identifiable information from the message text or add context variables to the message payload.
    
    Subscribe to the [`pre:send`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#presend){: external} event if you want to intercept an incoming response from the assistant before it is shown to the customer. For example, you might want to add formatting, links, or other elements that are specific to the web chat.

    ![development icon](images/development-icon.png) **Tutorial:** For a tutorial showing how to use the `pre:receive` event to intercept and modify incoming messages, see [Tutorial: implementing custom option buttons in the web chat](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-custom-buttons).

Rendering custom response types {: #custom-response-types}
:   If your assistant sends specialized responses using a custom (`user_defined`) response type, you can implement a custom view to display these responses in the web chat window. To do this, subscribe to the [`customResponse`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#customresponse){: external} event, which is fired each time a `user_defined` response is received. In your event handler method, you can then read the contents of the response and render the output using your own elements.

    ![development icon](images/development-icon.png) **Tutorial:** For a tutorial showing how to render a custom response type as a replacement for the default options response, see [Tutorial: implementing custom option buttons in the web chat](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-custom-buttons).

Implementing a contact center integration {: #contact-center}
:   You can use one of the web chat starter kits to integrate with a contact center (service desk) platform other than the ones available in as built-in {{site.data.keyword.conversationshort}} integrations. Fully functional reference implementations are available for several contact center platforms; in addition, you can use a starter kit to develop a custom integration with the platform of your choice.

    For more information, see [Adding contact center support](/docs/watson-assistant?topic=watson-assistant-deploy-web-chat-haa).

### Managing data
{: #web-chat-develop-data}

Managing user identity information {: #user-id}
:   The web chat associates a user ID with each message it sends to the assistant; this user ID is used for user-based billing and other purposes. You can either allow the web chat to generate an anonymous ID for each user, or you can control the user ID yourself.

    Depending on whether you have enabled security for the web chat, you can use either the [`updateUserID`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateuserid){: external} instance method or the [`updateIdentityToken`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateidentity){: external} method to specify user identity information.

    For more information about how user identity information is specified and how it is used, see [Managing user identity information](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-userid).

### Security and administration
{: #web-chat-develop-admin}

Securing the web chat {: #secure-web-chat}
:   To secure the web chat, you can use JSON Web Token (JWT) to authenticate users and encrypt private data. For more information, see [Securing the web chat](/docs/watson-assistant?topic=watson-assistant-web-chat-security).

Controlling the web chat version {: #web-chat-version}
:   The web chat code hosted by {{site.data.keyword.cloud_notm}} is regularly updated with improvements and new features. By default, the embed script automatically uses the latest version of the web chat. To avoid unexpected changes that might affect your website, you might want to control which version of the web chat your website uses, giving you an opportunity to test each new version before you deploy in in production., in order to avoid unexpected changes when a new version is released.

    For more information about web chat versioning, see [Controlling the web chat version](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-versions).

