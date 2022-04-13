---

copyright:
  years: 2019, 2022
lastupdated: "2022-03-28"

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

# Embedding the web chat on your page
{: #deploy-web-chat}

Add your assistant to your company website as a web chat widget that can help your customers with common questions and tasks, and can transfer customers to human agents.
{: shortdesc}

The web chat integration is automatically included for every assistant, and is configured separately for the draft and live environments. You can extensively customize the appearance and behavior of the web chat, but you can quickly add it to your website using the default configuration.

To add the web chat to your website, follow these steps:

1. Go to the ![Draft environment icon](images/draft-environment-icon.png) **Draft environment** or ![Live environment icon](images/live-environment-icon.png) page, depending on which environment you want to use.

1. In the **Channels** section, click the **Web chat** tile. The **Web chat** page opens, showing the settings for the web chat integration in the environment you are working in.

    The preview pane shows what the web chat will look like when it is embedded in a web page. If you see a message that starts with, `There is an error`, you probably haven't added any actions to your assistant yet. After you add an action, you can test the conversation from the preview pane.
    {: tip}

    ![Plus or higher plans only](images/plus.png) For environments where private endpoints are in use, keep in mind that the web chat integration sends traffic over the internet.
    <!--- For more information, see [Private network endpoints](/docs/assistant?topic=assistant-security#security-private-endpoints){: external}.
    {: note} --->

1.  Click the **Embed** tab.

    A code snippet is generated based on the web chat configuration. You (or a web developer) will add this code snippet to the web page where you want the web chat to appear.
    
    This code snippet contains an HTML `script` element. The script calls JavaScript code that is hosted on an IBM site. The code creates an instance of a widget that communicates with the assistant.
    
    Do not modify the `integrationID` or `region` property values.
    {: important}

1.  Click the ![Copy icon](images/copy-icon.png) **Copy to clipboard** icon to copy the embed script to the clipboard.

1.  Edit the HTML source for the web page where you want the web chat widget to appear. Paste the code snippet into the page. Paste the code as close as possible to the closing `</body>` tag to ensure that your page renders faster.

    If you want to quickly test the web chat in a local file, use this HTML code as the source for a test page:

    ```html
    <html>
    <head></head>
    <body>
        <title>My Test Page</title>
        <p>The body of my page.</p>
        <!-- copied script elements -->
        </body>
    </html>
    ```
    {: codeblock}

    Just copy this code into a file with the `.html` extension, and replace the `script` element with the embed script you copied in the previous step.

1.  If the system that hosts your website has limited Internet access (for example, if you use a proxy or firewall), make sure the following URLs are accessible:

    - `https://web-chat.global.assistant.watson.appdomain.cloud`: Hosts the code for the web chat widget, and is referenced by the script you embed on your website.
    - `https://integrations.{location}.assistant.watson.appdomain.cloud`: Hosts the web chat server, which handles communication with your assistant. Replace `{location}` with the location of the data center where your service instance is located, which is part of the service endpoint URL. For more information, see [Finding and updating the endpoint URL](/docs/watson?topic=watson-endpoint-change#endpoint-find-update){: external}.

1.  Open the web page (or local test file) in your browser. You should see the ![Web chat launcher icon](images/web-chat-icon.png).

1.  Click the launcher icon to open the chat window and talk to your assistant.

    ![Web chat window](images/web-chat-window.png)

    You can now test your assistant and see its responses just as your customers will see them.

1.  Paste the code snippet into each web page where you want the assistant to be available to your customers.

    You can paste the same script tag into as many pages on your website as you want. Add it anywhere where you want users to be able to reach your assistant for help. However, be sure to add it only one time per page.
    {: tip}
