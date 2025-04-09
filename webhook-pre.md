---

copyright:
  years: 2019, 2025
lastupdated: "2025-04-09"

keywords: pre webhook, prewebhook, pre-webhook

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Making a call before processing a message
{: #webhook-pre}

A pre-message webhook makes a call to an external service or application every time a customer submits input. The external service can process the message before your assistant processes it.
{: shortdesc}

Add a pre-message webhook to your assistant if you want the webhook to be triggered before each incoming message is processed by your assistant.

If you are using a custom channel, the pre-message webhook works with the v2 `/message` API only (stateless and stateful). For more information, see the [API reference](https://cloud.ibm.com/apidocs/assistant-v2#message.). All built-in channel integrations use this API.
{: important}

You can use pre-message webhooks for the following use cases:

- Translate the customer's input to the language that your assistant uses.

- Check for and remove any personally identifiable information, such as an email address or social security number that a customer might submit.

You can use this webhook in coordination with the post-message webhook. For example, the post-message webhook can do things like translate the response back into the customer's language or add back information that was removed for privacy reasons. For more information, see [Making a call after processing a message](/docs/watson-assistant?topic=watson-assistant-webhook-post).

For environments where private endpoints are in use, keep in mind that a webhook sends traffic over the internet.{: note}

For the **classic experience**, use a dialog webhook if you need to perform a one-time action when needed during a conversation. For example, conditions are met when the assistant collects all required details, such as the account number, user ID, and account secret. For more information, see [Making a programmatic call from dialog](/docs/watson-assistant?topic=watson-assistant-dialog-webhooks#making-a-programmatic-call-from-dialog).

## Defining the webhook
{: #webhook-pre-create}

You can define one webhook URL to use for preprocessing every incoming message.

The programmatic call to the external service must meet these requirements:

- The call must be a POST HTTP request.

- The request body must be a JSON object (`Content-Type: application/json`).

- The call must return in 30 seconds or less.

If your external service supports GET requests only, or if you need to specify URL parameters dynamically at run time, consider creating an intermediate service that accepts a POST request with a JSON payload that contains any runtime values. The intermediate service can then make a request to the target service, passing these values as URL parameters, and then return the response to the dialog.
{: tip}

Do not set up and test your webhook in a production environment where the assistant is deployed and is interacting with customers.
{: important}

### Procedure

To add the webhook details, complete the following steps:

1. In your assistant, go to **Environments** and open the environment where you want to configure the webhook.

1. Click the ![Environment settings icon](images/gear-icon-black.png) icon to open the environment settings.

1. On the **Environment settings** page, click **Pre-message webhook**.

For the **classic experience**, complete the following steps:

- For the assistant that you want to configure, click the ![Overflow menu](images/overflow-menu--vertical.svg) icon, and then choose **Assistant settings**.

- Click **Webhooks** > **Pre-message webhook**.

1. Set the **Pre-message webhook** switch to **Enabled**.

1. In the **Synchronous event**, select from one of the following options:

  - Continue processing user input without webhook update if there is an error.

  - Return an error to the client if the webhook call fails.

For more information see, [Configuring webhook error handling for preprocessing](#configuring-webhook-error-handling-for-preprocessing).

1.  In the **URL** field, add the URL for the external application to which you want to send HTTP POST request callouts.

    For example, you might write a Cloud Functions web action that checks if a message is in a language other than English, and send it to the Language Translator service to convert it to English. Specify the URL for your web action, as in this example:

    ```text
    https://us-south.functions.cloud.ibm.com/api/v1/web/my_org_dev/default/translateToEnglish.json
    ```
    {: codeblock}

    You must specify a URL that uses the SSL protocol, so specify a URL that begins with `https`.

1. Fill in the **Secret field** for the **classic experience**. For more information, see [Adding a secret for the classic experience only](#adding-a-secret-for-the-classic-experience-only).

1. In the Timeout field, specify the time duration (in seconds) that you want the assistant to wait for a response from the webhook before it returns an error. The timeout duration cannot be shorter than 1 second or longer than 30 seconds.

1.  In the **Headers** section, click **Add header +** to add any headers that you want to pass to the service, one at a time.

If you are using the **classic experience**, the service automatically sends an authorization header with a JWT. If you want to handle the authorization yourself, add your own authorization header and the service uses it instead.{: note}

If the external application that you call returns a response, it might be able to send a response in different formats. The webhook requires that the response is formatted in JSON. The following table illustrates how to add a header to indicate that you want the resulting value to be returned is in JSON format.

| Header name    | Header value       |
|----------------|--------------------|
| `Content-Type` | `application/json` |
{: caption="Header example" caption-side="bottom"}

After you save the header value, the string is replaced by asterisks and can't be viewed again. 

Your webhook details are saved automatically.

#### Adding a secret for the classic experience only
{: add-secret-for-classic}

If you are using the **classic experience**, add a private key in the **Secret** field to pass with the request for authentication with the external service.

- Enter the key as a text string, such as `purple unicorn`.

- Use a maximum of 1,024 characters.

- Do not use context variables.

The external service is responsible for checking and verifying the secret. If no token is required, specify any string. This field cannot be left empty.

To view the secret as you enter it, click the **Show password** icon ![View icon](images/view.svg) before typing. After saving the secret, asterisks replace the string, and you can't view it again.
{: note}

For more information about how this field is used, see [Webhook security for the classic experience only](#webhook-security-for-the-classic-experience-only).

#### Configuring webhook error handling for preprocessing
{: configure-webhook-error-handling-pre}

You can decide whether an error returns in the preprocessing step if the webhook call fails. You have two options:

- **Continue processing user input without webhook update if there is an error**: The assistant ignores errors and processes the message without the webhook result. If preprocessing is useful but not essential, consider this option.

- **Return an error to the client if the webhook call fails**: If preprocessing is critical before the assistant processes a message, select this option.

When you enable **Return an error to the client if the webhook call fails**, everything stops until the preprocessing step is completed successfully.{: important}

Regularly test the external process to identify potential failures. If necessary, adjust this setting to prevent disruptions in the message processing.

### Testing the webhook

Do extensive testing of your webhook before you enable it for an assistant that is used in a production environment.
{: important}

The webhook is triggered when a message is sent to your assistant to be processed.

### Troubleshooting the webhook

The following error codes can help you track down the cause of issues you might encounter. If you have a web chat integration, for example, you know that your webhook has an issue if every test message you submit returns a message such as `There is an error with the message you just sent, but feel free to ask me something else`. If this message is displayed, use a REST API tool, such as cURL, to send a test `/message` API request, so you can see the error code and the full message that is returned.

| Error code and message | Description |
|------------|-------------|
| 422 Webhook responded with invalid JSON body | The webhook's HTTP response body could not be parsed as JSON. |
| 422 Error validating webhook response | The webhook's HTTP response body was not a valid `/message` body. |
| 422 Webhook responded with `[500]` status code | There's a problem with the external service that you called. The code failed or the external server refused the request. |
| 500 Processor Exception : `[connections to all backends failing]` | An error occurred in the webhook microservice. It could not connect to backend services. |
{: caption="Error code details" caption-side="bottom"}

### Webhook security for the classic experience only
{: webhook-pre-security-classic}

If you are using the **classic experience**, authenticate the webhook request by verifying the JSON Web Token (JWT) that is sent with the request. The webhook microservice automatically generates a JWT and sends it in the `Authorization` header with each webhook call.

 - For new webhooks or webhooks updated through **Edit authentication**, the authorization header is ignored.

 - For existing webhooks with a saved authentication header, the **Edit authentication** option is disabled.

 - Updating an existing webhook to use the new authentication configuration will change its behavior.

For more information, see [Defining the authentication method for pre-message and post-message webhooks](/docs/watson-assistant?topic=watson-assistant-define-webhook-auth).

If you need to test the JWT verification, you can add code to the external service. For example, if you specify `purple unicorn` in the **Secret** field, you can use the following code:

```javascript
const jwt = require('jsonwebtoken');
...
const token = request.headers.authentication; // grab the "Authentication" header
try {
  const decoded = jwt.verify(token, 'purple unicorn');
} catch(err) {
  // error thrown if token is invalid
}
```
{: codeblock}

### Request body

It is useful to know the format of the request body of the pre-message webhook so that your external code can process it.

The payload contains the request body of the `/message` (stateful or stateless) v2 API request. The event name `message_received` indicates that the request is generated by the pre-message webhook. For more information about the message request body, see the [API reference](https://cloud.ibm.com/apidocs/assistant-v2#message){: external}.

```json
{
  "payload" : { Copy of request body sent to /message }
  "event": {
      "name": "message_received"
   }
}
```
{: codeblock}

### Skipping the assistant processing for classic experience only
{: #webhook-pre-skipping-assistant-processing}

If you are using the **classic experience**, enhancements to pre-message webhooks allow {{site.data.keyword.conversationshort}} to skip message processing and directly return the response from the webhook. This functionality is activated by setting the `x-watson-assistant-webhook-returnheader` in the webhook's HTTP response.

#### Before you begin
{: #webhook-pre-before-you-begin}

For the **classic experience** complete the following steps:

 - Include the `x-watson-assistant-webhook-returnheader` with any value in the HTTP response from your webhook.
 - Ensure that the webhook response contains a valid message response, which is formatted according to the {{site.data.keyword.conversationshort}} requirements.

This feature enables the webhook to dynamically control the conversation flow, enabling immediate responses when needed.

### Response body

The service that receives the POST request from the webhook must return a JSON object (`Accept: application/json`).

The response body must have the following structure:

```json
{
  "payload": {
    ...
  }
}
```
{: codeblock}

The response `payload` must include the `payload` from the request body. Your code can modify property values or modify context variables, but the returned message payload must follow the `message` method schema. For more information, see [API reference](https://cloud.ibm.com/apidocs/assistant-v2#message).

### Example 1
{: #webhook-pre-example1}

This example shows you how to check the language of the input text, and append the language information to the input text string.

In the pre-message webhook configuration page, the following values are specified:

For the **classic experience**, there is no value in the **Secret** field.{: note}

- **URL**: `https://us-south.functions.appdomain.cloud/api/v1/web/e97d2516-5ce4-4fd9-9d05-acc3dd8ennn/default/check_language`
- **Header name**: Content-Type
- **Header value**: application/json

The pre-message webhook calls an IBM Cloud Functions web action name `check_language`.

The node.js code in the `check_language` web action looks as follows.

```javascript
let rp = require("request-promise");

function main(params) {
console.log(JSON.stringify(params))
if (params.payload.input.text !== '') {
  // Send a request to the Watson Language Translator service to check the language of the input text.
const options = { method: 'POST',
  url: 'https://api.us-south.language-translator.watson.cloud.ibm.com/instances/572b37be-09f4-4704-b693-3bc63869nnnn/v3/identify?version=2018-05-01',
  auth: {
           'username': 'apikey',
           'password': 'nnn'
       },
headers: {
    "Content-Type":"text/plain"
},
  body: [
          params.payload.input.text
  ],
  json: true,
};
     return rp(options)
    .then(res => {
        params.payload.context.skills["actions skill"].user_defined["language"] = res.languages[0].language;
        console.log(JSON.stringify(params))
        //Append "in" plus "the language code" to the input text, surrounded by parentheses.
        const response = {
            body : {
                payload : {
                    input : {
                        text : params.payload.input.text + ' ' + '(in ' + res.languages[0].language + ')'
                    },
                },
            },
        };
        return response;
})
}
return { 
    body : params
}
};
```
{: codeblock}

To test the webhook, click **Preview**. Submit the text `Buenos días`. The assistant probably can't understand the input, and returns the response from your *Anything else* node. However, if you go to the Analyze page of your assistant and open **Conversations**, you can see what was submitted. Check the most recent user conversation. The log shows that the user input is `Buenos días (in es)`. The `es` in parentheses represents the language code for Spanish, so the webhook worked and recognized that the submitted text was a Spanish phrase.

### Example 2
{: #webhook-pre-example-translate}

This example shows you how to check the language of the incoming message, and if it's not English, translate it into English before you submit it to the assistant.

Define a sequence of web actions in IBM Cloud Functions. The first action in the sequence checks the language of the incoming text. The second action in the sequence translates the text from its original language into English.

In the pre-message webhook configuration page, the following values are specified:

For the **classic experience**, there is no value in the **Secret** field.{: note}

- **URL**: `https://us-south.functions.appdomain.cloud/api/v1/web/e97d2516-5ce4-4fd9-9d05-acc3dd8ennn/default/translation_sequence`
- **Header name**: Content-Type
- **Header value**: application/json

The node.js code for the first web action in your sequence looks as follows:

```javascript
let rp = require("request-promise");

function main(params) {
console.log(JSON.stringify(params))
if (params.payload.input.text !== '') {
const options = { method: 'POST',
  url: 'https://api.us-south.language-translator.watson.cloud.ibm.com/instances/572b37be-09f4-4704-b693-3bc63869nnnn/v3/identify?version=2018-05-01',
  auth: {
           'username': 'apikey',
           'password': 'nnn'
       },
headers: {
    "Content-Type":"text/plain"
},
  body: [
          params.payload.input.text
  ],
  json: true,
};
     return rp(options)
    .then(res => {
      //Set the language property of the incoming message to the language that was identified by Watson Language Translator. 
        params.payload.context.skills["actions skill"].user_defined["language"] = res.languages[0].language;
        console.log(JSON.stringify(params))
        return params;
})
}
else {
    params.payload.context.skills["actions skill"].user_defined["language"] = 'none'
    return params
}
};
```
{: codeblock}

The second web action in the sequence sends the text to the Watson Language Translator service to translate the input text from the language that was identified in the previous web action into English. The translated string is then sent to your assistant instead of the original text.

The node.js code for the second action in your sequence looks as follows:

```javascript
let rp = require("request-promise");

function main(params) {
console.log(JSON.stringify(params))
//If the the incoming message is not null and is not English, translate it.
if ((params.payload.context.skills["actions skill"].user_defined.language !== 'en') && (params.payload.context.skills["actions skill"].user_defined.language !== 'none')) {
const options = { method: 'POST',
  url: 'https://api.us-south.language-translator.watson.cloud.ibm.com/instances/572b37be-09f4-4704-b693-3bc63869nnnn/v3/translate?version=2018-05-01',
  auth: {
           'username': 'apikey',
           'password': 'nnn'
       },
  headers: {
    "Content-Type":"application/json"
  },
       //The body includes the parameters that are required by the Language Translator service, the text to translate and the target language to translate it into.
  body: { 
      text: [ 
          params.payload.input.text
          ],
          target: 'en' 
  },
  json: true 
};
     return rp(options)
    .then(res => {
        params.payload.context.skills["actions skill"].user_defined["original_input"] = params.payload.input.text;
        const response = {
            body : {
                payload : {
                    "context" : params.payload.context,
                    "input" : {
                        "text" : res.translations[0].translation,
                        "options" : {
                            "export" : true
                            }
                    },
                },
            },
        };
    return response
})
}
return { 
    body : params
    }
};
```
{: codeblock}

When you test the webhook in the preview panel, you can submit `Buenos días`, and the assistant responds as if you said `Good morning` in English. In fact, when you check the Analyze page of your assistant and open **Conversations**, the log shows that the user input was `Good morning`.

You can add a post-message webhook to translate the message's response back into the customer's language before it is displayed. For more information, see [Example 2](/docs/watson-assistant?topic=watson-assistant-webhook-post#webhook-post-example-translate-back).

### Example 3
{: #webhook-pre-example3}

This example shows how to compose a webhook response to let {{site.data.keyword.conversationshort}} skip processing the message and directly return the webhook's response.

#### Webhook configuration

In the pre-message webhook configuration page, specify the following values:

For the **classic experience**, there is no value in the **Secret** field.{: note}

 - **URL**: https://your-webhook-url/webhook_skip
 - **Header Name**: Content-Type
 - **Header Value**: application/json

The node.js code in the webhook_skip web action looks as follows.

```javascript
function main(params) {
  // Your custom logic to determine the response
  let responseText = "This response is directly from the pre-message webhook.";

  const response = {
    headers: {
      "X-Watson-Assistant-Webhook-Return": "true"
    },
    body: {
      output: {
        generic: [
          {
            response_type: "text",
            text: responseText
          }
        ]
      }
    }
  };

  return response;
}
```
{: codeblock}

### Removing the webhook

If you decide that you do not want to preprocess customer input with a webhook, complete the following steps:

1. In your assistant, go to **Environments** and open the environment where you want to remove the webhook.

1. Click the ![Environment settings icon](images/gear-icon-black.png) icon to open the environment settings.

1. On the **Environment settings** page, click **Pre-message webhook**.

For the **classic experience**, complete the following steps:

- For the assistant that you want to configure, click the ![Overflow menu](images/overflow-menu--vertical.svg) icon, and then choose **Assistant settings**.

- Click **Webhooks** > **Pre-message webhook**.

1. Do one of the following steps:

  - To stop calling a webhook to process every incoming message, set the **Pre-message webhook** switch to **Disabled**.

  - To change the webhook that you want to call, click **Delete webhook**.
