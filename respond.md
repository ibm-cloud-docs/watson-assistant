---

copyright:
  years: 2021, 2022
lastupdated: "2022-12-05"

subcollection: watson-assistant

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:deprecated: .deprecated}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

{{site.data.content.classiclink}}

# Adding assistant responses
{: #respond}

Once an action is activated, the body of the action is composed of multiple *steps* that make up the conversation between your assistant and your users. One part of each step is what the assistant says to the customer when the step is processed.

To create your assistant's response in a step, you use the **Assistant says** section. This represents the text or speech the assistant delivers to a user at a particular step. Depending on the step, you can add a complete answer to a user's question or ask a follow-up question.

You can enter a simple text response just by entering the text that you want your assistant to display to the user. You can also add formatting and web content, and you can reference user information using *variables*.

## Formatting responses
{: #respond-formatting}

Use the text editor tools to apply font styling, such as bold or italic, to the text or to add links.

Behind the scenes, font styling and link syntax are stored in Markdown format. If you are using the web chat integration, HTML and Markdown tagging are supported (for more information, see [Markdown formatting](/docs/watson-assistant?topic=watson-assistant-web-chat-architecture#web-chat-architecture-markdown)).

HTML tags (except for links) are automatically removed from text responses that are sent to the Facebook, WhatsApp, and Slack integrations, because those channels do not support HTML formatting. HTML tags are still handled appropriately in channels that support them (such as the web chat) and stored in the session history.

<!--- Behind the scenes, these three choices are stored using Markdown format.

| Choice | Markdown | Example output |
|------------|--------|---------|
| Bold | `There's **no** crying in baseball.` | There's **no** crying in baseball. |
| Italic | `We're talking about *practice*.` | We're talking about *practice*. |
| Link | `Contact us at [ibm.com](https://www.ibm.com).` | Contact us at [ibm.com](https://www.ibm.com). |
{: caption="Formatting" caption-side="top"} --->

If you're using a custom client application that does not support Markdown, don't apply text styling to your text responses.
{: note}

## Adding and referencing variables
{: #respond-variables}

During the conversation, your assistant stores information as *variables*. Variables are containers for data values that become available at run time; the value of a variable can change over time. Variables include *action variables*, which persist only during a particular action, and *session variables*, which are available to any action. For more information about variables, see [Managing information during the conversation](/docs/watson-assistant?topic=watson-assistant-manage-info).

In your assistant's output, you can reference variables in order to personalize the conversation or include information that is available at run time. For more information about referencing variables in what your assistant says, see [Using variables to customize the conversation](/docs/watson-assistant?topic=watson-assistant-manage-info#reference-variables).

## Testing responses
{: #respond-testing}

To see if the assistant responses are formatted correctly, you can use **Preview**.

1. Click the **Preview** button.
1. To start the action, enter your first phrase, for example: `What are your store hours?`.
1. When the assistant responds, check that the message displays as you intended with formatting, use of variables, and so on.

## Tips for adding responses
{: #respond-tips-responses}

- Keep answers short and useful.
- Reflect the user's intent in the response. Doing so assures users that the bot is understanding them, or if it is not, gives users a chance to correct a misunderstanding immediately.
- Only include links to external sites in responses if the answer depends on data that changes frequently.
- Word your responses carefully. You can change how someone reacts to your system based simply on how you phrase a response. Changing one line of text can prevent you from having to write multiple lines of code to implement a complex programmatic solution.

## Media responses
{: #respond-response-types}

In addition to text responses, you can use other _response types_ to send responses that include multimedia or interactive elements. 

The action editor supports the following media response types:

- **Image**: Embeds an image into the response. The source image file must be hosted somewhere and have a URL that you can use to reference it. It cannot be a file that is stored in a directory that is not publicly accessible.
- **Video**: Embeds a video player into the response. The source video must be hosted somewhere, either as a playable video on a supported video streaming service or as a video file with a URL that you can use to reference it. It cannot be a file that is stored in a directory that is not publicly accessible.
- **Audio**: Embeds an audio clip into the response. The source audio file must be hosted somewhere and have a URL that you can use to reference it. It cannot be a file that is stored in a directory that is not publicly accessible.
- **iframe**: Embeds content from an external website, such as a form or other interactive component, directly within the chat. The source content must be publicly accessible using HTTP, and must be embeddable as an HTML `iframe` element.

Different channel integrations have different capabilities for displaying media responses. To see which channel integrations support which response types, see [Channel integration support for response types](/docs/watson-assistant?topic=watson-assistant-assistant-responses-json-integration-support).

If you want to define different responses that are customized for different channels, you can do so by editing the response using the JSON editor. For more information, see [Targeting specific integrations](/docs/watson-assistant?topic=watson-assistant-assistant-responses-json#assistant-responses-json-target-integrations).

By editing your responses using the JSON editor, you can also access additional response types for handling channel-specific interactions.

For more information about how to edit responses using the JSON editor, see [Defining responses using the JSON editor](/docs/watson-assistant?topic=watson-assistant-assistant-responses-json).
{: note}

### Adding an *Image* response
{: #respond-add-image}

Add an *Image* response to display an image to the customer.

The *Image* response type is supported by the following channel integrations:
- Web chat
- SMS
- Slack
- Facebook
- WhatsApp

To add an *Image* response, complete the following steps:

1. In the **Assistant says** field, click the ![Image](images/image-response.png) **Image** icon.

1. In the **Source URL** field, type the full URL to the hosted image.

    The image must be in `.jpg`, `.gif`, or `.png` format. The image file must be stored in a location that is publicly addressable by an `https:` URL (such as `https://www.example.com/assets/common/logo.png`).

    To access an image that is stored in {{site.data.keyword.cloud}} {{site.data.keyword.cos_short}}, enable public access to the individual image storage object, and then reference it by specifying the image source with syntax like this: `https://s3.eu.cloud-object-storage.appdomain.cloud/your-bucket-name/image-name.png`.

1. Optionally specify an image title, description, and alt text in the fields provided. In the web chat integration, the title and description are displayed along with the image.

    References to variables are not supported. Some integration channels ignore titles or descriptions.
    {: note}

1. Click **Apply**.

### Adding an *Audio* response
{: #respond-add-audio}

Add an *Audio* response to include spoken-word or other audible content. In the web chat, an audio response renders as an embedded audio player. In the phone integration, an audio response plays over the phone.

The *Audio* response type is supported by the following channel integrations:
- Web chat
- Phone
- SMS
- Slack
- Facebook
- WhatsApp

To add an *Audio* response, complete the following steps:

1. In the **Assistant says** field, click the ![Audio](images/audio-response.png) **Audio** icon.

1. In the **Source URL** field, type the full URL to the hosted audio clip:

    - To link directly to an audio file, specify the URL to a file in any standard format such as MP3 or WAV. In the web chat, the linked audio clip will render as an embedded audio player.

    - To link to an audio clip on a supported audio hosting service, specify the URL to the audio clip. In the web chat, the linked audio clip will render using the embeddable player for the hosting service.

      Specify the URL you would use to access the audio file in your browser (for example, `https://soundcloud.com/ibmresearch/fallen-star-amped`). You do not need to convert the URL to an embeddable form; the web chat will do this automatically.
      {: note}

      You can embed audio hosted on the following services:
      - [SoundCloud](https://soundcloud.com){: external}
      - [Mixcloud](https://mixcloud.com){: external}

1. Optionally specify a title, description, and alt text in the fields provided. In the web chat integration, the title and description are displayed along with the audio player.

    References to variables are not supported. Some integration channels ignore titles or descriptions.
    {: note}

### Adding a *Video* response
{: #respond-add-video}

Add a *Video* response to display a how-to demonstration, promotional clip, or other video content. In the web chat, a video response renders as an embedded video player.

The *Video* response type is supported by the following channel integrations:
- Web chat
- SMS
- Slack
- Facebook
- WhatsApp

To add a *Video* response, complete the following steps:

1. In the **Assistant says** field, click the ![Video](images/video-response.png) **Video** icon.

1. In the **Source URL** field, type the full URL to the hosted video:

    - To link directly to a video file, specify the URL to a file in any standard format such as MPEG or AVI. In the web chat, the linked video will render as an embedded video player.

      HLS (`.m3u8`) and DASH (MPD) streaming videos are not supported.
      {: note}

    - To link to a video hosted on a supported video hosting service, specify the URL to the video. In the web chat, the linked video will render using the embeddable player for the hosting service.

      Specify the URL you would use to view the video in your browser (for example, `https://www.youtube.com/watch?v=52bpMKVigGU`). You do not need to convert the URL to an embeddable form; the web chat will do this automatically.
      {: note}

      You can embed videos hosted on the following services:
      - [YouTube](https://youtube.com){: external}
      - [Facebook](https://facebook.com){: external}
      - [Vimeo](https://vimeo.com){: external}
      - [Twitch](https://twitch.tv){: external}
      - [Streamable](https://streamable.com){: external}
      - [Wistia](https://wistia.com){: external}
      - [Vidyard](https://vidyard.com){: external}

1. Optionally specify a video title, description, and alt text in the fields provided. In the web chat integration, the title and description are displayed along with the video player.

    References to variables are not supported. Some integration channels ignore titles or descriptions.
    {: note}

1. If you want to scale the video to a specific display size, specify a number in the **Base height** field.

### Adding an *iframe* response
{: #respond-add-iframe}

Add an *iframe* response to embed content from another website directly inside the chat window as an HTML `iframe` element. An iframe response is useful if you want to enable customers to perform some interaction with an external service without leaving the chat. For example, you might use an *iframe* response to display the following within the web chat:

- An interactive map on [Google Maps](https://www.google.com/maps){: external}
- A survey using [SurveyMonkey](https://www.surveymonkey.com/){: external}
- A form for making reservations through [OpenTable](https://www.opentable.com/){: external}
- A scheduling form using [Calendly](https://calendly.com/){: external}

In the web chat, an iframe response renders as a preview card that describes the embedded content. Customers can click this card to display the frame and interact with the content.

The *iframe* response type is supported by the following channel integrations:
- Web chat
- Facebook

To add an *iframe* response type, complete the following steps:

1. In the **Assistant says** field, click the ![iframe](images/iframe-response.png) **iframe** icon.

1. Add the full URL to the external content in the **iframe source** field.

    The URL must specify content that is embeddable in an HTML `iframe` element. Different sites have different restrictions for embedding content, and different processes for generating embeddable URLs. An embeddable URL is one that can be specified as the value of the `src` attribute of the `iframe` element.

    For example, to embed an interactive map using Google Maps, you can use the Google Maps Embed API. (For more information, see [The Maps Embed API overview](https://developers.google.com/maps/documentation/embed/get-started){: external}.) Other sites have different processes for creating embeddable content.

    For technical details about using `Content-Security-Policy: frame-src` to allow embedding of your website content, see [CSP: frame-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-src){: external}.

1. Optionally add a descriptive title in the **Title** field.

    In the web chat, this title will be displayed in the preview card that the customer clicks to render the external content. (If you do not specify a title, the web chat will attempt to retrieve metadata from the specified URL and display the title of the content as specified at the source.)

    References to variables are not supported.
    {: note}
    
#### Technical details: &lt;iframe&gt; sandboxing

Content loaded in an iframe by the web chat is _sandboxed_, meaning that it has restricted permissions that reduce security vulnerabilities. The web chat uses the `sandbox` attribute of the `iframe` element to grant only the following permissions:

| Permission          | Description |
|---------------------|-------------|
| `allow-downloads`   | Allows downloading files from the network, if the download is initiated by the user. |
| `allow-forms`       | Allows submitting forms. |
| `allow-scripts`     | Allows running scripts, but _not_ opening pop-up windows. |
| `allow-same-origin` | Allows the content to access its own data storage (such as cookies), and allows only very limited access to JavaScript APIs. |

A script running inside a sandboxed iframe cannot make changes to any content content outside the iframe, _if_ the outer page and the iframe have different origins. Be careful if you use an *iframe* response to embed content that has the same origin as the the page where your web chat widget is hosted; in this situation the embedded content can defeat the sandboxing and gain access to content outside the frame. For more information about this potential vulnerability, see the `sandbox` attribute [documentation](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe#attr-sandbox){: external}.
{: note}

