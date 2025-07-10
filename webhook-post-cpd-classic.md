---

copyright:
  years: 2019, 2025
lastupdated: "2025-07-10"

keywords: post webhook, postwebhook, post-webhook

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Calling a service after processing a message for {{site.data.keyword.cpd_full_notm}} - classic experience
{: #webhook-post-cp4d-classic}

Use a post-message webhook to call an external service after your assistant generates a response.  
{: shortdesc}

You can use post-message webhooks for the following use cases:

 - Retrieve a response from an external source by using custom action IDs.
 - Translate the assistant's response to the user's language.
 - Reinsert personal data that was removed earlier for privacy.

## Learn more

For more information about related features and details, see the following resources:

 - [Making a call before processing a message](/docs/watson-assistant?topic=watson-assistant-webhook-pre)
 - [Calling a service before processing a message for {{site.data.keyword.cpd_full_notm}} - classic experience](/docs/watson-assistant?topic=watson-assistant-webhook-pre-cp4d-classic)
 - [Making a programmatic call from dialog](/docs/watson-assistant?topic=watson-assistant-dialog-webhooks#dialog-webhooks)
 - [API reference](https://cloud.ibm.com/apidocs/assistant-v2#message)

## Before you begin

Your webhook service must meet these technical requirements:

 - Do not set up or test the webhook in a production environment.
 - The call must be a POST HTTP request.
 - The request and response must use JSON (Content-Type: application/json).
 - The response must return within 30 seconds.

## Procedure
{: #post-procedure-cp4d-classic}

This section covers the procedure to define, test, and remove post-message webhooks for {{site.data.keyword.cpd_short}} - classic experience.

- [**Webhook configuration**](#post-webhook-config-cp4d-classic)
- [**Adding a secret**](#post-add-secret-cp4d-classic)
- [**Webhook security**](#post-webhook-security-cp4d-classic)
- [**Configuring webhook error handling for postprocessing**](#post-error-handling-cp4d-classic)
- [**Testing the webhook**](#post-testing-cp4d-classic)
- [**Troubleshooting the webhook**](#post-troubleshoot-cp4d-classic)
- [**Example request body**](#post-example-request-cp4d-classic)
- [**Example 1**](#post-example-1-cp4d-classic)
- [**Example 2**](#post-example-2-cp4d-classic)
- [**Removing the webhook**](#post-remove-cp4d-classic)

### Webhook configuration
{: #post-webhook-config-cp4d-classic}

To add the webhook details, complete the following steps:

1. For the assistant that you want to configure, click the ![Overflow menu](images/overflow-menu--vertical.svg) icon, and then choose **Settings**.

1. Click **Webhooks** > **Post-message webhook**.

1. Set the **Post-message webhook** switch to **Enabled**.

1. In the **Synchronous event**, select from one of the following options:

   - Continue processing user input without webhook update if there is an error.

   - Return an error to the client if the webhook call fails.

   For more information, see [Configuring webhook error handling for postprocessing](#post-error-handling-cp4d-classic).

1.  In the **URL** field, add the URL for the external application to which you want to send HTTP POST request callouts.

    For example, maybe you store your assistant's responses in a separate content management system. When the assistant understands the input, the processed action returns a unique ID that corresponds to a response in your CMS. To call a service that retrieves a response from your CMS for a given unique ID, specify the URL for your service instance. For example, `https://example.com/get_answer`.

    You must specify a URL that uses the SSL protocol, so specify a URL that begins with `https`.

1. Fill in the **Secret field**. For more information, see [Adding a secret](#post-add-secret-cp4d-classic).

1. In the **Timeout** field, specify the time duration (in seconds) that you want the assistant to wait for a response from the webhook before it returns an error. The timeout duration cannot be shorter than 1 second or longer than 30 seconds.

1.  In the **Headers** section, click **Add header +** to add any headers that you want to pass to the service, one at a time.

    The service automatically sends an Authorization header with a JWT. If you want to handle authorization yourself, add your own authorization header and the service uses it instead.{: note}

    If the external application that you call returns a response, it might be able to send a response in different formats. The webhook requires that the response is formatted in JSON. The following table illustrates how to add a header to indicate that you want the resulting value to be returned in JSON format.

    | Header name    | Header value       |
    |----------------|--------------------|
    | `Content-Type` | `application/json` |
    {: caption="Header example" caption-side="bottom"}

1. After you save the header value, the string is replaced by asterisks and can't be viewed again. 

1. Your webhook details are saved automatically.

### Adding a secret
{: #post-add-secret-cp4d-classic}

Add a client secret in the **Secret** field to pass with the request for authentication with the external service:

- Enter the key as a text string, such as `purple unicorn`.

- Use a maximum of 1,024 characters.

- Do not use context variables.

The external service is responsible for checking and verifying the secret. If no token is required, specify any string. This field cannot be left empty.

To view the secret as you enter it, click the **Show password** icon ![View icon](images/view.svg) before typing. After saving the secret, asterisks replace the string, and you can't view it again.
{: note}

For more information about how this field is used, see [Webhook security](#post-webhook-security-cp4d-classic).

### Webhook security
{: #post-webhook-security-cp4d-classic}

Authenticate the webhook request by verifying the JSON Web Token (JWT) that is sent with the request. The webhook microservice automatically generates a JWT and sends it in the `Authorization` header with each webhook call:

 - For new webhooks or webhooks updated through **Edit authentication**, the authorization header is ignored.

 - For existing webhooks with a saved authentication header, the **Edit authentication** button is disabled.

 - Updating an existing webhook to use the new authentication configuration changes its behavior.

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

### Configuring webhook error handling for postprocessing
{: #post-error-handling-cp4d-classic}

You can decide whether an error returns in the postprocessing step if the webhook call fails. You have two options:

- **Continue processing user input without webhook update if there is an error**: The assistant ignores the errors and processes the message without the webhook result. If postprocessing is useful but not essential, consider this option.

- **Return an error to the client if the webhook call fails**: If postprocessing is critical after the assistant sends a response, select this option.

When you enable **Return an error to the client if the webhook call fails**, everything stops until the postprocessing step is completed successfully.{: important}

Regularly test the external process to identify potential failures. If necessary, adjust this setting to prevent disruptions in the response processing.

### Testing the webhook
{: #post-testing-cp4d-classic}

Do extensive testing of your webhook before you enable it for an assistant that is used in a production environment.
{: important}

The webhook is triggered only when your assistant processes a message and a response is ready to be returned to the channel.

### Troubleshooting the webhook
{: #post-troubleshoot-cp4d-classic}

The following error codes can help you track down the cause of issues you might encounter. If you have a web chat integration, for example, you know that your webhook has an issue if every test message you submit returns a message such as `There is an error with the message you just sent, but feel free to ask me something else`. If this message is displayed, use a REST API tool, such as cURL, to send a test `/message` API request, so you can see the error code and the full message that is returned.

| Error code and message | Description |
|------------|-------------|
| 422 Webhook responded with invalid JSON body | The webhook's HTTP response body could not be parsed as JSON. |
| 422 Webhook responded with `[500]` status code | A problem occurred with the external service that you called. The code failed or the external server refused the request. |
| 500 Processor Exception : `[connections to all backends failing]` | An error occurred in the webhook microservice. It could not connect to backend services. |
{: caption="Error code details" caption-side="bottom"}

### Example request body
{: #post-example-request-cp4d-classic}

It is useful to know the format of the request post-message webhook body so that your external code can process it.

The payload contains the response body that your assistant returns for the version 2 of the `/message`, stateful and stateless, API call. The event name `message_processed` indicates that the post-message webhook generates the request. For more information about the message request body, see the [API reference](https://cloud.ibm.com/apidocs/assistant-v2#message){: external}.

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

### Example 1
{: #post-example-1-cp4d-classic}

This example shows how to add `y'all` to the end of each response from the assistant.

In the post-message webhook configuration page, the following values are specified:

- **URL**: `https://your-webhook-url/`
- **Secret**: None
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
{: #post-example-2-cp4d-classic}

This example shows how to translate a message response back to the customer's language. It works only if you perform the steps in [Example 2](/docs/watson-assistant?topic=watson-assistant-webhook-pre-cp4d-classic#pre-example-2-cp4d-classic) to define a pre-message webhook that translates the original message into English.

Define a sequence of web actions in IBM Cloud Functions. The first action in the sequence checks for the language of the original incoming text, which you stored in a context variable named `original_input` in the pre-message webhook code. The second action in the sequence translates the dialog response text from English into the original language that was used by the customer.

In the post-message webhook configuration page, the following values are specified:

- **URL**: `https://your-webhook-url/`
- **Secret**: None
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

### Removing the webhook
{: #post-remove-cp4d-classic}

If you do not want to process message responses with a webhook, complete the following steps:

1. For the assistant that you want to configure, click the ![Overflow menu](images/overflow-menu--vertical.svg) icon, and then choose **Settings**.

1. Click **Webhooks** > **Post-message webhook**.

1. Do one of the following steps:

 - To stop calling a webhook to process every incoming message, set the **Post-message webhook** switch to **Disabled**.

 - To change the webhook that you want to call, click **Delete webhook**.
