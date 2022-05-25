---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-25"

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

# Configuring the web chat
{: #web-chat-config}

You can modify the web chat integration settings to configure the styling and appearance of the web chat.
{: shortdesc}

Before you deploy the web chat widget to your production website, you will probably need to update at least the following basic settings for your assistant:

- The [assistant name](#web-chat-style) that you want to show to your customers
- The contents of the [home screen](#web-chat-home-screen)
- The [suggestions](#web-chat-suggestions) your assistant will offer if customers get stuck

You might also want to make additional configurations, such as changing the web chat colors to match your branding, changing the launcher greeting, or enabling encryption.

If you are a developer, you can customize the web chat extensively by using the web chat API. With the API, you can customize the styling, change the behavior of the web chat widget and launcher, customize strings, modify message content, and more. For more information about using the web chat API, see [Customizing the web chat](/docs/watson-assistant?topic=watson-assistant-web-chat-customize).
{: tip}

To change the web chat configuration, follow these steps:

1. On the ![Integrations icon](images/integrations-icon.png) **Integrations** page, find the **Web chat** tile and click click **Open**. The **Open web chat** window opens.

1. In the **Environment** field, select **Draft** or **Live**, depending on which environment you want to configure the web chat widget in. The web chat is configured separately for the draft and live environments. Click **Confirm**.

    The **Web chat** page opens, showing the settings for the web chat integration in the selected environment.

## Configuring style and appearance
{: #web-chat-style}

On the **Style** tab, you can configure the overall appearance of the web chat widget. You can make the following changes:

- Set the assistant name. Click **Assistant's name as known by customers** to specify the name that is displayed in the header of the chat window. The name can be up to 64 characters in length.

- Change the colors used in the web chat widget. You can set the following colors:
  
    - **Primary color**: The color of the web chat header.
    - **Secondary color**: The color of the customer input message bubble.
    - **Accent color**: The color of interactive elements such as the following:
        - Web chat buttons such as the suggestions button and the "send message" button
        - The border around the input text field (when in focus)
        - The markers that appear beside the assistant’s messages
        - The borders that appear around buttons and drop-down lists when customers select from options
        - The home screen background

    Each color is specified as an HTML hexadecimal color code, such as `#FF33FC` for pink and `#329A1D` for green. To change a color, type the HTML color code you want to use, or click the dot next to the field and choose the color from the interactive color picker.

- Enable or disable the **Built with IBM Watson** watermark that is displayed in the web chat widget. To disable the watermark, click to toggle the **IBM Watermark** switch to the off position. (The watermark cannot be disabled on the Lite plan.)

- Provide an avatar image to represent your assistant or organization in the web chat header. Click **Add an avatar image** to add an image, or **Change avatar image** to change an image you have previously added.

    Specify the URL for a publicly accessible hosted image, such as a company or brand logo or an assistant avatar. The image file must be between 64 x 64 and 100 x 100 pixels in size.

Style changes you make are immediately reflected by the web chat preview that is shown on the page. However, no configuration changes are applied to the environment until you click **Save and exit**.

## Configuring the launcher
{: #web-chat-configure-launcher}

On the **Launcher** tab, you can change the greeting text that is shown by the launcher that invites users to open the web chat. Separate greeting messages are configured for the desktop launcher and the mobile launcher.

The message you specify is immediately reflected by the launcher preview that is shown on the page. However, no configuration changes are applied to the environment until you click **Save and exit**.

## Configuring the home screen
{: #web-chat-configure-home-screen}

On the **Home screen** tab, you can configure the contents of the home screen, which welcomes customers and helps them start the conversation with the assistant. The home screen replaces any greeting that would otherwise be sent by the *Greet customer* system action.

![An example of the home screen](images/home-screen.png)

If you prefer to use a *Greet customer* system action instead of the home screen, you can disable it by clicking the toggle switch on the **Home screen** tab.

If you use the home screen, you must configure it to show content that is relevant to your customers:

- In the **Greeting message** field, type a greeting that is engaging and invites the user to interact with your assistant. This greeting is the first message your customers will see when they open the web chat window.

- In the **Conversation starters** section, specify three conversation starter messages.

    These messages are displayed on the home screen as options that customers can click to start the conversation (for example, `I need to reset my password` or `What is my account balance?`). Specify conversation starters that are likely to be useful to your customers, and that your assistant knows how to handle. 

    Be sure to test each conversation starter. Use only messages that your assistant understands and knows how to answer well. Conversation starters cannot be longer than 35 characters.

    All three conversation starters are required.

The messages you specify are immediately reflected by the web chat preview that is shown on the page, and you can click the conversation starters to see how your assistant responds. However, no configuration changes are applied to the environment until you click **Save and exit**.

## Configuring suggestions
{: #web-chat-suggestions}

*Suggestions* give your customers a way to try something else when the current exchange with the assistant isn't delivering what they expect. A question mark icon ![Question mark icon](images/question-mark.png) is displayed in the web chat that customers can click at any time to see other topics that might be of interest or, if configured, to request support. Customers can click a suggested topic to submit it as input or click the **X** icon to close the suggestions list.

If customers select a suggestion and the response is not helpful, they can open the suggestions list again to try a different suggestion. The input generated by the first choice is submitted and recorded as part of the conversation. However, any contextual information that is generated by the initial suggestion is reset when the subsequent suggestion is submitted.

The suggestions are shown automatically in situations where the customer might otherwise become frustrated. For example, if a customer uses different wording to ask the same question multiple times in succession, and the same action is triggered each time, then related topic suggestions are shown in addition to the triggered action's response. The suggestions that are offered give the customer a quick way to get the conversation back on track.

The suggestions list is populated with actions that are relevant in some way to the matched action. The actions are ones that the AI model considered to be possible alternatives, but that didn't meet the high confidence threshold that is required for an action to be listed as a disambiguation option. Any action can be shown as a suggestion, unless its **Ask clarifying question** setting is set to **Off**. For more information about the **Ask clarifying question** setting, see [Asking clarifying questions](/docs/watson-assistant?topic=watson-assistant-understand-questions#understand-questions-ask-clarifying-question).

To configure suggestions, complete the following steps:

1. Open the **Suggestions** tab.

    Suggestions are enabled automatically for new web chat integrations. If you don't want to use suggestions, toggle the switch to **Off**.

1. In the **Include a connection to support** section, specify when you want an option to connect with support to be included in the list of suggestions. You can specify **Always**, **Never**, or **After one failed attempt**.

    **After one failed attempt**: Adds the option to the list only if the customer reached a node with an `anything_else` condition in the previous conversation turn or reaches the same action for a second time in succession.

1. In the **Option label** field, type the text of the message that requests help from support. This message is shown as the label for the support option, which is included in the **Suggestions** window under the circumstances you specified in the previous step. If the customer clicks this option, the same message is sent to the assistant.

    The message you specify should trigger an action that gives customers a way to connect with support. By default, the message `Connect with agent` is used. If your web chat is integrated with a service desk, this message initiates a transfer to a human agent. (For more information about integrating with a service desk, see [Adding service desk support](/docs/watson-assistant?topic=watson-assistant-deploy-web-chat-haa).)

    If your web chat is not integrated with a service desk, specify a message that helps your customers reach whatever form of support you do offer. If you offer a toll-free support line, you might add `Get the support line phone number`. Or if you offer an online support request form, you might add `Open a support ticket`.

    Whether you use the default support message or add your own, make sure your action is designed to recognize the message and respond to it appropriately.
    <!--- For more information, see [Connecting customers with support](/docs/assistant?topic=assistant-dialog-support){: external}. --->

## Security
{: #web-chat-configure-security}

To secure the web chat, click the **Security** tab. For more information, see [Securing the web chat](/docs/watson-assistant?topic=watson-assistant-web-chat-security).
