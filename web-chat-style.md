---

copyright:
  years: 2019, 2024
lastupdated: "2024-06-23"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Configuring style and appearance
{: #web-chat-style}

## Steps to Customize the Chat Window

You can configure the style and appearance of your web chat widget by doing the following steps.

1. Go to Home > Preview > Customize web chat > Style to configure the overall appearance of the web chat widget. 

1.	Select the name of the assistant per the customer requirement so that it is displayed in the header of the chat window. The name can be up to 64 characters in length. 

1.	You can set the following colors: 

-   Primary color: The color of the web chat header. 
-   Secondary color: The color of the customer input message bubble. 
-   Accent color: The color of the interactive elements, including: 
    -   Web chat buttons, such as the suggestions button and the **send message** button. 
    -   The border around the input text field (when in focus). 
    -   The markers that appear next to the assistant's messages. 
    -   The borders around the buttons and drop-down lists when customers select from options. 
    -   The **home screen** background. 
    
    Each color is specified as an HTML hexadecimal color code, such as `#FF33FC` for pink and `#329A1D` for green. To change a color, type the HTML color code that you want to use, or click the dot next to the field and choose the color from the interactive **color picker**.
    {: tip}

1.  Toggle the **IBM Watermark** switch to `enable` or `disable` the `Built with IBM Watson` watermark in the web chat widget.

    The watermark cannot be disabled if you are on the Lite plan of watsonx Assistant.
    {: note}

1.	Click **Add an avatar image** to add an image, or **Change avatar image** to change an existing image. Specify the URL for a publicly accessible hosted image, such as a company logo or assistant avatar. The image must be between `64×64` and `100×100` pixels in size.

Style changes are immediately reflected in the web chat preview shown on the page. However, no configuration changes are applied to the environment until you **Save and exit**.

You can now use the Carbon for AI in your web chat style. For more information about Carbon for AI integration in your web chat, see [Configuration](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#theme-config).

You can customize a full-screen chat window by setting a max-width and removing the drop shadow that provides seamless integration for your assistant. For more information, see [Layout configuration](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html).
{: shortdesc}
