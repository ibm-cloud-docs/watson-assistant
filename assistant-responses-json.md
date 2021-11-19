---

copyright:
  years: 2015, 2021
lastupdated: "2021-11-19"

subcollection: watson-assistant

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:deprecated: .deprecated}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

{{site.data.content.classiclink}}

# Defining responses using the JSON editor
{: #assistant-responses-json}

In some situations, you might need to define your assistant's responses using the JSON editor. (For more information about assistant responses, see [Adding assistant responses](/docs/watson-assistant?topic=watson-assistant-respond)).
{: shortdesc}

To edit a response using the access the JSON editor, click the **Switch to JSON editor** icon ![Switch to JSON editor icon](images/json-editor-icon.png) in the corner of the **Assistant says** field. The JSON editor shows how the response is defined behind the scenes and sent to the channel.

## Generic JSON format
{: #assistant-responses-json-generic}

If you open the JSON editor on a new, empty response, you see the following basic structure:

```json
{
  "generic": []
}
```
{: codeblock}

The `generic` property defines an array of responses that will be sent to the channel when the step is executed. These term _generic_ refers to the fact that these responses are defined using a generic JSON format that is not specific to any channel. This format can accommodate various response types that are supported by multiple integrations, and can also be implemented by a custom client application that uses the REST API.

The `generic` array for a step can contain multiple responses, and each response has a _response type_. A basic step that sends a simple text response typically includes only a single response with the response type `text`. However, many other response types are available, supporting multimedia and interactive content, as well as control over the behavior of some channel integrations.

Although the `generic` format can be sent to any channel integration, not all channels support all response types, so a particular response might be ignored (or handled differently) by some channels. For information about which channels support which response types, see [Response types](#assistant-responses-json-response-types).

At run time, output containing multiple responses might be split into multiple message payloads. The channel integration sends these messages to the channel in sequence, but it is the responsibility of the channel to deliver these messages to the end user; this can be affected by network or server issues.
{: note}

### Adding responses

To specify a response in the JSON editor, insert the appropriate JSON objects into the `output.generic` field of the step response. The following example shows output containing two responses of different types (text and an image):

```json
{
  "output": {
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
}
```
{: codeblock}

For information about the available response types, see [Response types](#assistant-responses-json-response-types).

<!-- If you are building your own custom channel application using the REST API, your app must implement each response type as appropriate. For more information, see [Implementing responses](/docs/assistant?topic=assistant-api-dialog-responses). -->

### Targeting specific integrations
{: #assistant-responses-json-target-integrations}

If you plan to deploy your assistant to multiple channels, you might want to send different responses to different integrations based on the capabilities of each channel. The `channels` property of the generic response object provides a way to do this.

This mechanism is useful if your conversation flow does not change based on the integration in use, and if you cannot know in advance what integration the response will be sent to at run time. By using `channels`, you can define a single step that supports all integrations, while still customizing the output for each channel. For example, you might want to customize the text formatting, or even send different response types, based on what the channel supports.

<!-- Channel transfer not yet supported in actions
Using `channels` is particularly useful in conjunction with the `channel_transfer` response type. Because the message output is processed both by the channel initiating the `transfer` and by the target channel, you can use `channels` to define responses that will only be processed by one or the other. (For more information, and an example, see [Channel transfer](#assistant-responses-json-channel-transfer).) -->

To specify the integrations for which a response is intended, include the optional `channels` array as part of the response object. All response types support the `channels` array. This array contains one or more objects using the following syntax:

```json
{
  "channel": "<channel_name>"
}
```
{: codeblock}

The value of `<channel_name>` can be any of the following strings:

- **`chat`**: Web chat
- **`voice_telephony`**: Phone
- **`text_messaging`**: SMS with Twilio
- **`slack`**: Slack
- **`facebook`**: Facebook Messenger
- **`whatsapp`**: WhatsApp

The following example shows step output that contains two responses: one intended for the web chat integration and one intended for the Slack and Facebook integrations.

```json
{
  "output": {
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
}
```
{: codeblock}

If the `channels` array is present, it must contain at least one channel object. Any integration that is not listed ignores the response. If the `channels` array is absent, all integrations handle the response.

<!--
**Note:** If you need to change the logic of your dialog flow based on which integration is in use, or based on context data that is specific to a particular integration, see [Adding custom dialog flows for integrations](/docs/assistant?topic=assistant-dialog-integrations).
-->

## Response types
{: #assistant-responses-json-response-types}

The following response types are available. (For detailed information about how to specify each response type, see [Response types reference](/docs/watson-assistant?topic=watson-assistant-response-types-reference).)

Not all channel integrations support all response types. For information about which integrations support which response types, see [Channel integration support for response types](#assistant-responses-json-integration-support).
{: note}

`audio`
:   Plays an audio clip specified by a URL.

<!-- Channel transfer not yet supported in actions
`channel_transfer`

:   Requests that the conversation be transferred to a different integration. (Currently, only the web chat integration can be the target of a channel transfer.) -->

`connect_to_agent`
:   Requests that the conversation be transferred to a human service desk agent for help.

`dtmf`
:   Sends commands to the phone integration to control input or output using dual-tone multi-frequency (DTMF) signals. (DTMF is a protocol used to transmit the tones that are generated when a user presses keys on a push-button phone.)

`end_session`
:   Sends a command to the channel ending the session. This response type instructs the phone integration to hang up the call.

`iframe`
:   Embeds content from an external website as an HTML `iframe` element.

`image`
:   Displays an image specified by a URL.

`option`
:   Presents a set of options (such as buttons or a drop-down list) that users can choose from. The selected value is then sent to the assistant as user input.

<!-- Pause not yet supported in actions
`pause`
:   Pauses before sending the next message to the channel, and optionally sends a "user is typing" event (for channels that support it).
-->

<!-- Search response type not yet supported in actions
`search`
:   Calls the search integration linked to the assistant to retrieve results that are relevant to the user's query.
-->

`speech_to_text`
:   Sends a command to the {{site.data.keyword.speechtotextshort}} service instance used by the phone integration. These commands can dynamically change the configuration or behavior of the service during a conversation.

`start_activities`
:   Sends a command to a channel integration to start one or more activities that are specific to that channel. You can use this response type to restart any activity you previously stopped using the `stop_activities` response type.

`stop_activities`
:   Sends a command to a channel integration to stop one or more activities that are specific to that channel. The activities remain stopped until they are restarted using the `start_activities` response type.

`text`
:   Displays text (or reads it aloud, for the phone integration). To add variety, you can specify multiple alternative text responses. If you specify multiple responses, you can choose to rotate sequentially through the list, choose a response randomly, or output all specified responses.

`text_to_speech`
:   Sends a command to the {{site.data.keyword.texttospeechshort}} service instance used by the phone integration. These commands can dynamically change the configuration or behavior of the service during a conversation.

`user_defined`
:   A custom response type containing any JSON data the client or integration knows how to handle.

`video`
:   Displays a video specified by a URL.

## Channel integration support for response types
{: #assistant-responses-json-integration-support}

The following table indicates which channel integrations support each type. For additional information about any channel-specific limitations, see [Response types reference](/docs/watson-assistant?topic=watson-assistant-response-types-reference).

| Response type    | Web chat                          | Phone                             | SMS                               | Slack                             | Facebook                          | Whatsapp                          |
|------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| audio            | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |
| connect_to_agent | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   | ![Yes](images/checkmark-icon.svg) |
| dtmf             |                                   | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   |                                   |
| end_session      |                                   | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   |                                   |
| iframe           | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   | ![Yes](images/checkmark-icon.svg) |                                   |
| image            | ![Yes](images/checkmark-icon.svg) |                                   | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |
| option           | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |
| speech_to_text   |                                   | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   |                                   |
| start_activities |                                   | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   |                                   |
| stop_activities  |                                   | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   |                                   |
| text             | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |
| text_to_speech   |                                   | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   |                                   |
| user_defined     | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |
| video            | ![Yes](images/checkmark-icon.svg) |                                   | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |

