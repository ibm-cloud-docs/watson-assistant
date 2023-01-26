---

copyright:
  years: 2015, 2023
lastupdated: "2023-01-23"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Integration variables
{: #expression-integration-variables}

By writing expressions, you can access integration variables, which are context variables that are specific to integrations (such as the web chat and phone integrations). All integration variables are contained in the `system_integrations` JSON object, which you can access using the following expression:

```text
${system_integrations}
```
{: codeblock}

The `system_integrations` object has the following structure:

```json
{
  "channel": {
    "name": "{channel_name}",
    "private": {
      "user": {
        "id": "{user_id}",
        "phone_number": "{phone_number}"
      }
    }
  },
  "chat": {...},
  "voice_telephony": {...},
  "text_messaging": {...},
  "whatsapp": {...},
  "slack": {...},
  "facebook": {...}
}
```
{: codeblock}

## `channel`
{: #expression-integration-variables-channel}

Always included. This object contains general information about the channel that is being used to communicate with the assistant.

Properties contained in the `private` object are treated as private variables, which are not included in logs.
{: note}

| Name                                | Type   | Description |
|-------------------------------------|--------|-------------|
| `channel.name`                      | String | The name of the channel that is in use. One of the following values: \n - `Web chat` \n - `Phone` \n - `SMS` \n - `Whatsapp` \n - `Slack` \n - `Facebook Messenger` |
| `channel.private.user.id`           | String | The ID of the user who is interacting with the assistant through the channel. Set by the channel. |
| `channel.private.user.phone_number` | String | The phone number associated with the user. Set by the phone, SMS, and WhatsApp integrations. |
{: caption="Fields of the channel object" caption-side="top"}

### Example JSON
{: #expression-integration-variables-channel-example}

```json
{
  "name": "Web chat",
  "private": {
    "user": {
      "id": "anonymous_IBMuid-727c0302-6fd7-4abb-b7ee-f06b4bf30e99"
    }
  }
}
```
{: codeblock}

## `chat`
{: #expression-integration-variables-chat}

Included only if the web chat integration is in use.

### Properties
{: #expression-integration-variables-chat-properties}

| Name                             | Type   | Description |
|----------------------------------|--------|-------------|
| `browser_info.browser_name`      | String | The browser name, such as `chrome`, `edge`, or `firefox`. |
| `browser_info.browser_version`   | String | The browser version, such as `109.0.0`. |
| `browser_info.browser_OS`        | String | The operating system of the customer's computer, such as `Mac OS`. |
| `browser_info.language`          | String | The default locale code of the browser, such as `en-US`. |
| `browser_info.page_url`          | String | The URL of the web page where the web chat is embedded, not including any query parameters or hashes. |
| `browser_info.screen_resolution` | String | The height and width of the browser window, such as `width: 1440, height: 900`. |
| `browser_info.user_agent`        | String | The content of the HTTP `User-Agent` request header. |
| `browser_info.client_ip_address` | String | The IP address of the customer's computer. |
| `browser_info.ip_address_list`   | Array  | Ann array IP addresses specified by HTTP `X-Forwarded-For` request headers. |

### Example JSON
{: #expression-integration-variables-chat-example}

```json
{
  "chat": {
    "browser_info": {
      "browser_name": "chrome",
      "browser_version": "109.0.0",
      "browser_OS": "Mac OS",
      "language": "en-US",
      "page_url": "https://us-south.assistant.watson.cloud.ibm.com/crn%3Av1%3Abluemix%3Apublic%3Aconversation%3Aus-south%3Aa%2Fc41400d63d91741a749091dc63574c2c%3Ab696c1e5-7316-4fb0-a61c-664438397e91%3A%3A/assistants/e344fcfe-506c-449f-a182-ebdefe4356ad/actions/actions/custom/edit/action_28584",
      "screen_resolution": "width: 1920, height: 1080",
      "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.0.0 Safari/537.36",
      "client_ip_address": "65.191.135.254",
      "ip_address_list": [
        "65.191.135.254",
        " 104.99.56.143",
        "10.185.27.136",
        "172.30.226.64"
      ]
    }
  },
  "channel": {
    "name": "Web chat",
    "private": {
      "user": {
        "id": "anonymous_IBMuid-727c0302-6fd7-4abb-b7ee-f06b4bf30e99"
      }
    }
  }
}
```
{: codeblock}

### Example expression
{: #expression-integration-variables-chat-example-expression}

This expression tests whether the customer is using the Chrome browser:

```
${system_integrations}.chat.browser_info.browser_name.equals("chrome")
```

You might specify this expression as the value for a boolean session variable, which you could then use in a step condition. For example, if your website supports only Chrome, you could have a step conditioned on this variable being `false` and has the following output: `I see you aren't using the Chrome browser. Some features of our website work only on Chrome.`

## `voice_telephony`
{: #expression-integration-variables-phone}

Included only if the phone integration is in use.

### Properties
{: #expression-integration-variables-phone-properties}

Properties contained in the `private` object are treated as private variables, which are not included in logs.
{: note}

| Name                        | Type   | Description |
|-----------------------------|--------|-------------|
| `sip_call_id`               | String | The SIP call ID associated with the phone call. |
| `assistant_phone_number`    | String | The phone number associated with with the {{site.data.keyword.conversationshort}} end of the call. |
| `sip_custom_invite_headers` | Object | A user-defined array of key/value pairs containing SIP headers from the SIP `INVITE` request. |
| `private.user_phone_number` | String | The phone number from which the customer's call originated. |
| `private.sip_request_uri`   | String | The inbound SIP request URI that initiated the phone call. |
| `private.sip_from_uri`      | String | The URI from the `From` header of the SIP request. |
| `private.sip_to_uri`        | String | The URI from the `To` header of the SIP request. |

### Example JSON
{: #expression-integration-variables-phone-example}

```json
{
  "output": {
    "generic": [{
        "response_type": "text",
        ...
    }]
  },
  "context" : {
    "integrations" :{
      "voice_telephony" : {
        "post_response_timeout_count":10000,
        "final_utterance_timeout_count":30000,
        "turn_settings": {
          "timeout_count": 5000
        },
        "cdr_custom_data" : {
           "custom_data_1": "data 1",
           "custom_data_2": "data_2"
        }
      }
    }
  }
}
```
{: codeblock}

