---

copyright:
  years: 2019, 2025
lastupdated: "2025-06-09"

keywords: post webhook, postwebhook, post-webhook

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Making a call after processing a message
{: #webhook-post}

A post-message webhook calls an external service or application every time that the assistant renders a response. The external service can process the assistant's output before it is sent to the channel.
{: shortdesc}

You can add a post-message webhook to your assistant if you want to trigger the webhook before each message response is shown to the customer.

You can use a post-message webhook to do things like extract custom responses from an external content repository. For example, you can define actions with custom IDs in the responses instead of text. The post-message webhook can pass these IDs to an external database to retrieve stored text responses.

You can use this webhook in coordination with the pre-message webhook. For example, if you use the pre-message webhook to strip personally identifiable information from the customer's input, you can use the post-message webhook to add it back. If you use the pre-message webhook to translate the customer's input to the assistant's language, you can use the post-message webhook to translate the response into the customer's language before returning it. For more information, see [Making a call before processing a message](/docs/watson-assistant?topic=watson-assistant-webhook-pre).

For environments where private endpoints are in use, keep in mind that a webhook sends traffic over the internet.
{: note}

For the **Classic experience**, use a dialog webhook if you need to perform a one-time action when needed during a conversation. For example, conditions are met when the assistant collects all required details, such as the account number, user ID, and account secret. For more information, see [Making a programmatic call from dialog](/docs/watson-assistant?topic=watson-assistant-dialog-webhooks#dialog-webhooks).

## Defining the webhook
{: #webhook-post-create}

You can define one webhook URL to use for processing every message response before it is sent to the channel and shown to the customer.

The programmatic call to the external service must meet these requirements:

- The call must be a POST HTTP request.
- The call must be completed in 30 seconds or less.
- The format of the request and response must be in JSON. For example, `Content-Type: application/json`.

Do not set up and test your webhook in a production environment where the assistant is deployed and is interacting with customers.
{: important}

### Procedure
{: #webhook-post-procedure}

To add the webhook details, complete the following steps:

1. In your assistant, go to **Environments** and open the environment where you want to configure the webhook.

1. Click the ![Environment settings icon](images/gear-icon-black.png) icon to open the environment settings.

1. On the **Environment settings** page, click **Post-message webhook**.

   For the **Classic experience**, complete the following steps:

    - For the assistant that you want to configure, click the ![Overflow menu](images/overflow-menu--vertical.svg) icon, and then choose **Settings**.

    - Click **Webhooks** > **Post-message webhook**.

1. Set the **Post-message webhook** switch to **Enabled**.

1. In the **Synchronous event**, select from one of the following options:

   - Continue processing user input without webhook update if there is an error.

   - Return an error to the client if the webhook call fails.

   For more information see, [Configuring webhook error handling for postprocessing](#configure-webhook-error-handling-post).

1.  In the **URL** field, add the URL for the external application to which you want to send HTTP POST request callouts.

    For example, maybe you store your assistant's responses in a separate content management system. When the assistant understands the input, the processed action returns a unique ID that corresponds to a response in your CMS. To call a service that retrieves a response from your CMS for a given unique ID, specify the URL for your service instance. For example, `https://example.com/get_answer`.

    You must specify a URL that uses the SSL protocol, so specify a URL that begins with `https`.

1.  To configure the authentication for post-message webhooks, click **Edit authentication**. For detailed instructions, see [Defining the authentication method for pre-message and post-message webhooks](/docs/watson-assistant?topic=watson-assistant-define-webhook-auth). 

    - For the **Classic experience**, fill in the **Secret field**. For more information, see [Adding a secret for the Classic experience only](#add-secret-for-classic-webhook-post).

1. In the **Timeout** field, specify the time duration (in seconds) that you want the assistant to wait for a response from the webhook before it returns an error. The timeout duration cannot be shorter than 1 second or longer than 30 seconds.

1.  In the **Headers** section, click **Add header +** to add any headers that you want to pass to the service, one at a time.

    For the **Classic experience**, the service automatically sends an Authorization header with a JWT. If you want to handle authorization yourself, add your own authorization header and the service uses it instead.{: note}

    If the external application that you call returns a response, it might be able to send a response in different formats. The webhook requires that the response is formatted in JSON. The following table illustrates how to add a header to indicate that you want the resulting value to be returned is in JSON format.

    | Header name    | Header value       |
    |----------------|--------------------|
    | `Content-Type` | `application/json` |
    {: caption="Header example" caption-side="bottom"}

1. After you save the header value, the string is replaced by asterisks and can't be viewed again. 

1. Your webhook details are saved automatically.

#### Adding a secret for the Classic experience only
{: #add-secret-for-classic-webhook-post}

For the **Classic experience**, add a private key in the **Secret** field to pass with the request for authentication with the external service:

- Enter the key as a text string, such as `purple unicorn`.

- Use a maximum of 1,024 characters.

- Do not use context variables.

The external service is responsible for checking and verifying the secret. If no token is required, specify any string. This field cannot be left empty.

To view the secret as you enter it, click the **Show password** icon ![View icon](images/view.svg) before typing. After saving the secret, asterisks replace the string, and you can't view it again.
{: note}

For more information about how this field is used, see [Webhook security for the Classic experience only](#webhook-post-security-classic).

#### Configuring webhook error handling for postprocessing
{: #configure-webhook-error-handling-post}

You can decide whether an error returns in the preprocessing step if the webhook call fails. You have two options:

- **Continue processing user input without webhook update if there is an error**: The assistant ignores the errors and processes the message without the webhook result. If postprocessing is useful but not essential, consider this option.

- **Return an error to the client if the webhook call fails**: If postprocessing is critical after the assistant sends a response, select this option.

When you enable **Return an error to the client if the webhook call fails**, everything stops until the postprocessing step is completed successfully.{: important}

Regularly test the external process to identify potential failures. If necessary, adjust this setting to prevent disruptions in the response processing.

### Testing the webhook
{: #webhook-post-testing}

Do extensive testing of your webhook before you enable it for an assistant that is used in a production environment.
{: important}

The webhook is triggered only when your assistant processes a message and a response is ready to be returned to the channel.

### Troubleshooting the webhook
{: #webhook-post-troubleshooting}

The following error codes can help you track down the cause of issues you might encounter. If you have a web chat integration, for example, you know that your webhook has an issue if every test message you submit returns a message such as `There is an error with the message you just sent, but feel free to ask me something else`. If this message is displayed, use a REST API tool, such as cURL, to send a test `/message` API request, so you can see the error code and the full message that is returned.

| Error code and message | Description |
|------------|-------------|
| 422 Webhook responded with invalid JSON body | The webhook's HTTP response body could not be parsed as JSON. |
| 422 Webhook responded with `[500]` status code | A problem occurred with the external service that you called. The code failed or the external server refused the request. |
| 500 Processor Exception : `[connections to all backends failing]` | An error occurred in the webhook microservice. It could not connect to backend services. |
{: caption="Error code details" caption-side="bottom"}

### Webhook security for the Classic experience only
{: #webhook-post-security-classic}

For the **Classic experience**, authenticate the webhook request by verifying the JSON Web Token (JWT) that is sent with the request. The webhook microservice automatically generates a JWT and sends it in the `Authorization` header with each webhook call:

 - For new webhooks or webhooks updated through **Edit authentication**, the authorization header is ignored.

 - For existing webhooks with a saved authentication header, the **Edit authentication** button is disabled.

 - Updating an existing webhook to use the new authentication configuration will change its behavior.

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

### Example request body
{: #webhook-post-request-body-example}

It is useful to know the format of the request post-message webhook body so that your external code can process it.

The payload contains the response body that your assistant returns for the v2 `/message` (stateful and stateless) API call. The event name `message_processed` indicates that the post-message webhook generates the request. For more information about the message request body, see the [API reference](https://cloud.ibm.com/apidocs/assistant-v2#message){: external}.

The following sample shows how a simple request body is formatted:

```json
{
 "event": {
    "name": "message_processed"
},
"options": {},
"payload": {
    "output": {
        "intents": [
            {
                "intent": "General_Greetings",
                "confidence": 1
            }
        ],
        "entities": [],
        "generic": [
            {
                "response_type": "text",
                "text": "Hello. Good evening"
            }
        ]
    },
    "user_id": "test user",
    "context": {
        "global": {
            "system": {
                "user_id": "test user",
                "turn_count": 11
            },
            "session_id": "sxxx"
        },
        "skills": {
            "actions skill": {
                "user_defined": {
                    "var": "anthony"
                },
                "system": {
                    "state": "nnn"
                }
            }
        }
    }
}
```
{: codeblock}

### Skipping the assistant processing

Enhancements to pre-message webhooks allow {{site.data.keyword.conversationshort}} to skip message processing and directly return the response from the webhook. This functionality is activated by setting the `x-watson-assistant-webhook-returnheader` in the webhook's HTTP response.

#### Before you begin
{: #webhook-post-before-you-begin}

Complete the following steps:

 - Include the `x-watson-assistant-webhook-returnheader` with any value in the HTTP response from your webhook.

 - Ensure that the webhook response contains a valid message response, which is formatted according to {{site.data.keyword.conversationshort}}'s requirements.

This feature enables the webhook to dynamically control the conversation flow, enabling immediate responses when needed.

#### Response body
{: #webhook-post-response-body}

In the response body, the `output` does not need to be wrapped inside a `payload` property as it is returned directly to the client:

```javascript
{
    "output": {
      "generic": [
        {
          "response_type": "text",
          "text": "This response is directly from the pre-message webhook."
        }
      ]
    }
}
```
{: codeblock}

For a practical implementation of this feature, see [Example 3](#webhook-post-example-3).

### Example 1
{: #webhook-post-example1}

This example shows how to add `y'all` to the end of each response from the assistant.

In the post-message webhook configuration page, the following values are specified:

For the **Classic experience**, there is no value in the **Secret** field.{: note}

- **URL**: `https://your-webhook-url/`
- **Header name**: Content-Type
- **Header value**: application/json

The post-message webhook calls an IBM Cloud Functions web action name `add_southern_charm`.

The node.js code in the `add_southern_charm` web action looks as follows:

```javascript
function main(params) {
  console.log(JSON.stringify(params))
  if (params.payload.output.generic[0].text !== '') {
      //Get the length of the input text
        var length = params.payload.output.generic[0].text.length;
        //create a substring that removes the last character from the input string, which is typically punctuation.
        var revision = params.payload.output.generic[0].text.substring(0,length-1);
        const response = {
            body : {
                payload : {
                    output : {
                        generic : [
                              {
                                  //Replace the input text with your shortened revision and append y'all to it.
                                "response_type": "text",
                                "text": revision + ', ' + 'y\'all.'
                              }
                        ],
                    },
                },
            },
        };
        return response;
  }
  else {
    return { 
        body : params
    }
  }
}
```
{: codeblock}

### Example 2
{: #webhook-post-example-translate-back}

This example shows how to translate a message response back to the customer's language. It works only if you perform the steps in [Example 2](/docs/watson-assistant?topic=watson-assistant-webhook-pre#webhook-pre-example-translate) to define a pre-message webhook that translates the original message into English.

Define a sequence of web actions in IBM Cloud Functions. The first action in the sequence checks for the language of the original incoming text, which you stored in a context variable named `original_input` in the pre-message webhook code. The second action in the sequence translates the dialog response text from English into the original language that was used by the customer.

In the pre-message webhook configuration page, the following values are specified:

For the **Classic experience**, there is no value in the **Secret** field.{: note}

- **URL**: `https://your-webhook-url/`
- **Header name**: Content-Type
- **Header value**: application/json

The node.js code for the first web action in your sequence looks as follows:

```javascript
let rp = require("request-promise");

function main(params) {
console.log(JSON.stringify(params))

if (params.payload.output.generic[0].text !== '') {
const options = { method: 'POST',
  url: 'https://api.us-south.language-translator.watson.cloud.ibm.com/instances/572b37be-09f4-4704-b693-3bc63869nnnn/v3/identify?version=2018-05-01',
  auth: {
           'username': 'apikey',
           'password': 'nnnn'
       },
  headers: {
    "Content-Type":"text/plain"
},
  body: [
          params.payload.context.skills['actions skill'].user_defined.original_input
  ],
  json: true,
};
     return rp(options)
    .then(res => {
      //Set the language property of the incoming message to the language that was identified by Watson Language Translator. 
        params.payload.context.skills['actions skill'].user_defined['language'] = res.languages[0].language;
        console.log(JSON.stringify(params))
        return params;
})
}
else {
    params.payload.context.skills['actions skill'].user_defined['language'] = 'none';
    return param
}
};
```
{: codeblock}

The second web action in the sequence looks as follows:

```javascript
let rp = require("request-promise");

function main(params) {
  console.log(JSON.stringify(params))
    if ((params.payload.context.skills["actions skill"].user_defined.language !== 'en') && (params.payload.context.skills["actions skill"].user_defined.language !== 'none')) {
    const options = { method: 'POST',
    url: 'https://api.us-south.language-translator.watson.cloud.ibm.com/instances/572b37be-09f4-4704-b693-3bc63869nnnn/v3/translate?version=2018-05-01',
    auth: {
            'username': 'apikey',
            'password': 'nnn'
        },
    body: { 
        text: [ 
            params.payload.output.generic[0].text
            ],
            target: params.payload.context.skills["actions skill"].user_defined.language
    },
    json: true 
    };
      return rp(options)
      .then(res => {
          params.payload.context.skills["actions skill"].user_defined["original_output"] = params.payload.output.generic[0].text;
          params.payload.output.generic[0].text = res.translations[0].translation;
          return {
            body : params
          }
  })
  }
  return { 
    body : params
  }
};
```
{: codeblock}

### Example 3
{: #webhook-post-example-3}

This example shows how to compose a webhook response to let {{site.data.keyword.conversationshort}} skip processing the message and directly return the webhook's response.

#### Webhook configuration

In the pre-message webhook configuration page, specify the following values:

 - URL: https://your-webhook-url/webhook_skip
 - Header Name: Content-Type
 - Header Value: application/json

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
{: #webhook-post-remove}

If you decide that you do not want to process message responses with a webhook, complete the following steps:

1. In your assistant, go to **Environments** and open the environment where you want to remove the webhook.

1. Click the ![Environment settings icon](images/gear-icon-black.png) icon to open the environment settings.

1. On the **Environment settings** page, click **Post-message webhook**.

   For the **Classic experience**, complete the following steps:

   - For the assistant that you want to configure, click the ![Overflow menu](images/overflow-menu--vertical.svg) icon, and then choose **Settings**.

   - Click **Webhooks** > **Post-message webhook**.

1. Do one of the following steps:

  - To stop calling a webhook to process every incoming message, set the **Post-message webhook** switch to **Disabled**.

  - To change the webhook that you want to call, click **Delete webhook**.
