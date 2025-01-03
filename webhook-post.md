---

copyright:
  years: 2019, 2025
lastupdated: "2025-01-03"

keywords: post webhook, postwebhook, post-webhook

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Making a call after processing a message
{: #webhook-post}

A post-message webhook calls an external service or application every time that the assistant renders a response. The external service can process the assistant's output before it is sent to the channel.
{: shortdesc}

You can add a post-message webhook to your assistant if you want to trigger the webhook before each message response is shown to the customer.

If you are using a custom channel, the post-message webhook works with the v2 `/message` API only (stateless and stateful). For more information, see the [API reference](https://cloud.ibm.com/apidocs/assistant-v2?code=node#message). All built-in channel integrations use this API.
{: important}

You can use a post-message webhook to do things like extract custom responses from an external content repository. For example, you can define actions with custom IDs in the responses instead of text. The post-message webhook can pass these IDs to an external database to retrieve stored text responses.

You can use this webhook in coordination with the pre-message webhook. For example, if you use the pre-message webhook to strip personally identifiable information from the customer's input, you can use the post-message webhook to add it back. If you use the pre-message webhook to translate the customer's input to the assistant's language, you can use the post-message webhook to translate the response into the customer's language before returning it. For more information, see [Making a call before processing a message](/docs/watson-assistant?topic=watson-assistant-webhook-pre).

For environments where private endpoints are in use, keep in mind that a webhook sends traffic over the internet.
{: note}

## Defining the webhook
{: #webhook-post-create}

You can define one webhook URL to use for processing every message response before it is sent to the channel and shown to the customer.

The programmatic call to the external service must meet these requirements:

- The call must be a POST HTTP request.
- The call must be completed in 30 seconds or less.
- The format of the request and response must be in JSON. For example, `Content-Type: application/json`.

Do not set up and test your webhook in a production environment where the assistant is deployed and is interacting with customers.
{: important}

To add the webhook details, complete the following steps:

1. In your assistant, open the environment where you want to configure the webhook.

1. Click the ![Environment settings icon](images/../../icons/settings.svg) icon to open the environment settings.

1. On the **Environment settings** page, click **Post-message webhook**.

   1.  Or, if you're using the classic experience, open the **Assistants** page.
   
   1. For the assistant you want to configure, click the ![Overflow menu](images/overflow-menu--vertical.svg) icon, and then choose **Settings**.

   1.  Click **Webhooks**, then click **Post-message webhook**.

1.  Set the **Post-message webhook** switch to **Enabled**.

1.  Decide whether to return an error if the webhook call fails.

    When enabled, everything stops until the processing step is completed successfully.
    {: important}

    - If you have a critical postprocessing step that must be taken before you want to allow the response to be sent to the customer, then enable this setting.

    - When this setting is disabled, the assistant ignores any errors that it encounters and continues to process the response without taking the processing step. If the postprocessing step is helpful but not critical, consider keeping this setting disabled.

1.  In the **URL** field, add the URL for the external application to which you want to send HTTP POST request callouts.

    For example, maybe you store your assistant's responses in a separate content management system. When the assistant understands the input, the processed action returns a unique ID that corresponds to a response in your CMS. To call a service that retrieves a response from your CMS for a given unique ID, specify the URL for your service instance. For example, `https://example.com/get_answer`.

    You must specify a URL that uses the SSL protocol, so specify a URL that begins with `https`.

    You cannot use a webhook to call a {{site.data.keyword.openwhisk_short}} action that uses token-based Identity and Access Management (IAM) authentication. However, you can make a call to a {{site.data.keyword.openwhisk_short}} web action or a secured web action.
    {: important}

1.  In the **Secret** field, add a private key to pass with the request that can be used to authenticate with the external service.

    The key must be specified as a text string, such as `purple unicorn`. The maximum length is 1,024 characters. You cannot specify a context variable.

    It is the responsibility of the external service to check for and verify the secret. If the external service does not require a token, specify any string that you want. You cannot leave this field empty.

    If you want to see the secret as you enter it, click the **Show password** icon ![View icon](../../icons/view.svg) before you start typing. After you save the secret, asterisks replace the string and can't be viewed again.
    {: note}

1. In the **Timeout** field, specify the length of time (in seconds) you want the assistant to wait for a response from the webhook before it returns an error. The timeout duration cannot be shorter than 1 second or longer than 30 seconds.

1.  In the Headers section, add any headers that you want to pass to the service one at a time by clicking **Add header**.

    For example, if the external application that you call returns a response, it might be able to send a response in multiple different formats. The webhook requires that the response is formatted in JSON. The following table illustrates how to add a header that indicates that you want the resulting value to be returned in JSON format.

    | Header name    | Header value       |
    |----------------|--------------------|
    | `Content-Type` | `application/json` |
    {: caption="Header example" caption-side="bottom"}

    The service automatically sends an `Authorization` header with a JWT; you do not need to add one. If you want to handle authorization yourself, add your own authorization header and it is used instead.

    After you save the secret, asterisks replace the string and can't be viewed again. 
    {: note}

Your webhook details are saved automatically.

## Testing the webhook
{: #webhook-post-test}

Do extensive testing of your webhook before you enable it for an assistant that is being used in a production environment.
{: important}

The webhook is triggered only when your assistant processes a message and a response is ready to be returned to the channel.

If you enable the setting to return an error when a webhook call fails, the assistant's processing halts entirely if the webhook encounters any issues. Regularly test the process you are calling to ensure that you receive alerts if the external service is down, which helps prevent failures in returning message responses.

If you call an {{site.data.keyword.openwhisk_short}} web action, you can use the logging capability in {{site.data.keyword.openwhisk_short}} to help you troubleshoot your code. You can [download the command-line interface](/functions/learn/cli){: external}, and then enable logging with the [activation polling command](/docs/cloud-functions-cli-plugin?topic=cloud-functions-cli-plugin-functions-cli#cli_activation_poll){: external}.
{: tip}

## Troubleshooting the webhook
{: #webhook-post-ts}

The following error codes can help you track down the cause of issues you might encounter. If you have a web chat integration, for example, you know that your webhook has an issue if every test message you submit returns a message such as `There is an error with the message you just sent, but feel free to ask me something else`. If this message is displayed, use a REST API tool, such as cURL, to send a test `/message` API request, so you can see the error code and the full message that is returned.

| Error code and message | Description |
|------------|-------------|
| 422 Webhook responded with invalid JSON body | The webhook's HTTP response body could not be parsed as JSON. |
| 422 Webhook responded with `[500]` status code | A problem occurred with the external service that you called. The code failed or the external server refused the request. |
| 500 Processor Exception : `[connections to all backends failing]` | An error occurred in the webhook microservice. It could not connect to backend services. |
{: caption="Error code details" caption-side="bottom"}

## Webhook security
{: #webhook-post-security}

To authenticate the webhook request, verify the JSON Web Token (JWT) that is sent with the request. The webhook microservice automatically generates a JWT and sends it in the `Authorization` header with each webhook call. It is your responsibility to add code to the external service that verifies the JWT.

For example, if you specify `purple unicorn` in the **Secret** field, you might add code such as:

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

## Example request body
{: #webhook-post-request-body}

It is useful to know the format of the request post-message webhook body so that your external code can process it.

The payload contains the response body that your assistant returns for the v2 `/message` (stateful and stateless) API call. The event name `message_processed` indicates that the post-message webhook generates the request. For more information about the message request body, see the [API reference](https://cloud.ibm.com/apidocs/assistant-v2?code=node#message){: external}.

The following sample shows how a simple request body is formatted.

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

### Response body

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

## Example 1
{: #webhook-post-example1}

This example shows you how to add `y'all` to the end of each response from the assistant.

In the post-message webhook configuration page, the following values are specified:

- **URL**: `https://your-webhook-url/`
- **Secret**: none
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

## Example 2
{: #webhook-post-example-translate-back}

This example shows you how to translate a message response back to the customer's language. It works only if you perform the steps in [Example 2](/docs/watson-assistant?topic=watson-assistant-webhook-pre#webhook-pre-example-translate) to define a pre-message webhook that translates the original message into English.

Define a sequence of web actions in IBM Cloud Functions. The first action in the sequence checks for the language of the original incoming text, which you stored in a context variable named `original_input` in the pre-message webhook code. The second action in the sequence translates the dialog response text from English into the original language that was used by the customer.

In the pre-message webhook configuration page, the following values are specified:

- **URL**: `https://your-webhook-url/`
- **Secret**: none
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

## Removing the webhook
{: #webhook-post-delete}

If you decide you do not want to process message responses with a webhook, complete the following steps:

1. In your assistant, go to **Environments** and open the environment where you want to configure the webhook.

1. Click the ![Environment settings icon](images/../../icons/settings.svg) icon to open the environment settings.

1. On the **Environment settings** page, click **Post-message webhook**.

   1.  Or, if you're using the classic experience, open the **Assistants** page.
   
   1. For the assistant you want to configure, click the ![Overflow menu](images/overflow-menu--vertical.svg) icon, and then choose **Settings**.

   1.  Click **Webhooks**, then click **Post-message webhook**.

1.  Do one of the following things:

    - To change the webhook that you want to call, click the **Delete webhook** button to delete the currently specified URL and secret. You can then add a URL and other details.

    - To stop calling a webhook to process every incoming message, click the switch to disable the webhook altogether.
