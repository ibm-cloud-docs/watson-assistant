---

copyright:
  years: 2015, 2024
lastupdated: "2024-02-08"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Defining responses by using the JSON editor
{: #assistant-responses-json}

In some situations, you might need to define your assistant's responses by using the JSON editor. For more information, see [Adding assistant responses](/docs/watson-assistant?topic=watson-assistant-respond)).
{: shortdesc}

To edit a response by using the JSON editor, click the **Switch to JSON editor** icon ![Switch to JSON editor icon](images/json-editor-icon.png) in the **Assistant says** field. The JSON editor shows how the response is defined behind the scenes and sent to the channel.

## Generic JSON format
{: #assistant-responses-json-generic}

If you open the JSON editor on a new, empty response, you see the following basic structure:

```json
{
  "generic": []
}
```
{: codeblock}

The `generic` property defines an array of responses that are sent to the channel when the step is executed. The term _generic_ refers to the fact that these responses are defined by using a generic JSON format that is not specific to any channel. This format can accommodate various response types that are supported by multiple integrations, and can also be implemented by a custom client application that uses the REST API.

The `generic` array for a step can contain multiple responses, and each response has a _response type_. A basic step that sends a simple text response typically includes only a single response with the response type `text`. However, many other response types are available, supporting multimedia and interactive content, plus control over the behavior of some channel integrations.

Although the `generic` format can be sent to any channel integration, not all channels support all response types, so a particular response might be ignored or handled differently by some channels. For more information, see [Channel integration support for response types](#assistant-responses-json-integration-support).

At run time, output with multiple responses might be split into multiple message payloads. The channel integration sends these messages to the channel in sequence, but it is the responsibility of the channel to deliver these messages to the user; this can be affected by network or server issues.
{: note}

### Adding responses
{: #assistant-responses-json-add-responses}

To specify a response in the JSON editor, insert the appropriate JSON objects into the `generic` field of the step response. The following example shows output with two responses of different types (text and an image):

```json
{
  "generic":[
    {
      "response_type": "text",
      "values": [
        {
          "text_expression": {
            "concat": [
              {
                "scalar": "This is a text response."
              }
            ]
          }
        }
      ]
    },
    {
      "response_type": "image",
      "source": "https://example.com/image.jpg",
      "title": "Example image",
      "description": "This is an image response."
    }
  ]
}
```
{: codeblock}

For more information, see [Response types](#assistant-responses-json-response-types).

### Targeting specific integrations
{: #assistant-responses-json-target-integrations}

If you plan to deploy your assistant to multiple channels, you might want to send different responses to different integrations based on the capabilities of each channel. The `channels` property of the generic response object provides a way to do this.

This mechanism is useful if your conversation flow does not change based on the integration in use, and if you cannot know in advance what integration the response is sent to at run time. By using `channels`, you can define a single step that supports all integrations, while still customizing the output for each channel. For example, you might want to customize the text formatting, or even send different response types, based on what the channel supports.

Using `channels` is useful along with the `channel_transfer` response type. Because the message output is processed both by the channel that initiates the `transfer` and by the target channel, you can use `channels` to define responses that are processed by one or the other.

To specify the integrations for which a response is intended, include the optional `channels` array as part of the response object. All response types support the `channels` array. This array contains one or more objects by using the following syntax:

```json
{
  "channel": "<channel_name>"
}
```
{: codeblock}

The value of `<channel_name>` can be any of the following strings:

- **`chat`**: Web chat
- **`voice_telephony`**: Phone
- **`text_messaging`**: SMS
- **`slack`**: Slack
- **`facebook`**: Facebook Messenger
- **`whatsapp`**: WhatsApp

The following example shows step output that contains two responses: one intended for the web chat integration and one intended for the Slack and Facebook integrations.

```json
{
  "generic": [
    {
      "response_type": "text",
      "channels": [
        {
          "channel": "chat"
        }
      ],
      "values": [
        {
          "text_expression": {
            "concat": [
              {
                "scalar": "This output is intended for the <strong>web chat</strong>."
              }
            ]
          }
        }
      ]
    },
    {
      "response_type": "text",
      "channels": [
        {
          "channel": "slack"
        },
        {
          "channel": "facebook"
        }
      ],
      "values": [
        {
          "text_expression": {
            "concat": [
              {
                "scalar": "This output is intended for either Slack or Facebook."
              }
            ]
          }
        }
      ]
    }
  ]
}
```
{: codeblock}

If the `channels` array is present, it must contain at least one channel object. Any integration that is not listed ignores the response. If the `channels` array is absent, all integrations handle the response.

## Response types
{: #assistant-responses-json-response-types}

You can configure different types of responses using JSON. To learn more about response types and supported integrations for JSON response types, see [Response types reference](/docs/watson-assistant?topic=watson-assistant-response-types-reference).




