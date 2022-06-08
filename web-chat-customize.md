---

copyright:
  years: 2019, 2022
lastupdated: "2022-06-06"

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

# Web chat customization overview
{: #web-chat-customize}

If you are comfortable with JavaScript code, you can customize and extend the web chat by modifying the embed script and using the web chat API.
{: shortdesc}

For detailed reference about the web chat API, see the web chat [developer documentation](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=){: external}.

## Web chat API
{: #web-chat-customize-api}

The web chat API consists of several components:

- **Configuration object**: The embed script defines a configuration object named `watsonAssistantChatOptions`, which specifies configuration objects for the web chat widget. By editing the configuration object, you can customize the appearance and behavior of the web chat before it is rendered. For more information about the available configuration options, see [Configuration options object](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#configurationobject){: external} in the web API reference.
- **Instance methods**: The web chat instance methods provide low-level control of the web chat widget. You can use the instance methods to implement custom behavior such as changing how the web chat widget opens, showing and hiding content, and setting identity information. For more information about the available instance methods, see [List of methods and properties](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#listofmethods){: external} in the web chat API reference.
- **Events**: The web chat event system makes it possible for your website to respond to web chat events (such as opening or closing the web chat window, sending or receiving messages). By subscribing to events, you can implement custom behavior or even intercept and modify message content. For more information about the event system, see [Events](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events){: external} in the web chat API reference.

## Customization tasks
{: #web-chat-customize-tasks}

You can customize the web chat in the following ways:

Replacing the default launcher
:   To better integrate with your website, you might want to replace the built-in launcher icon with a different mechanism for opening the web chat. To hide the default launcher, set the [`showLauncher`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#optionsshowLauncher){: external} configuration option to `false`. To open the web chat based on some other interaction, use the [`openWindow`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#openwindow){: external} instance method.

    For a tutorial that shows you how to implement a custom launcher, see [Using a custom launcher](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-launcher){: external}.

Keeping the web chat always open
:    If you want to keep the web chat always open on your page, use the [`openChatByDefault`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#optionsopenChatByDefault){: external} configuration open to render the page with the chat window open, and the [`hideCloseButton`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#optionshideCloseButton){: external} option to prevent customers from closing it.

Changing where the web chat renders
:   Your website design might require that you change where and how the web chat window renders on your website. For example, you might want it to appear in a different location, at a different size, or nested within another section of the page. To accomplish this, you can use the [`element`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#optionselement){: external} configuration option to specify a custom DOM element that will contain the web chat window at run time.

    For a tutorial that shows how to do this, see [Render to a custom element](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-example-element){: external}.

Customizing the home screen
:   You can customize what is displayed in the home screen. For more information, see [Customizing the home screen](/docs/watson-assistant?topic=watson-assistant-web-chat-customize-home-screen).

Intercept and modify incoming or outgoing messages
:   By [subscribing to events](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#summary){: external}, your code can intercept messages that are sent and received between the customer and the assistant, and even modify their content.

    Subscribe to the [`pre:receive`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#prereceive){: external} event if you want to intercept a customer's message before it is sent to the assistant. For example, you might want to remove personally identifiable information from the message text or add context variables to the message payload.
    
    Subscribe to the [`pre:send`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#presend){: external} event if you want to intercept an incoming response from the assistant before it is shown to the customer. For example, you might want to add formatting, links, or other elements that are specific to the web chat.

Rendering custom response types
:   If your assistant sends specialized responses using a custom (`user_defined`) response type, you can implement a custom view to display these responses in the web chat window. For a tutorial that shows how to do this, see **?????**.

Customizing the look of the web chat
:   You can customize the style and appearance of the web chat beyond the options that are available from the **Style** tab in the web chat settings. For more information, see [Customizing the look of the web chat](/docs/watson-assistant?topic=watson-assistant-web-chat-customize-look).

Managing user identity information
:   You can control the user identity information the web chat sends to the assistant. For more information, see [Managing user identity information](/docs/watson-assistant?topic=watson-assistant-web-chat-customize-userid)

Customizing strings
:   You can customize the strings that define the various labels and hardcoded phrases displayed by the web chat. For more information, see [Customizing strings](/docs/watson-assistant?topic=watson-assistant-web-chat-customize-strings).

Supporting global audiences
:   You can change the language of the strings displayed by the web chat to match the language used by the assistant. For more information, see [Supporting global audiences](/docs/watson-assistant?topic=watson-assistant-web-chat-customize-global).

Securing the web chat
:   You can secure the web chat to support user authentication and protect private data. For more information, see [Securing the web chat](/docs/watson-assistant?topic=watson-assistant-web-chat-security).

Controlling the web chat version
:   You can control which version of the web chat your website uses, in order to avoid unexpected changes when a new version is released. For more information, see [Controlling the web chat version](/docs/watson-assistant?topic=watson-assistant-web-chat-customize-versions).

Implementing a contact center integration
:   You can use one of the web chat starter kits to integrate with a contact center (service desk) platform other than the ones available in as {{site.data.keyword.conversationshort}} integrations. For more information, see [Service desk starter kits](/docs/watson-assistant?topic=watson-assistant-web-chat-service-desk-starter-kits).

