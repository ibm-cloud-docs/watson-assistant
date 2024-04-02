---

copyright:
  years: 2019, 2024
lastupdated: "2024-04-02"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Embedding the web chat on your page
{: #deploy-web-chat}

To add the web chat widget to your website, you need to embed a generated script element in your HTML source.
{: shortdesc}

The web chat integration is automatically included for every assistant, and is configured separately for each environment.

For the webchat integration with a React-based application, see the alternative ways [here](https://github.com/watson-developer-cloud/assistant-web-chat-react).{: note}

To add the web chat to your website:

1. On the ![Integrations icon](images/integrations-icon.png) **Integrations** page, find the **Web chat** tile and click **Open**. The **Open web chat** window opens.

1. In the **Environment** field, select the environment you want the web chat widget to connect to. Click **Confirm**.

    The **Web chat** page opens, showing the settings for the web chat integration in the selected environment.

    The preview pane shows what the web chat will look like when embedded in a web page. If you see a message that starts with, `There is an error`, you probably haven't added any actions to your assistant yet. After you add an action, you can test the conversation from the preview pane.
    {: tip}

1.  Click the **Embed** tab.

    A code snippet is generated based on the web chat configuration. You (or a web developer) will add this code snippet to the web page where you want the web chat to appear.
    
    This code snippet contains an HTML `script` element. The script calls JavaScript code that is hosted on an IBM site and creates an instance of a widget that communicates with the assistant.
    
1.  Click the ![Copy icon](images/copy-icon.png) **Copy to clipboard** icon to copy the embed script to the clipboard.

1.  Edit the HTML source for the web page where you want the web chat widget to appear. Paste the code snippet into the page. Paste the code as close as possible to the closing `</body>` tag to ensure that your page renders faster.

    Do not modify the `integrationID` or `region` property values in the generated embed script.
    {: important}

    If you aren't ready to add the web chat to a live website, you can quickly test it using a local HTML file. Use this HTML code as the source for a test page:

    ```html
    <html>
    <head></head>
    <body>
        <title>My Test Page</title>
        <p>The body of my page.</p>
        &lt;!-- copied script elements --&gt;
        </body>
    </html>
    ```
    {: codeblock}

    Copy this code into a file with the `.html` extension, and replace the `script` element with the embed script you copied in the previous step.

    The identifiers in the embed script (such as `integrationID` `serviceInstanceID`) are not considered secret, and are visible to anyone who has access to your website. For more information, see [Security](/docs/watson-assistant?topic=watson-assistant-web-chat-architecture#web-chat-architecture-security).
    {: note}

1.  If the system that hosts your website has limited Internet access (for example, if you use a proxy or firewall), make sure the URLs that host the web chat are accessible. For more information, see [Access to web chat hosts](/docs/watson-assistant?topic=watson-assistant-web-chat-architecture#web-chat-hosts).

1.  Open the web page (or local test file) in your browser. You should see the launcher icon displayed on the page:

    ![Web chat launcher icon](images/web-chat-icon.png) 

1.  Click the launcher icon to open the chat window.

    ![Web chat window](images/home-screen.png)

1.  Paste the same embed script into each web page where you want the assistant to be available to your customers.

    You can paste the same script tag into as many pages on your website as you want. Add it anywhere where you want users to be able to reach your assistant for help. However, be sure to add it only once on each page.
    {: tip}

You can now test your assistant and see its responses just as your customers would.

Before you go to production with the web chat, however, you will probably want to customize it for your site and for the needs of your customers. For more information, see [Web chat development overview](/docs/watson-assistant?topic=watson-assistant-web-chat-develop).
