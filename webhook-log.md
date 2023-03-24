---

copyright:
  years: 2019, 2023
lastupdated: "2023-03-24"

keywords: log webhook

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Logging activity with a webhook
{: #webhook-log}

[Plus]{: tag-green}[Enterprise]{: tag-purple}

You can log activity by making a call to an external service or application every time a customer submits input to the assistant.
{: shortdesc}

A webhook is a mechanism that allows you to call out to an external program based on events in your program.

This feature is available only to Plus and Enterprise plan users.

The Plus plan allows no more than 5 log webhooks per instance. This limit does not apply to Enterprise plan instances.
{: note}

Add a log webhook to your assistant if you want to use an external service to log {{site.data.keyword.conversationshort}} activity. You can log two kinds of activity:

- **Messages and responses**: The log webhook is triggered each time the assistant responds to customer input. You can use this option as an alternative to the built-in analytics feature to handle logging yourself. (For more information about the built-in analytics support, see [Review your entire assistant at a glance](/docs/watson-assistant?topic=watson-assistant-analytics-overview).)
  
    If you are using a custom channel, note that the log webhook works with the v2 `/message` API only (stateless and stateful). For more information, see the [API reference](https://cloud.ibm.com/apidocs/assistant/assistant-v2#message). All built-in channel integrations use this API.
    {: important}

- **Call detail records (CDRs)**: The log webhook is triggered after each telephone call a user makes to your assistant using the phone integration. A Call Detail Record (CDR) is a summary report that documents the details of a telephone call, including phone numbers, call length, latency, and other diagnostic information. CDR records are only for assistants that use the phone integration.

The log webhook does not return anything to your assistant.

For environments where private endpoints are in use, keep in mind that a webhook sends traffic over the internet.
{: note}

## Defining the webhook
{: #webhook-log-create}

You can define one webhook URL to use for logging every incoming message or CDR event.

The programmatic call to the external service must meet these requirements:

- The call must be a POST HTTP request.

To add the webhook details, complete the following steps:

1. In your assistant, go to **Environments** and open the environment where you want to configure the webhook.

1. On the **Environments** page, click the ![Environment settings icon](images/gear-icon-black.png) icon beside the environment title to open the environment settings.

1. On the **Environment settings** page, click **Webhooks > Log webhook**.

1. Set the *Log webhook* switch to **Enabled**.

    If you cannot enable the webhook, you might need to upgrade your service plan.

1. In the **URL** field, add the URL for the external application to which you want to send HTTP POST request callouts (for example, `https://example.com/my_log_service`.

    You must specify a URL that uses the SSL protocol, so specify a URL that begins with `https`.

1. In the **Secret** field, add a token to pass with the request that can be used to authenticate with the external service.

    The secret must be specified as a text string, such as `purple unicorn`.  The maximum length is 1,024 characters. You cannot specify a context variable.

    It is the responsibility of the external service to check for and verify the secret. If the external service does not require a token, specify any string you want. You cannot leave this field empty.

    If you want to see the secret as you enter it, click on the **Show password** icon ![view icon](../../icons/view.svg) before you start typing. After you save the secret, the string is replaced by asterisks and can't be viewed again.
    {: note}

1. Click the appropriate checkboxes to select which kinds of activity you want to log:

    - To log messages and responses, select **Subscribe to conversation logs**.
    - To log CDR events for the phone integration, select **Subscribe to CDR (Call Detail Records)**.

1. In the Headers section, add any headers that you want to pass to the service one at a time by clicking **Add header**.

    The service automatically sends an `Authorization` header with a JWT; you do not need to add one. If you want to handle authorization yourself, add your own authorization header and it will be used instead.

    After you save the header value, the string is replaced by asterisks and can't be viewed again. 
    {: note}

Your webhook details are saved automatically.

## Removing the webhook
{: #webhook-log-delete}

If you decide you do not want to log messages with a webhook, complete the following steps:

1. In your assistant, go to **Environments** and open the environment where you want to remove the webhook.

1. On the **Environments** page, click the ![Environment settings icon](images/gear-icon-black.png) icon beside the environment title to open the environment settings.

1. On the **Environment settings** page, click **Webhooks > Log webhook**.

1. Do one of the following things:

    - To change the webhook that you want to call, click **Delete webhook** to delete the currently specified URL and secret. You can then add a new URL and other details.
    - To stop calling a webhook to log every message and response, click the *Log webhook* switch to disable the webhook altogether.

## Webhook security
{: #webhook-log-security}

To authenticate the webhook request, verify the JSON Web Token (JWT) that is sent with the request. The webhook microservice automatically generates a JWT and sends it in the `Authorization` header with each webhook call. It is your responsibility to add code to the external service that verifies the JWT.

For example, if you specify `purple unicorn` in the **Secret** field, you might add code similar to this:

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

## Webhook request body
{: #webhook-log-request-body}

The request body the webhook sends to the external service is a JSON object with the following structure:

```json
{
  "event": {
    "name": "{event_type}"
   },
  "payload": {
    ...
  }
}
```
{: codeblock}

where `{event_type}` is either `message_logged` (for messages and responses) or `cdr_logged` (for CDR events).

The `payload` object contains the event data to be logged. The structure of the `payload` object depends on the type of event.

### Message event payload
{: #webhook-log-request-body-message}

For `message_logged` events, the `payload` object contains data about a message request sent to the assistant and the message response returned to the integration or client application. For more information about the fields that are part of message requests and responses, see the [API reference](https://cloud.ibm.com/apidocs/assistant/assistant-v2#message).

The log webhook payload might include data that is not currently supported by the API. Any fields that are not defined in the API reference documentation are subject to change.
{: important}

### CDR event payload
{: #webhook-log-request-body-cdr}

For `cdr_logged` events, the `payload` object contains data about a Call Detail Record (CDR) event that was handled by the phone integration. The structure of the `payload` object for a CDR event is as shown by this example:

```json
{
  "primary_phone_number": "+18005550123",
  "global_session_id": "9caa8bad-aaa8-4a5a-a4b5-62bccc703d15",
  "failure_occurred": false,
  "transfer_occurred": false,
  "active_calls": 0,
  "warnings_and_errors": [
    {
      "code": "CWSMR0033W",
      "message": "CWSMR0033W: The inbound RTP audio stream jitter of 43 ms exceeds the maximum jitter threshold of 30 ms."
    },
    {
      "code": "CWSMR0070W",
      "message": "CWSMR0070W: A request to the Watson Speech To Text service failed for the following reason = Unexpected server response: 403, response headers = {\"strict-transport-security\":\"max-age=31536000; includeSubDomains;\",\"content-length\":\"157\",\"content-type\":\"application/json\",\"x-dp-watson-tran-id\":\"23860083-88b6-41d7-9130-30bbfebe647e\",\"x-request-id\":\"23860083-88b6-41d7-9130-30bbfebe647e\",\"x-global-transaction-id\":\"6c764df3-81db-41bb-a14f-62384facffca\",\"server\":\"watson-gateway\",\"x-edgeconnect-midmile-rtt\":\"1\",\"x-edgeconnect-origin-mex-latency\":\"28\",\"date\":\"Thu, 13 May 2021 20:31:12 GMT\",\"connection\":\"keep-alive\"}, response body = {\"code\":403,\"trace\":\"23860083-88b6-41d7-9130-30bbfebe647e\",\"error\":\"Forbidden\",\"more_info\":\"[https://cloud.ibm.com/docs/watson?topic=watson-forbidden-error](https://cloud.ibm.com/docs/watson?topic=watson-forbidden-error)\"}, x-global-transaction-id = 6c764df3-81db-41bb-a14f-62384facffca. The Media Relay will reattempt to send the request."
    }
  ],
  "realtime_transport_network_summary": {
    "inbound_stream": {
      "average_jitter": 4,
      "canonical_name": "b74f3689-1ae8-4a0a-bde3-adf5b488553e",
      "maximum_jitter": 18,
      "packets_lost": 0,
      "packets_transmitted": 952,
      "tool_name": ""
    },
    "outbound_stream": {
      "average_jitter": 0,
      "canonical_name": "voice.gateway",
      "maximum_jitter": 0,
      "packets_lost": 0,
      "packets_transmitted": 838,
      "tool_name": "IBM Voice Gateway/1.0.7.0"
    }
  },
  "call": {
    "start_timestamp": "2021-10-12T20:54:02.591Z",
    "stop_timestamp": "2021-10-12T20:54:20.375Z",
    "milliseconds_elapsed": 17784,
    "outbound": false,
    "end_reason": "assistant_hangup",
    "security": {
      "media_encrypted": false,
      "signaling_encrypted": false,
      "sip_authenticated": false
    }
  },
  "session_initiation_protocol": {
    "invite_arrival_time": "2021-10-12T20:54:00.565Z",
    "setup_milliseconds": 2026,
    "headers": {
      "call_id": "17465345_115257202@10.90.150.99",
      "from_uri": "sip:+18885550456@pstn.twilio.com",
      "to_uri": "sip:+18005550123@public.voip.us-south.assistant.test.watson.cloud.ibm.com"
    }
  },
  "max_response_milliseconds": {
    "assistant": 339,
    "text_to_speech": 535,
    "speech_to_text": 0
  },
  "assistant_interaction_summaries": [
    {
      "session_id": "7874ec3a-1330-4180-afe1-46bfb220af5b",
      "assistant_id": "97f16ba4-ad94-41af-aa6c-33cd56ad5e7e",
      "turns": [
        {
          "assistant": {
            "log_id": "58bebfd1-0118-419b-a555-b152a1efbbe8",
            "response_milliseconds": 339,
            "start_timestamp": "2021-10-12T20:54:00.722Z"
          },
          "request": {
            "type": "start"
          },
          "response": [
            {
              "barge_in_occurred": true,
              "streaming_statistics": {
                "response_milliseconds": 301,
                "start_timestamp": "2021-10-12T20:54:00.722Z",
                "stop_timestamp": "2021-10-12T20:54:01.023Z",
                "transaction_id": "3dce431c-fb2f-4b62-9fce-585f4e06fe00"
              },
              "type": "text_to_speech"
            }
          ]
        },
        {
          "assistant": {
            "log_id": "38f36bfb-c2aa-4600-9418-6ab422664e31",
            "response_milliseconds": 158,
            "start_timestamp": "2021-10-12T20:54:05.621Z"
          },
          "request": {
            "type": "dtmf"
          },
          "response": [
            {
              "type": "disable_speech_barge_in"
            },
            {
              "type": "text_to_speech",
              "barge_in_occurred": false,
              "streaming_statistics": {
                "transaction_id": "af4c47c3-5cc4-43c8-9b9c-81d6f997c52f",
                "start_timestamp": "2021-10-12T20:54:06.321Z",
                "stop_timestamp": "2021-10-12T20:54:14.338Z",
                "response_milliseconds": 535
              }
            },
            {
              "type": "enable_speech_barge_in"
            },
            {
              "type": "text_to_speech",
              "barge_in_occurred": true,
              "streaming_statistics": {
                "transaction_id": "eafdd846-2829-4e1a-8068-b1035510b1e1",
                "start_timestamp": "2021-10-12T20:54:14.795Z",
                "stop_timestamp": "2021-10-12T20:54:20.388Z",
                "response_milliseconds": 447
              }
            }
          ]
        },
        {
          "assistant": {
            "log_id": "07d74b35-0205-43e4-923c-1e43e1cb429c",
            "response_milliseconds": 0,
            "start_timestamp": "2021-10-12T20:54:20.377Z"
          },
          "request": {
            "type": "hangup"
          },
          "response": []
        }
      ]
    }
  ]
}

```
{: codeblock}

For detailed information about the structure of the CDR event payload, see [CDR log event reference](/docs/watson-assistant?topic=watson-assistant-cdr-log-reference).
