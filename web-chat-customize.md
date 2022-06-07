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

If you are comfortable with JavaScript code, you can extensively customize and extend the web chat by modifying the embed script and using the web chat API.
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

Changing how the web chat opens and closes
:   You can change the appearance and behavior of the launcher, or remove the launcher and define a different way of opening the web chat window. For more information, see [Changing how the web chat opens and closes](/docs/watson-assistant?topic=watson-assistant-web-chat-customize-open-close).

Customizing the home screen
:   You can customize what is displayed in the home screen. For more information, see [Customizing the home screen](/docs/watson-assistant?topic=watson-assistant-web-chat-customize-home-screen).

Customizing the conversation
:   You can modify the information that is sent and received between the web chat and the assistant, and customize how assistant responses are displayed in the web chat. For more information, see [Customizing the conversation](/docs/watson-assistant?topic=watson-assistant-web-chat-customize-conversation).

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

