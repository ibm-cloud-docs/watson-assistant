---

copyright:
  years: 2019, 2023
lastupdated: "2023-09-27"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Making a programmatic call from dialog
{: #dialog-webhooks}

To make a programmatic call, define a webhook that sends a POST request callout to an external application that performs a programmatic function. You can then start the webhook from one or more dialog nodes.

If you are using actions instead of dialog, you can use a custom extension to make programmatic calls. For more information, see [Calling a custom extension](/docs/watson-assistant?topic=watson-assistant-call-extension).
{: note}

A webhook is a mechanism that you can use to call out to an external program based on an event in your program. When used in a dialog, a webhook is triggered when the assistant processes a node with a webhook that is enabled. The webhook collects data that you specify or that you collect from the user during the conversation and save in context variables. It sends the data as part of an HTTP POST request to the URL that you specify as part of your webhook definition. The URL that receives the webhook is the listener. It performs a predefined action that uses the information that you pass to it as specified in the webhook definition, and can optionally return a response.

You can use a webhook to do the following types of things:

- Validate information that you collected from the user.
- Interact with an external web service to get information. For example, you might check on the expected arrival time for a flight from an air traffic service or get a forecast from a weather service.
- Send requests to an external application, such as a restaurant reservation site, to complete a simple transaction on the user's behalf.
- Trigger an SMS notification.
- Trigger an {{site.data.keyword.openwhisk}} web action.

You cannot use a webhook to call a {{site.data.keyword.openwhisk_short}} action that uses token-based Identity and Access Management (IAM) authentication. However, you can make a call to a secured {{site.data.keyword.openwhisk_short}} web action. For more information, see [Calling an {{site.data.keyword.openwhisk}} web action](#dialog-webhooks-cf-web-action).
{: important}

For information about how to call a client application, see [Requesting client actions](/docs/watson-assistant?topic=watson-assistant-dialog-actions-client).

For environments where private endpoints are in use, keep in mind that a webhook sends traffic over the internet.
{: note}

## Defining the webhook
{: #dialog-webhooks-create}

You can define one webhook URL for a dialog, and then call the webhook from one or more dialog nodes.

The programmatic call to the external service must meet these requirements:

- The call must be a POST HTTP request.
- The request body must be a JSON object (`Content-Type: application/json`).
- The response must be a JSON object (`Accept: application/json`).
- The call must return in 8 seconds or less. If started more than once in a single message call through [dialog nodes](#dialog-webhooks-dialog-node-callout), all of those invocations must return in 8 seconds or less.

If your external service supports GET requests only, or if you need to specify URL parameters dynamically at run time, consider creating an intermediate service that accepts a POST request with a JSON payload that contains any runtime values. The intermediate service can then make a request to the target service, passing these values as URL parameters, and then return the response to the dialog.
{: tip}

If you need to call a service that might not return within 8 seconds, you can manage the call through a custom client application and pass the information to the dialog as a separate step. For more information, see [Requesting client actions](/docs/watson-assistant?topic=watson-assistant-dialog-actions-client).
{: tip}

To add the webhook details, complete the following steps:

1. In the dialog where you want to add the webhook, click **Webhooks**.

1. In the **URL** field, add the URL for the external application to which you want to send HTTP POST request callouts.

   For example, to call the {{site.data.keyword.languagetranslationshort}} service, specify the URL for your service instance.

   ```bash
   https://api.us-south.language-translator.watson.cloud.ibm.com/v3/translate?version=2018-05-01
   ```
   {: codeblock}

   If the external application that you call returns a response, it must be able to send back a response in JSON format. For the {{site.data.keyword.languagetranslationshort}} service, for example, you must specify the format in which you want the result to be returned. You can do so by passing a header to the service.

1. In the Headers section, add any headers that you want to pass to the service one at a time by clicking **Add header**.

   For example, this header indicates that the request is in JSON format.

   | Header name    | Header value       |
   |----------------|--------------------|
   | `Content-Type` | `application/json` |
   {: caption="Header example" caption-side="bottom"}
      
1. If the external service requires that you pass basic authentication credentials with the request, then provide them. Click **Add authorization**, add your credentials to the **User name** and **Password** fields, and then click **Save**. 

   The product creates a base-64 encoded ASCII string from the credentials and generates a header that it adds to the page for you. 
   | Header name    | Header value       |
   |----------------|--------------------|
   | Authorization | Basic `<encoded-credentials>` |
   {: caption="Header example" caption-side="bottom"}

   If you use the web chat integration and enable security, you can use the same token that you use to secure the web chat in the Authorization header. For more information, see [Web chat: Reusing the JWT for webhook authentication](/docs/watson-assistant?topic=watson-assistant-dialog-integrations#dialog-integrations-chat-jwt).
   {: tip}

Your webhook details are saved automatically.

## Adding a webhook callout to a dialog node
{: #dialog-webhooks-dialog-node-callout}

To use a webhook from a dialog node, you must enable webhooks on the node, and then add details for the callout.

1. Find the dialog node where you want to add a callout. The callout to the webhook occurs whenever this node is triggered during a conversation with a user.

   For example, you might want to send a callout to the webhook from the `#General_Greetings` node.

1. Click to open the dialog node, and then click **Customize**.

1. Scroll down to the webhook section. Set the **Call out to webhooks / actions** switch to **On**.

1. Select **Call a webhook**, and then click **Apply**.

   If you did not have it enabled already, the **Multiple conditioned responses** switch is set to **On** automatically and you cannot disable it. This setting is enabled to support adding different responses depending on the success or failure of the webhook call. If you have a response that is specified for the node already, it becomes the first conditional response.
   {: note}

1. Add any data that you want to pass to the external application as key and value pairs in the *Parameters* section.

   Parameters are passed as request body properties. You cannot specify query parameters or URL parameters in a dialog node. These parameters can be configured with static values only as part of the webhook definition. For more information, see [Defining the webhook](https://cloud.ibm.com/docs/assistant?topic=assistant-dialog-webhooks#dialog-webhooks-create).
   {: note}

   For example, if you call the Language Translator service, you must provide values for the following parameters:
   
   | Key | Value | Description | 
   | --- | --- | --- |
   | model_id | "en-es" | Identifies the input and output languages. In this example, the request is for text in English (en) to be translated into Spanish (es). | 
   | text | "How are you?" | This parameter contains the text string that you want the service to translate. You can hardcode this value, pass a context variable, such as $saved_text, or pass the user input to the service directly, by specifying `<? input.text ?>` as this value. |
   {: caption="Parameter example" caption-side="bottom"}

   In more complex use cases, you might collect information during a conversation with a user about their travel plans, for example. You can collect dates and destination information and save it in context variables that you can pass to an external application as parameters.
  
   | Key | Value |
   | --- | --- | 
   | depart_date | $departure | 
   | arrive_date | $arrival | 
   | origin | $origin | 
   | destination | $destination | 
   {: caption="Travel parameters example" caption-side="bottom"}

1. Any response that is made by the callout is saved to the return variable. You can rename the variable that is automatically added to the **Return variable** field for you. If the callout results in an error, this variable is set to `null`.

   The generated variable name has the syntax `webhook_result_n`, where the `_n` suffix is incremented each time that you add a webhook callout to a dialog node. This naming convention ensures that context variable names are unique across the dialog. If you change the name, be sure to use a unique name.

1. In the conditional responses section, two response conditions are added automatically, one response to show when the webhook callout is successful and a return variable is sent back. And one response to show when the callout fails. You can edit these responses, and add more conditional responses to the node.

   - If the callout returns a response, and you know the format of the JSON response, then you can edit the dialog node response to include only the section of the response that you want to share with users. 
   
      For example, the Language Translator service returns an object like this:
    
      ```json
         {
         "translations":[
            {"translation":"¿Cómo estás?"}
         ],
         "word_count":3,
         "character_count":12
         }
      ```
      {: codeblock}
    
      Use a SpEL expression that extracts only the translated text value.

      | Condition | Response | 
      | --- | --- |
      | $webhook_result_1 | Your words in Spanish: <? $webhook_result_1.translations[0].translation ?>. | 
      | anything_else | The call to the external application failed. Please try again later. | 
      {: caption="Conditional responses example" caption-side="bottom"}

      If you use the recommended format for the response and the translation response that is shown earlier is returned, the assistant's response to the user would be: `Your words in Spanish: ¿Cómo estás?`

   - If you want to provide a specific response if the callout returns an empty string, meaning the call is successful, but the value that is returned is an empty string, you can add a conditional response that has a condition with syntax like this:
   
      ```text
      $webhook_result_1.size() == 0
      ```
      {: codeblock}

1. When you are done, click the X to close the node. Your changes are automatically saved.

## Testing webhooks
{: #dialog-webhooks-test}

When you first add a webhook callout, it can be useful to see exactly what is returned in the response from the external application, the data, and its format. Add this expression as the text response for the successful callout conditional response: `$webhook_result_n` where `n` is the appropriate number for the webhook that you are testing.

This response returns the full body of the return variable, so you can see what the callout is sending back and decide what to share with the user. You can then use the methods that are documented in [Expression language methods](/docs/watson-assistant?topic=watson-assistant-dialog-methods) to extract only the information you care about from the response.

Test whether certain user inputs can generate errors in the callout, and build in ways to handle those situations. Errors that are generated by the external application are stored in `output.webhook_error.<result_variable>`. You can use a conditional response like this while you are testing to capture such errors:

| Condition | Response |
|-----------|----------|
| output.webhook_error | The callout generated this error: `<? output.webhook_error.webhook_result_1 ?>` |
{: caption="Conditional response example" caption-side="bottom"}

For example, you might not be authenticating the request properly (401), or you might be trying to pass a parameter with a name that is already in use by the external application. Test the webhook to discover and fix these types of errors before you deploy the webhook.

## Removing a webhook
{: #dialog-webhooks-delete}

If you decide you do not want to make a webhook call from a dialog node, open the node's *Customize* page, and then switch Webhooks **Off**.

The *Parameters* section and the **Return variable** field are removed from the dialog node editor. However, any conditional responses that were added for you or that you added yourself remain.

The *Multiple conditioned responses* section is editable again. You can choose to switch off the feature. If you do so, then only the first conditional response is saved as the node's only text response.

To change the external service that you call from dialog nodes, edit the webhook details defined on the Webhooks page of the **Options** tab. If the new service expects different parameters to be passed to it, be sure to update any dialog nodes that call it.

## Calling an {{site.data.keyword.openwhisk}} web action
{: #dialog-webhooks-cf-web-action}

Typically, web actions can be run without requiring the caller to authenticate first. However, you can secure a web action that requires any callers to pass an ID with the request. For more information about how to secure a web action, see [Securing web actions](/docs/openwhisk?topic=openwhisk-actions_web#actions_web_secure){: external}.

Use the following tips when you call a {{site.data.keyword.openwhisk_short}} web action from your dialog. 

1. In the dialog, click **Webhooks**.

1. In the **URL** field, add the URL for the external application to which you want to send HTTP POST request callouts.

    For example, to call a {{site.data.keyword.openwhisk_short}} web action, specify the URL for the public web action. For example:

    ```bash
    https://us-south.functions.cloud.ibm.com/api/v1/web/my_org_dev/default/Hello%20World.json
    ```
    {: codeblock}

    If the external application that you call returns a response, it must be able to send back a response in JSON format.

    Notice the request URL in this example ends in `.json`. By specifying this extension, you take advantage of a feature of web actions where you can specify the content type of the response. Specifying this extension type ensures that, if the web actions can return responses in more than one format, a JSON response is returned. For more information, see [Content extensions](https://cloud.ibm.com/docs/openwhisk?topic=openwhisk-actions_web#extra_features){: external}.
    {: tip}

1. If the web action is secured, specify any headers, such as `X-Require-Whisk-Auth`, that are required to call the web action.

   | Header name | Header value | 
   | --- | --- | 
   | `X-Require-Whisk-Auth` | `{my-secret}` | 
   {: caption="Header example" caption-side="bottom"}

1. Click to open the dialog node, and then click **Customize**.

1. Scroll down to the webhook section. Set the **Call out to webhooks / actions** switch to **On**.

1. Select **Call a webhook**, and then click **Apply**.

1. Add any data that you want to pass to the external application as key and value pairs in the *Parameters* section.

    For example, if you call the Hello World {{site.data.keyword.openwhisk_short}} web action, you might want to add the following information to pass in the message parameter that is accepted by that application:
    
    | Key | Value | 
    | --- | --- | 
    | message "hello" | 
    {: caption="Parameter example" caption-side="bottom"}

    When you call a {{site.data.keyword.openwhisk_short}} web action, you cannot pass parameters with the same key as parameters that are defined as part of the web action. See [Protected parameters](/docs/openwhisk?topic=openwhisk-actions_web#actions_web_protect_parameters){: external} for more details.
    {: note}

1. You can edit the dialog node response to include only the section of the response that you want to display to users.

   The Hello World {{site.data.keyword.openwhisk_short}} web action includes a message name and value pair in its response, along with other information. To show only the content of the message, you can use `<return-variable>.message` syntax to extract the message section only from the response object.

   | Condition | Response |
   | --- | --- | 
   | $webhook_result_1 | The application returned "$webhook_result_1.message". | 
   | anything_else | The call to the external application failed. Please try again later. | 
   {: caption="Parameter example" caption-side="bottom"}

1. When you are done, click the X to close the node. Your changes are automatically saved.

## Updating output.generic with a webhook
{: #dialog-webhooks-outputgeneric}

You can use a webhook to update `output.generic` and provide dynamic responses. For more information, see the blog article [How to Dynamically Add Response Options to Dialog Nodes in Watson Assistant](https://medium.com/ibm-data-ai/how-to-dynamically-add-response-options-to-dialog-nodes-in-watson-assistant-e14c5e08beca){: external}.
