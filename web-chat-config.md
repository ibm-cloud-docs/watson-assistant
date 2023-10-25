---

copyright:
  years: 2019, 2023
lastupdated: "2023-10-25"

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



# Web chat setup overview
{: #web-chat-config}

You can modify the web chat integration settings to configure the styling and appearance of the web chat.
{: shortdesc}

You can quickly deploy and test the web chat integration using the default settings. However, before you go to production with your chatbot, you will need to configure the web chat to integrate with your website and better serve the needs of your customers.

At a minimum, you should update the following basic settings for your assistant:

- The [assistant name](/docs/watson-assistant?topic=watson-assistant-web-chat-style) that you want to show to your customers
- The contents of the [home screen](/docs/watson-assistant?topic=watson-assistant-web-chat-configure-home-screen)
- The [suggestions](/docs/watson-assistant?topic=watson-assistant-web-chat-suggestions) your assistant will offer if customers get stuck

You might also want to make additional configurations, such as changing the web chat colors to match your branding, changing the launcher greeting, or enabling encryption.

If you are a developer, you can customize the web chat by using the web chat API. With the API, you can customize the styling, change the behavior of the web chat widget and launcher, customize strings, modify message content, and more. For more information about using the web chat API, see [Web chat development overview](/docs/watson-assistant?topic=watson-assistant-web-chat-develop).
{: tip}

To change the web chat configuration, follow these steps:

1. On the ![Integrations icon](images/integrations-icon.png) **Integrations** page, find the **Web chat** tile and click **Open**. The **Open web chat** window opens.

1. In the **Environment** field, select the environment you want the web chat widget to connect to. Click **Confirm**.

    The **Web chat** page opens, showing the settings for the web chat integration in the selected environment.

## Setup tasks
{: #web-chat-config-tasks}

You can configure the web chat in the following ways:

Style and appearance
:   You can configure the overall appearance of the web chat widget, including the assistant name, the colors of various elements, and the avatar image. For more information, see [Configuring style and appearance](/docs/watson-assistant?topic=watson-assistant-web-chat-style).

Launcher
:   You can change the greeting text that is shown by the launcher that invites users to open the web chat. On the **Launcher** tab, you can specify separate greeting messages for the desktop launcher and the mobile launcher.

    The message you specify is immediately reflected by the launcher preview that is shown on the page. However, no configuration changes are applied to the environment until you click **Save and exit**.

Home screen
:   You can configure the contents of the home screen that greets customers and helps them start the conversation. For more information, see [Configuring the home screen](/docs/watson-assistant?topic=watson-assistant-web-chat-configure-home-screen).

Suggestions
:   You can configure how and when the web chat offers offers suggestions to customers when the assistant isn't delivering what they expect. For more information, see [Configuring suggestions](/docs/watson-assistant?topic=watson-assistant-web-chat-suggestions).

Security
:   You can protect your users' private information and prevent unauthorized messages to your assistant by enabling security on the **Security** tab. For more information about web chat security and how it works, see [Security](/docs/watson-assistant?topic=watson-assistant-web-chat-security).

Voice
:   You can [give your assistant a clear and friendly voice](https://www.ibm.com/products/watson-assistant/voice) by adding Watson Text to Speech. For more information about converting written text to natural-sounding audio and explore a demo, see [Text to Speech](https://www.ibm.com/products/text-to-speech).
