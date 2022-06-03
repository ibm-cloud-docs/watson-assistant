---

copyright:
  years: 2019, 2022
lastupdated: "2022-06-01"

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

# Configuring style and appearance
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
