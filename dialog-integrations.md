---

copyright:
  years: 2015, 2023
lastupdated: "2023-10-26"

keywords: integration settings

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Adding custom dialog flows for integrations
{: #dialog-integrations}

Use the JSON editor in dialog to access information that is submitted from the web chat integration.
{: shortdesc}

Starting with API version `2020-04-01`, the `context` object that is passed as part of the v2 `/message` API request contains an `integrations` object. This object makes it possible to pass information that is specific to a single integration type in the context. For more information, see [Context variables](/docs/watson-assistant?topic=watson-assistant-dialog-runtime-context#dialog-runtime-context-variables).

The `integrations` object is available in the v2 API in version `2020-04-01` or later only.
{: important} 

To take advantage of the `context.integrations` object, you can create context variables that are named as follows to get and set values for different integrations:

| Integration type | Context variable syntax |
|------------------|-------------------------|
| Phone | `$integrations.voice_telephony` |
| Salesforce service desk from web chat | `$integrations.salesforce` |
| SMS with Twilio | `$integrations.text_messaging` |
| Web chat (and assistant preview) | `$integrations.chat` |
| Zendesk service desk from web chat | `$integrations.zendesk` |
{: caption="Integration-specific context variables" caption-side="bottom"}

## Building integration-specific dialog flow
{: #dialog-integrations-condition-by-type}

Create a single dialog that is optimized to use the best features that are offered by each channel or client interface in which it is deployed.

You can customize the conversation in the following ways:

- To add an entire dialog branch that is only processed by a specific integration type, add the appropriate integration type context variable, such as `$integrations.chat`, to the *If assistant recognizes* field of the dialog root node.
- To add a single dialog node that is only processed by a specific integration type, add the appropriate integration type context variable, such as `$integrations.zendesk`, to the *If assistant recognizes* field of the dialog child node.
- To add slightly different responses for a single dialog node based on the integration type, complete the following steps:

   - From the node's edit view, click **Customize** and then set the *Multiple conditioned responses* switch to **On**. Click **Apply**.
   
   - In the dialog node response section, add the appropriate condition and corresponding response for each custom response type.

      The following examples show how to specify a hypertext link in the best format for the integration where the text response is displayed. For the *Web chat* integration, which supports Markdown formatting, you can include a link label in the response text to make the response look nicer. For the *SMS with Twilio* integration, you can skip the formatting that makes sense in a web page, and add the straight URL.

      | Integration type | Condition | Sample text response |
      | --- | --- | --- |
      | SMS with Twilio | `$integrations.text_messaging` | `For more information, go to https://www.ibm.com.` |
      | Web chat |  `$integrations.chat` | `For more information, go to [the ibm.com site](https://www.ibm.com).` |
      | Response to show if no other conditions are met. | `true` | `For more information, go to ibm.com.` |
      {: caption="Custom conditioned responses" caption-side="bottom"}

The rich response types often behave differently when they are displayed in different built-in integrations or in the assistant preview.

If you need to provide customized responses for different channels, and you do not need to modify your dialog flow based on which integration is in use, you can also use the `channels` array to target your responses to specific integrations.
{: note}

## Web chat: Accessing sensitive data
{: #dialog-integrations-chat-private}

If you enable security for the web chat, you can configure your web chat implementation to send encrypted data to the dialog. Payload data that is sent from web chat is stored in a private context variable named `context.integrations.chat.private.user_payload`. No private variables are sent from the dialog to any integrations. For more information about how to pass data, see [Encrypting sensitive data in web chat](/docs/watson-assistant?topic=watson-assistant-web-chat-security-encrypt).

To access the payload data, you can reference the `context.integrations.chat.private.user_payload` object from the dialog node condition. 

You must know the structure of the JSON object that is sent in the payload.
{: note}

For example, if you passed the value `"mvp:true"` in the JSON payload, you can add a dialog flow that checks for this value to define a response that is meant for VIP customers only. Add a dialog node with a condition like this:

| Field | Value |
|-------|-------|
| If assistant recognizes | `$integrations.chat.private.user_payload.mvp` |
| Assistant responds | `I can help you reserve box seats at the upcoming conference!` |
{: caption="Private variable as node condition" caption-side="bottom"}

## Web chat: Accessing web browser information
{: #dialog-integrations-chat-browser-info}

When you use the web chat integration, information about the web browser that your customer is using to access the web chat is automatically collected and stored. The information is stored in the `context.integrations.chat.browser_info` object. 

You can design your dialog to take advantage of details about the web browser in use. The following properties are taken from the `window` object that represents the window in which the web chat is running:

- `browser_name`: The browser name, such as `chrome`, `edge`, or `firefox`.
- `browser_version`: The browser version, such as `80.0.0`.
- `browser_OS`: The operating system of the customer's computer, such as `Mac OS`.
- `language`: The default locale code of the browser, such as `en-US`.
- `page_url`: Full URL of the web page in which the web chat is embedded. For example,: `https://www.example.com/products`
- `screen_resolution`: Specifies the height and width of the browser window in which the web page is displayed. For example,: `width: 1440, height: 900`
- `user_agent`: Content from the User-Agent request header. For example,: `Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:80.0) Gecko/20100101 Firefox/80.0`
- `client_ip_address`: IP address of the customer's computer. For example,: `183.49.92.42`

### Example: Using page URL information in your dialog
{: #dialog-integrations-chat-browser-info-example}

You might embed the web chat in multiple pages on your website. Perhaps you want to route chat transfers from the web chat to different Salesforce agents based on the page from which the customer asks to speak to someone. If the customer is on the insurance plans page of your website (`https://www.example.com/insurance.html`), you want to route them to agents who are experts in your company's insurance plans. If the customer is on the investments web page (`https://www.example.com/invest.html`), you want to route them to agents who are experts in your company's investment opportunities. You can add multiple conditioned responses to the dialog node where the transfer takes place and add logic like this:

**Conditioned response 1**

- Condition: `$integrations.chat.browser_info.page_url.contains('insurance.html')`
- Response type: *Connect to human agent*
- Button ID: `Z23453e25vv` (The button that routes to the insurance experts agent queue)

**Conditioned response 2**

- Condition: `$integrations.chat.browser_info.page_url.contains('invest.html')`
- Response type: *Connect to human agent*
- Button ID: `Z23453j24ty` (The button that routes to the investment experts agent queue)

## Web chat: Reusing the JWT for webhook authentication
{: #dialog-integrations-chat-jwt}

You can use the same JSON Web Token (JWT) that was used to secure your web chat to authenticate webhook calls. If you specify a token in the `identityToken` property when you add the web chat to your web page, the token is stored in a private variable named `context.integrations.chat.private.jwt`. For more information about passing a JWT, see [Enabling web chat security](/docs/watson-assistant?topic=watson-assistant-web-chat-security-enable).

1. In your dialog, open **Webhooks**.

1. Click **Add header**. 

1. In **Header name**, enter any name, such as `JWT`.

1. In the **Header value** field, add `$integrations.chat.private.jwt`.
