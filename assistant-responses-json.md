---

copyright:
  years: 2015, 2023
lastupdated: "2023-10-24"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Defining responses by using the JSON editor
{: #assistant-responses-json}

In some situations, you might need to define your assistant's responses by using the JSON editor. (For more information about assistant responses, see [Adding assistant responses](/docs/watson-assistant?topic=watson-assistant-respond)).
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

Although the `generic` format can be sent to any channel integration, not all channels support all response types, so a particular response might be ignored (or handled differently) by some channels. For more information, see [Channel integration support for response types](#assistant-responses-json-integration-support).

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

For information about the available response types, see [Response types](#assistant-responses-json-response-types).



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

The following response types are available. (For detailed information about how to specify each response type, see [Response types reference](/docs/watson-assistant?topic=watson-assistant-response-types-reference).)

Not all channel integrations support all response types. For information about which integrations support which response types, see [Channel integration support for response types](#assistant-responses-json-integration-support).
{: note}

`audio`
:   Plays an audio clip that is specified by a URL.

`channel_transfer`
:   Requests that the conversation is transferred to a different integration. (Currently, only the web chat integration can be the target of a channel transfer.)

`connect_to_agent`
:   Requests that the conversation is transferred to a contact center with live agents for help.

`date`
:   Requests that the channel collects a date value from the customer (for example, by displaying an interactive calendar).

`dtmf`
:   Sends commands to the phone integration to control input or output by using dual-tone multi-frequency (DTMF) signals. (DTMF is a protocol that is used to transmit the tones that are generated when a user presses keys on a push-button phone.)

`end_session`
:   Sends a command to the channel to end the session. This response type instructs the phone integration to hang up the call.

`iframe`
:   Embeds content from an external website as an HTML `iframe` element.

`image`
:   Displays an image that is specified by a URL.

`option`
:   Presents a set of options (such as buttons or a drop-down list) that users can choose from. The selected value is then sent to the assistant as user input.

`pause`
:   Pauses before sending the next message to the channel, and optionally sends a "user is typing" event (for channels that support it).



`speech_to_text`
:   Sends a command to the {{site.data.keyword.speechtotextshort}} service instance used by the phone integration. These commands can dynamically change the configuration or behavior of the service during a conversation.

`start_activities`
:   Sends a command to a channel integration to start one or more activities that are specific to that channel. You can use this response type to restart any activity you previously stopped by using the `stop_activities` response type.

`stop_activities`
:   Sends a command to a channel integration to stop one or more activities that are specific to that channel. The activities remain stopped until they are restarted by using the `start_activities` response type.

`text`
:   Displays text (or reads it aloud, for the phone integration). To add variety, you can specify multiple alternative text responses. If you specify multiple responses, you can choose to rotate sequentially through the list, choose a response randomly, or output all specified responses.

`text_to_speech`
:   Sends a command to the {{site.data.keyword.texttospeechshort}} service instance used by the phone integration. These commands can dynamically change the configuration or behavior of the service during a conversation.

`user_defined`
:   A custom response type with any JSON data the client or integration knows how to handle.

`video`
:   Displays a video that is specified by a URL.

## Channel integration support for response types
{: #assistant-responses-json-integration-support}

The following table indicates which channel integrations support each type. For additional information about any channel-specific limitations, see [Response types reference](/docs/watson-assistant?topic=watson-assistant-response-types-reference).

| Response type    | Web chat                          | Phone                             | SMS                               | Slack                             | Facebook                          | WhatsApp                          |
|------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| audio            | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |
| channel_transfer |                                   | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |
| connect_to_agent | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   | ![Yes](images/checkmark-icon.svg) |
| date             | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   |                                   |                                   |
| dtmf             |                                   | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   |                                   |
| end_session      |                                   | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   |                                   |
| iframe           | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   | ![Yes](images/checkmark-icon.svg) |                                   |
| image            | ![Yes](images/checkmark-icon.svg) |                                   | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |
| option           | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |
| pause            | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |
| speech_to_text   |                                   | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   |                                   |
| start_activities |                                   | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   |                                   |
| stop_activities  |                                   | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   |                                   |
| text             | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |
| text_to_speech   |                                   | ![Yes](images/checkmark-icon.svg) |                                   |                                   |                                   |                                   |
| user_defined     | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |
| video            | ![Yes](images/checkmark-icon.svg) |                                   | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |
{: caption="Channel integration support" caption-side="bottom"}
