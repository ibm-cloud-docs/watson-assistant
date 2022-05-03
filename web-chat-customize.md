---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-03"

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

# Customizing the web chat
{: #web-chat-customize}

You can modify the web chat integration settings to configure the styling and appearance of the web chat.
{: shortdesc}

Before you deploy the web chat widget to your production website, you will probably need to make the following basic customizations for your assistant:

- Specify the [assistant name](/docs/watson-assistant?topic=watson-assistant-topicid) that you want to show to your customers
- Configure the [home screen](/docs/watson-assistant?topic=watson-assistant-topicid)
- Suggestions

You might also want to make additional customizations, such as changing the web chat colors to match your branding, customizing the launcher behavior, or enabling encryption. The web chat is configured separately for the draft and live environments.

If you are a developer, you can customize the web chat even more extensively by using the web chat API. With the API, you can customize the styling, change the behavior of the web chat widget and launcher, customize strings, modify message content, and more. For more information about using the web chat API, see [Heading](/docs/watson-assistant?topic=watson-assistant-topicid).
{: tip}

To customize the web chat integration, follow these steps:

1. On the ![Integrations icon](images/integrations-icon.png) **Integrations** page, find the **Web chat** tile and click click **Open**. The **Open web chat** window opens.

1. In the **Environment** field, select **Draft** or **Live**, depending on which environment you want to configure the web chat widget in. Click **Confirm**.

    The **Web chat** page opens, showing the settings for the web chat integration in the selected environment.

## Style
{: #web-chat-customize-style}

On the **Style** tab, you can customize the overall appearance of the web chat widget. You can make the following changes:

  - Set the assistant name. Click **Assistant's name as known by customers** to specify the name that is displayed in the header of the chat window. The name can be up to 64 characters in length.

  - Customize the colors used in the web chat widget. You can set the following colors:
  
    - **Primary color**: The color of the web chat header.
    - **Secondary color**: The color of the customer input message bubble.
    - **Accent color**: The color of interactive elements such as the following:
      - Web chat buttons such as the suggestions button and the "send message" button
      - The border around the input text field (when in focus)
      - The markers that appear beside the assistant’s messages
      - The borders that appear around buttons and drop-down lists when customers select from options
      - The home screen background
      <!--- Pause response type not yet supported in actions --->
      <!--- - Typing indicator that is shown to represent a pause response --->

    Each color is specified as an HTML color code, such as `#FF33FC` for pink and `#329A1D` for green. To change a color, type the HTML color code you want to use, or click the dot next to the field and choose the color from the interactive color picker.

  - Enable or disable the **Built with IBM Watson** watermark that is displayed in the web chat widget. To disable the watermark, click to toggle the **IBM Watermark** switch to the off position. (The watermark cannot be disabled on Lite plans.)

  - Provide an avatar image to represent your assistant or organization in the web chat header. Click **Add an avatar image** to add an image, or **Change avatar image** to change an image you have previously added.

    Specify the URL for a publicly accessible hosted image, such as a company or brand logo or an assistant avatar. The image file must be between 64 x 64 and 100 x 100 pixels in size.

Style changes you make are immediately applied to the preview that is shown on the page, so you can see how your choices impact the style of the chat UI. However, no changes are applied to the environment until you click **Save and exit**.

## Launcher
{: #web-chat-customize-launcher}

customize launcher

## Home screen
{: #web-chat-customize-home-screen}

The home screen helps to ease your customers into a conversation with your assistant. You can add a greeting and a list of quick conversation starter questions for customers to click. For more information, see [Configuring the home screen](#deploy-web-chat-home-screen).

If you don't want to use a home screen, go to the **Home screen** tab and toggle the switch to **Off**.

By default, the web chat window shows a home screen that can welcome users and tell them how to interact with the assistant. The home screen replaces any greeting that would otherwise be sent by the *Greet customer* system action in an actions skill. If you prefer to use a *Greet customer* system action instead of the home screen, you can disable the home screen on the **Home screen** tab.

![An example of the home screen](images/home-screen.png)

1.  Add a greeting that is engaging and invites the user to interact with your assistant. A greeting is required.

1.  Add three conversation starter messages.

    These messages are displayed in the web chat as examples of the types of questions that customers can ask. Customers can click one of them to submit it to the assistant.

    You must test each message that you add as a conversation starter. Use only questions that the assistant understands and knows how to answer well.

    All three conversation starters are required.

A developer can customize the home screen even more:

- A **Get started** heading is displayed before the list of conversation starter messages. A developer can change the heading text by replacing the `homeScreen_conversationStarterLabel` in the web chat language strings file. For more information, see the [instance.updateLanguagePack() method](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updatelanguagepack){: external} documentation.
- You can use the web chat API to add other elements to the home screen page. For more information, see the [instance.writeableElements() method](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#writeableelements){: external} documentation.
- For information about CSS helper classes that you can use to change the home screen style, see the [prebuilt templates](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-render#html){: external} documentation.

## Live agent
{: #web-chat-customize-live-agent}

To configure support for transferring conversations to a service desk agent, click the **Live agent** tab. For more information, see [Adding service desk support](#deploy-web-chat-haa).

## Suggestions
{: #web-chat-customize-suggestions}

The web chat gives your customers a way to reroute the conversation if they get stuck by showing them a list of intelligent suggestions, search results, and a path of contact for more help. Suggestions are enabled automatically. You can control how often suggestions are displayed and what they include. Click the **Suggestions** tab.
<!--- For more information, see [Showing more suggestions](#deploy-web-chat-alternate). --->

*Suggestions* give your customers a way to try something else when the current exchange with the assistant isn't delivering what they expect. A question mark icon ![Question mark icon](images/question-mark.png) is displayed in the web chat that customers can click at any time to see other topics that might be of interest or, if configured, to request support. Customers can click a suggested topic to submit it as input or click the **X** icon to close the suggestions list.

If customers select a suggestion and the response is not helpful, they can open the suggestions list again to try a different suggestion. The input generated by the first choice is submitted and recorded as part of the conversation. However, any contextual information that is generated by the initial suggestion is reset when the subsequent suggestion is submitted.

The suggestions are shown automatically in situations where the customer might otherwise become frustrated. For example, if a customer uses different wording to ask the same question multiple times in succession, and the same action is triggered each time, then related topic suggestions are shown in addition to the triggered action's response. The suggestions that are offered give the customer a quick way to get the conversation back on track.

The suggestions list is populated with actions that are relevant in some way to the matched action. The actions are ones that the AI model considered to be possible alternatives, but that didn't meet the high confidence threshold that is required for an action to be listed as a disambiguation option. Any action can be shown as a suggestion, unless its **Ask clarifying question** setting is set to **Off**. For more information about the **Ask clarifying question** setting, see [Asking clarifying questions](/docs/watson-assistant?topic=watson-assistant-understand-questions#understand-questions-ask-clarifying-question).

To customize suggestions, complete the following steps:

1.  Open the *Suggestions* tab.

    The Suggestions feature is enabled automatically for new web chat integrations. If it's not enabled, set the Suggestions switch to **On**.

    The *Include a connection to support* section is displayed where you can configure whether and how to give customers the ability to connect with support.
1.  Decide when you want an option to connect with support to be shown in the suggestions list. The choices are:

    - **Always**: Always shows the option to get support in the list of suggestions.
    - **Never**: Never shows the option to get support in the list of suggestions.
    - **After one failed attempt**: Adds the option to the list only if the customer reached a node with an `anything_else` condition in the previous conversation turn or reaches the same action for a second time in succession.

1.  In the **Option label** field, add a label for the option.

    The text in the **Option label** field has two functions:

    - The text is shown in the suggestions list as an option for customers to select.
    - When selected by a customer, the text is sent to your assistant as a new message. The label must be able to function as input that your action understands and knows how to handle.

    By default, the option label `Connect with agent` is used. If your web chat is integrated with a service desk, this message initiates a conversation transfer, as long as your action is designed to handle transfer requests.

    If your web chat is not integrated with a service desk, you can change the option label to a message that helps your customers reach whatever form of support you do offer. If you offer a toll-free support line, you might add `Get the support line phone number`. Or if you offer an online support request form, you might add `Open a support ticket`.

    Whether you use the default option label or add your own, make sure your action is designed to recognize the message and respond to it appropriately.
    <!--- For more information, see [Connecting customers with support](/docs/assistant?topic=assistant-dialog-support){: external}. --->

## Security
{: #web-chat-customize-security}

To secure the web chat, click the **Security** tab. For more information, see [Securing the web chat](/docs/watson-assistant?topic=watson-assistant-web-chat-security).

