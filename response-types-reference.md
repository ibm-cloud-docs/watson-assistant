---

copyright:
  years: 2015, 2022
lastupdated: "2022-05-25"

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

# Response types reference
{: #response-types-reference}

You can use the JSON editor to specify responses of many different types.
{: shortdesc}

For more information about using response types in the JSON editor, see [Defining responses using the JSON editor](/docs/watson-assistant?topic=watson-assistant-assistant-responses-json).

The following response types are supported in the JSON editor.

## `audio`
{: response-types-json-audio}

Plays an audio clip specified by a URL.

### Integration channel support
{: response-types-json-audio-integrations}

| Web chat                          | Phone                             | SMS                               | Slack                             | Facebook                          | Whatsapp                          |
|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |

- Some channel integrations do not display audio titles or descriptions.

### Fields
{: response-types-json-audio-fields}

| Name          | Type   | Description                        | Required? |
|---------------|--------|------------------------------------|-----------|
| response_type | string | `audio`                            | Y         |
| source        | string | The `https:` URL of the audio clip. The URL can specify either an audio file or an audio clip on a supported hosting service. <!-- For more information, see [Adding an *Audio* response type](/docs/assistant?topic=assistant-dialog-overview#dialog-overview-add-audio).--> | Y |
| title         | string | The title to show before the audio player.| N  |
| description   | string | The text of the description that accompanies the audio player. | N |
| alt_text      | string | Descriptive text that can be used for screen readers or other situations where the audio player cannot be seen. | N |
| channel_options.voice_telephony.loop | string | Whether the audio clip should repeat indefinitely (phone integration only). | N |

The URL specified by the `source` property can be either of the following:

- The URL of an audio file in any standard format such as MP3 or WAV. In the web chat, the linked audio clip will render as an embedded audio player.

- The URL of an audio clip on a supported streaming service. In the web chat, the linked audio clip will render using the embeddable player for the hosting service.

    Specify the URL you would use to access the audio file in yourbrowser (for example, `https://soundcloud.com/ibmresearchfallen-star-amped`). You do not need to convert the URL to anembeddable form; the web chat will do this automatically.

    You can embed audio hosted on the following services:
    - [SoundCloud](https://soundcloud.com){: external}
    - [Mixcloud](https://mixcloud.com){: external}

For the phone integration, the URL must specify an audio file that is single-channel (mono) and PCM-encoded, and is sampled at 8,000 Hz with 16 bits per sample.
{: note}

### Example
{: response-types-json-audio-example}

This example plays an audio clip with a title and descriptive text.

```json
{
  "generic":[
    {
      "response_type": "audio",
      "source": "https://example.com/audio/example-file.mp3",
      "title": "Example audio file",
      "description": "An example audio clip returned as part of a multimedia response."
    }
  ]
}
```
{: codeblock}

<!-- Channel transfer not yet supported in actions
## `channel_transfer`
{: response-types-json-channel-transfer}

Requests that the conversation be transferred to a different channel integration. Currently, the web chat integration is the only supported target of a channel transfer.

### Integration channel support
{: response-types-json-channel-transfer-integrations}

| SMS                               | Slack                             | Facebook                          | Whatsapp                          |
|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |

The indicated channel integrations support _initiating_ a channel transfer (currently, the web chat integration is the only supported transfer target).
{: note}

### Fields
{: response-types-json-channel-transfer-fields}

| Name          | Type   | Description        | Required? |
|---------------|--------|--------------------|-----------|
| response_type | string | `channel_transfer` | Y         |
| message_to_user | string | A message to display to the user before the link for initiating the transfer. | Y |
| transfer_info | object | Information used by an integration to transfer the conversation to a different channel. | Y |
| transfer_info.target.chat | string | The URL for the website hosting the web chat to which the conversation is to be transferred. | Y |

### Example
{: response-types-json-channel-transfer-example}

This example requests a transfer from Slack to web chat. In addition to the `channel_transfer` response, the output also includes a `text` response to be displayed by the web chat integration after the transfer. The use of the `channels` array ensures that the `channel_transfer` response is handled only by the Slack integration (before the transfer), and the `connect_to_agent` response only by the web chat integration (after the transfer). For more information about using `channels` to target specific integrations, see [Targeting specific integrations](#assistant-responses-json-target-integrations).

```json
{
  "output": {
    "generic": [
      {
        "response_type": "channel_transfer",
        "channels": [
          {
            "channel": "whatsapp"
          }
        ],
        "message_to_user": "Click the link to connect with an agent using our website.",
        "transfer_info": {
          "target": {
            "chat": {
              "url": "https://example.com/webchat"
            }
          }
        }
      },
      {
        "response_type": "connect_to_agent",
        "channels": [
          {
            "channel": "chat"
          }
        ],
        "message_to_human_agent": "User asked to speak to an agent.",
        "agent_available": {
          "message": "Please wait while I connect you to an agent."
        },
        "agent_unavailable": {
          "message": "I'm sorry, but no agents are online at the moment. Please try again later."
        },
        "transfer_info": {
          "target": {
            "zendesk": {
              "department": "Payments department"
            }
          }
        }
      }
    ]
  }
}
```
{: codeblock}
-->

## `connect_to_agent`
{: response-types-json-connect-to-agent}

Requests that the conversation be transferred to a human service desk agent for help. Service desk support must be configured for the channel integration.

### Integration channel support
{: response-types-json-connect-to-agent-integrations}

| Web chat                          | Phone                             | Whatsapp                          |
|-----------------------------------|-----------------------------------|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |

- For information about adding service desk support to the web chat integration, see [Adding service desk support](/docs/watson-assistant?topic=watson-assistant-deploy-web-chat-haa).
- For information about adding service desk support to the phone integration, see [Configuring backup call center support](/docs/watson-assistant?topic=watson-assistant-deploy-phone-config#deploy-phone-config-transfer-service).

### Fields
{: response-types-json-channel-transfer-fields}

| Name                   | Type   | Description        | Required? |
|------------------------|--------|--------------------|-----------|
| response_type          | string | `connect_to_agent` | Y         |
| message_to_human_agent | string | A message to display to the human agent to whom the conversation is being transferred. | Y |
| agent_available        | string | A message to display to the user when agents are available.                            | Y |
| agent_unavailable      | string | A message to display to the user when no agents are available.                         | Y |
| transfer_info          | object | Information used by the web chat service desk integrations for routing the transfer.   | N |
| transfer_info.target.zendesk.department | string | A valid department from your Zendesk account.                         | N |
| transfer_info.target.salesforce.button_id | string | A valid button ID from your Salesforce deployment.                  | N |

### Example
{: response-types-json-connect-to-agent-example}

This example requests a transfer to a human agent and specifies messages to be displayed both to the user and to the agent at the time of transfer.

```json
{
  "generic": [
    {
      "response_type": "connect_to_agent",
      "message_to_human_agent": "User asked to speak to an agent.",
      "agent_available": {
        "message": "Please wait while I connect you to an agent."
      },
      "agent_unavailable": {
        "message": "I'm sorry, but no agents are online at the moment. Please try again later."
      }
    }
  ]
}
```
{: codeblock}

## `date`
{: response-types-json-date}

Displays an interactive date picker the customer can use to specify a date value.

### Integration channel support
{: response-types-json-date-integrations}

| Web chat                          |
|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) |

- In the web chat, the customer can specify a date value either by clicking the interactive date picker or typing a date value in the input field.

### Fields
{: response-types-json-date-fields}

| Name          | Type   | Description        | Required? |
|---------------|--------|--------------------|-----------|
| response_type | string | `date`             | Y         |

### Example
{: response-types-json-connect-to-agent-example}

This example sends a text response asking the user to specify a date, and then shows an interactive date picker.

```json
{
  "generic": [
    {
      "response_type": "text",
      "text": "What day will you be checking in?"
    },
    {
      "response_type": "date"
    }
  ]
}
```
{: codeblock}

## `dtmf`
{: response-types-json-dtmf}

Sends commands to the phone integration to control input or output using dual-tone multi-frequency (DTMF) signals. (DTMF is a protocol used to transmit the tones that are generated when a user presses keys on a push-button phone.)

### Integration channel support
{: response-types-json-dtmf-integrations}

| Phone                             |
|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) |

### Fields
{: response-types-json-dtmf-fields}

| Name          | Type   | Description        | Required? |
|---------------|--------|--------------------|-----------|
| response_type | string | `dtmf`             | Y         |
| command_info  | object | Information specifying the DTMF command to send to the phone integration. | Y |
| command_info.type | string | The DTMF command to send (`collect`, `disable_barge_in`, `enable_barge_in`, or `send`). | Y |
| command_info.parameters | object | See [Handling phone interactions](/docs/watson-assistant?topic=phone-actions) | N |

The `command_info.type` field can specify any of the following supported commands:

- `collect`: Collects DTMF keypad input.
- `disable_barge_in`: Disables DTMF barge-in so that playback from the phone integration is not interrupted when the customer presses a key.
- `enable_barge_in`: Enables DTMF barge-in so that the customer can interrupt playback from the phone integration by pressing a key.
- `send`: Sends DTMF signals.

For detailed information about how to use each of these commands, see [Handling phone interactions](/docs/watson-assistant?topic=watson-assistant-phone-actions).

### Example

This example shows the `dtmf` response type with the `collect` command, used to collect DTMF input. For more information, including examples of other DTMF commands, see [Handling phone interactions](/docs/watson-assistant?topic=watson-assistant-phone-actions).

```json
{
  "generic": [
    {
      "response_type": "dtmf",
      "command_info": {
        "type": "collect",
        "parameters": {
          "termination_key": "#",
          "count": 16,
          "ignore_speech": true
        }
      },
      "channels": [
        {
          "channel": "voice_telephony"
        }
      ]
    }
  ]
}
```
{: codeblock}

## `end_session`
{: response-types-json-end-session}

Sends a command to the channel ending the session. This response type instructs the phone integration to hang up the call.

### Integration channel support
{: response-types-json-end-session-integrations}

| Phone                             | SMS                               |
|-----------------------------------|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) |                                   |

- The SMS with Twilio integration supports ending a session by using the `terminateSession` action command. <!-- For more information, see XXXX -->

### Fields
{: response-types-json-end-session-fields}

| Name          | Type   | Description        | Required? |
|---------------|--------|--------------------|-----------|
| response_type | string | `end_session`      | Y         |

For the phone integration, you can use the `channel_options` object to include custom headers with the SIP `BYE` request that is generated. For more information, see [End the call](/docs/watson-assistant?topic=watson-assistant-phone-actions#phone-actions-hangup).

### Example

This example uses the `end_session` response type to end a conversation.

```json
{
  "generic": [
    {
      "response_type": "end_session"
    }
  ]
}
```
{: codeblock}

## `iframe`
{: response-types-json-iframe}

Embeds content from an external website as an HTML `iframe` element.

### Integration channel support
{: response-types-json-iframe-integrations}

| Web chat                          | Facebook                          |
|-----------------------------------|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |

- Currently, the web chat integration ignores the `description` and `image_url` properties. Instead, the description and preview image are dynamically retrieved from the source at run time.

### Fields
{: response-types-json-iframe-fields}

| Name          | Type   | Description                        | Required? |
|---------------|--------|------------------------------------|-----------|
| response_type | string | `iframe`                           | Y         |
| source        | string | The URL of the external content. The URL must specify content that is embeddable in an HTML `iframe` element. <!-- For more information, see [Adding an *iframe* response type](/docs/assistant?topic=assistant-dialog-overview#dialog-overview-add-iframe).--> | Y |
| title         | string | The title to show before the embedded content. | N |
| description   | string | The text of the description that accompanies the embedded content. | N |
| image_url     | string | The URL of an image that shows a preview of the embedded content. | N |

Note that different sites have varying restrictions for embedding content, and different processes for generating embeddable URLs. An embeddable URL is one that can be specified as the value of the `src` attribute of the `iframe` element.

For example, to embed an interactive map using Google Maps, you can use the Google Maps Embed API. (For more information, see [The Maps Embed API overview](https://developers.google.com/maps/documentation/embed/get-started){: external}.) Other sites have different processes for creating embeddable content.

For technical details about using `Content-Security-Policy: frame-src` to allow embedding of your website content, see [CSP: frame-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-src){: external}.

### Example
{: response-types-json-iframe-example}

This example embeds an iframe with a title and description.

```json
{
  "generic":[
    {
      "response_type": "iframe",
      "source": "https://example.com/embeddable/example",
      "title": "Example iframe",
      "description": "An example of embeddable content returned as an iframe response."
    }
  ]
}
```
{: codeblock}

## `image`
{: response-types-json-image}

Displays an image specified by a URL.

### Integration channel support
{: response-types-json-image-integrations}

| Web chat                          | SMS                               | Slack                             | Facebook                          | Whatsapp                          |
|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |

- Some channel integrations do not display image titles or descriptions.

### Fields
{: response-types-json-image-fields}

| Name          | Type   | Description                        | Required? |
|---------------|--------|------------------------------------|-----------|
| response_type | string | `image`                            | Y         |
| source        | string | The `https:` URL of the image. The specified image must be in `.jpg`, `.gif`, or `.png` format. | Y |
| title         | string | The title to show before the image. | N        |
| description   | string | The text of the description that accompanies the image. | N |
| alt_text      | string | Descriptive text that can be used for screen readers or other situations where the image cannot be seen. | N |

### Example
{: response-types-json-image-example}

This example displays an image with a title and descriptive text.

```json
{
  "generic":[
    {
      "response_type": "image",
      "source": "https://example.com/image.jpg",
      "title": "Example image",
      "description": "An example image returned as part of a multimedia response."
    }
  ]
}
```
{: codeblock}

## `option`
{: response-types-json-option}

Presents a set of options (such as buttons or a drop-down list) that users can choose from. The selected value is then sent to the assistant as user input. An `options` response is automatically defined when you choose the **Options** customer response type for a step (for more information, see [Collecting information from your customers](/docs/watson-assistant?topic=watson-assistant-collect-info)).

### Integration channel support
{: response-types-json-option-integrations}

| Web chat                          | Phone                             | SMS                               | Slack                             | Facebook                          | Whatsapp                          |
|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |

- The way in which options are presented varies depending on the channel integration. The `preference` field is supported when possible, but not all channels support drop-down lists or buttons.

### Fields
{: response-types-json-option-fields}

| Name          | Type   | Description                         | Required? |
|---------------|--------|-------------------------------------|-----------|
| response_type | string | `option`                            | Y         |
| title         | string | The title to show before the options. | Y       |
| description   | string | The text of the description that accompanies the options. | N |
| preference    | string | The preferred type of control to display, if supported by the channel (`dropdown` or `button`). | N |
| options       | list   | A list of key/value pairs specifying the options from which the user can choose. | Y |
| options[].label | string | The user-facing label for the option. | Y     |
| options[].value | object | An object defining the response that will be sent to the {{site.data.keyword.conversationshort}} service if the user selects the option. | Y |
| options[].value.input | object | An object that includes the message input corresponding to the option, including input text and any other field that is a valid part of a {{site.data.keyword.conversationshort}} message. For more information about the structure of message input, see the [API Reference](https://cloud.ibm.com/apidocs/assistant/assistant-v2?curl=#message){: external}. | N |

### Example
{: response-types-json-option-example}

This example presents two options (`Buy something` and `Exit`).

```json
{
  "generic":[
    {
      "response_type": "option",
      "title": "Choose from the following options:",
      "preference": "button",
      "options": [
        {
          "label": "Buy something",
          "value": {
            "input": {
              "text": "Place order"
            }
          }
        },
        {
          "label": "Exit",
          "value": {
            "input": {
              "text": "Exit"
            }
          }
        }
      ]
    }
  ]
}
```
{: codeblock}

<!-- Pause not yet supported in actions
## `pause`
{: response-types-json-pause}

Pauses before sending the next message to the channel, and optionally sends a "user is typing" event (for channels that support it).

### Integration channel support
{: response-types-json-pause-integrations}

| Web chat                          | Phone                             | SMS                               | Facebook                          | Whatsapp                          |
|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) |                                   |                                   | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |

<!-- - With the phone integration, you can add a pause by using the `turn_settings.timeout_count` context variable (for more information, see [Context variables that are set by your dialog or actions](/docs/watson-assistant?topic=watson-assistant-phone-context#phone-context-variables-set-by-dialog)).
- With the SMS with Twilio integration, you can add a pause by using the `vgwConversationResponseTimeout` context variable (for more information, see [Context variables that are set by your action](/docs/watson-assistant?topic=watson-assistant-sms-reference#sms-reference-context-variables-set-by-action).

### Fields
{: response-types-json-pause-fields}

| Name          | Type   | Description        | Required? |
|---------------|--------|--------------------|-----------|
| response_type | string | `pause`            | Y         |
| time          | int    | How long to pause, in milliseconds. | Y |
| typing        | boolean | Whether to send the "user is typing" event during the pause. Ignored if the channel does not support this event. | N |

### Example
{: response-types-json-pause-example}

This examples sends the "user is typing" event while pausing for 5 seconds.

```json
{
  "output": {
    "generic":[
      {
        "response_type": "pause",
        "time": 5000,
        "typing": true
      }
    ]
  }
}
```
{: codeblock}
-->

<!-- Search not yet supported in actions. This also needs to be updated so it does not refer to search_skill (unless it is ultimately replaced by something else)
## `search`
{: response-types-json-search}

Calls the search skill linked to the assistant to retrieve results that are relevant to the user's query.

### Integration channel support
{: response-types-json-search-integrations}

| Web chat                          | Phone                             | SMS                               | Slack                             | Facebook                          | Whatsapp                          |
|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |

- The phone integration reads the introductory message (for example, `I found this information that might be helpful`), and then the body of only the first search result.

### Fields
{: response-types-json-search-skill-fields}

| Name          | Type   | Description        | Required? |
|---------------|--------|--------------------|-----------|
| response_type | string | `search`           | Y         |
| query         | string | The text to use for the search query. This string can be empty, in which case the user input is used as the query. | Y |
| filter        | string | An optional filter that narrows the set of documents to be searched. | N |
| query_type    | string | The type of search query to use (`natural_language` or `discovery_query_language`). | Y |
| discovery_version | string | The version of the Discovery service API to use. The default is `2018-12-03`. | N |

### Example
{: response-types-json-search-skill-example}

This examples uses the user input text to send a natural-language query to the search skill.

```json
{
  "output": {
    "generic": [
      {
        "response_type": "search_skill",
        "query": "",
        "query_type": "natural_language"
      }
    ]
  }
}
```
{: codeblock}
-->

## `speech_to_text`
{: response-types-json-speech-to-text}

Sends a command to the {{site.data.keyword.speechtotextshort}} service instance used by the phone integration. These commands can dynamically change the configuration or behavior of the service during a conversation.

### Integration channel support
{: response-types-json-speech-to-text-integrations}

| Phone                             |
|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) |

### Fields
{: response-types-json-speech-to-text-fields}

| Name          | Type   | Description        | Required? |
|---------------|--------|--------------------|-----------|
| response_type | string | `speech_to_text`   | Y         |
| command_info  | object | Information specifying the command to send to the {{site.data.keyword.speechtotextshort}}. | Y |
| command_info.type | string | The command to send (currently only the `configure` command is supported). | Y |
| command_info.parameters | object | See [Applying advanced settings to the {{site.data.keyword.speechtotextshort}} service](/docs/watson-assistant?topic=watson-assistant-phone-actions#phone-actions-speech-advanced) | N |

The `command_info.type` field can specify any of the following supported commands:

- `configure`: Dynamically updates the {{site.data.keyword.speechtotextshort}} configuration. Configuration changes can be applied only to the next conversation turn, or for the rest of the session.

For detailed information about how to this command, see [Applying advanced settings to the {{site.data.keyword.speechtotextshort}} service](/docs/watson-assistant?topic=watson-assistant-phone-actions#phone-actions-speech-advanced).

### Example

This example uses the `speech_to_text` response type with the `configure` command to change the language model used by the {{site.data.keyword.texttospeechshort}} service to Spanish, and to enable smart formatting.

```json
{
  "generic": [
    {
      "response_type": "speech_to_text",
      "command_info": {
        "type": "configure",
        "parameters": {
          "narrowband_recognize": {
            "model": "es-ES_NarrowbandModel",
            "smart_formatting": true
          }
        }
      },
      "channels":[
        {
          "channel": "voice_telephony"
        }
      ]
    }
  ]
}
```
{: codeblock}

## `start_activities`
{: response-types-json-start-activities}

Sends a command to a channel integration to start one or more activities that are specific to that channel. You can use this response type to restart any activity you previously stopped using the `stop_activities` response type.

### Integration channel support
{: response-types-json-start-activities-integrations}

| Phone                             |
|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) |

### Fields
{: response-types-json-start-activities-fields}

| Name          | Type   | Description        | Required? |
|---------------|--------|--------------------|-----------|
| response_type | string | `start_activities` | Y         |
| activities    | list   | A list of objects identifying the activities to start. | Y |
| activities[].type | string | The name of the activity to start. | Y |

Currently, the following activities for the phone integration can be started:

- `speech_to_text_recognition`: Starts recognizing speech. Streaming audio to the {{site.data.keyword.speechtotextshort}} service is resumed.
- `dtmf_collection`: Starts processing of inbound DTMF signals.

### Example

This example uses the `start_activities` response type to restart recognizing speech. Because this command is specific to the phone integration, the `channels` property specifies `voice_telephony` only.

```json
{
  "generic": [
    {
      "response_type": "start_activities",
      "activities": [
        {
          "type": "speech_to_text_recognition"
        }
      ],
      "channels":[
        {
          "channel": "voice_telephony"
        }
      ]
    }
  ]
}
```
{: codeblock}

## `stop_activities`
{: response-types-json-stop-activities}

Sends a command to a channel integration to stop one or more activities that are specific to that channel. The activities remain stopped until they are restarted using the `start_activities` response type.

### Integration channel support
{: response-types-json-stop-activities-integrations}

| Phone                             |
|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) |

### Fields
{: response-types-json-stop-activities-fields}

| Name          | Type   | Description        | Required? |
|---------------|--------|--------------------|-----------|
| response_type | string | `stop_activities`  | Y         |
| activities    | list   | A list of objects identifying the activities to stop. | Y |
| activities[].type | string | The name of the activity to stop. | Y |

Currently, the following activities for the phone integration can be stopped:

- `speech_to_text_recognition`: Stops recognizing speech. All streaming audio to the {{site.data.keyword.speechtotextshort}} service is stopped.
- `dtmf_collection`: Stops processing of inbound DTMF signals.

### Example

This example uses the `stop_activities` response type to stop recognizing speech. Because this command is specific to the phone integration, the `channels` property specifies `voice_telephony` only.

```json
{
  "generic": [
    {
      "response_type": "stop_activities",
      "activities": [
        {
          "type": "speech_to_text_recognition"
        }
      ],
      "channels":[
        {
          "channel":"voice_telephony"
        }
      ]
    }
  ]
}
```
{: codeblock}

## `text`
{: response-types-json-text}

Displays text (or reads it aloud, for the phone integration). To add variety, you can specify multiple alternative text responses. If you specify multiple responses, you can choose to rotate sequentially through the list, choose a response randomly, or output all specified responses.

### Integration channel support
{: response-types-json-text-integrations}

| Web chat                          | Phone                             | SMS                               | Slack                             | Facebook                          | Whatsapp                          |
|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |

### Fields
{: response-types-json-text-fields}

| Name          | Type   | Description        | Required? |
|---------------|--------|--------------------|-----------|
| response_type | string | `text`             | Y         |
| values        | list   | A list of one or more objects defining text response. | Y |
| values.[_n_].text_expression | object | An object describing the text of the response. | N |
| values.[_n_].text_expression.concat | list | A list of objects that form components of the text response. These objects can include scalar text strings and references to variables. | N |
| selection_policy | string | How a response is selected from the list, if more than one response is specified. The possible values are `sequential`, `random`, and `multiline`. | N |
| delimiter     | string | The delimiter to output as a separator between responses. Used only when `selection_policy`=`multiline`. The default delimiter is newline (`\n`). | N |

### Example
{: response-types-json-text-example}

This examples displays a greeting message to the user.

```json
{
  "generic": [
    {
      "response_type": "text",
      "values": [
        {
          "text_expression": {
            "concat": [
              {
                "scalar": "Hi, "
              },
              {
                "variable": "step_472"
              },
              {
                "scalar": ". How can I help you?"
              }
            ]
          }
        }
      ],
      "selection_policy": "sequential"
    }
  ]
}  
```
{: codeblock}

## `text_to_speech`
{: response-types-json-text-to-speech}

Sends a command to the {{site.data.keyword.texttospeechshort}} service instance used by the phone integration. These commands can dynamically change the configuration or behavior of the service during a conversation.

### Integration channel support
{: response-types-json-text-to-speech-integrations}

| Phone                             |
|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) |

### Fields
{: response-types-json-text-to-speech-fields}

| Name          | Type   | Description        | Required? |
|---------------|--------|--------------------|-----------|
| response_type | string | `text_to_speech`   | Y         |
| command_info  | object | Information specifying the command to send to the {{site.data.keyword.texttospeechshort}}. | Y |
| command_info.type | string | The command to send (`configure`, `disable_barge_in`, or `enable_barge_in`). | Y |
| command_info.parameters | object | See [Applying advanced settings to the {{site.data.keyword.texttospeechshort}} service](/docs/watson-assistant?topic=watson-assistant-phone-actions#phone-actions-text-advanced) | N |

The `command_info.type` field can specify any of the following supported commands:

- `configure`: Dynamically updates the {{site.data.keyword.texttospeechshort}} configuration. Configuration changes can be applied only to the next conversation turn, or for the rest of the session.
- `disable_barge_in`: Disables speech barge-in so that playback from the phone integration is not interrupted when the customer speaks.
- `enable_barge_in`: Enables speech barge-in so that the customer can interrupt playback from the phone integration by speaking.

For detailed information about how to use each of these commands, see [Applying advanced settings to the {{site.data.keyword.texttospeechshort}} service](/docs/watson-assistant?topic=watson-assistant-phone-actions#phone-actions-text-advanced).

### Example

This example uses the `text_to_speech` response type with the `configure` command to change the voice used by the {{site.data.keyword.texttospeechshort}} service.

```json
{
  "generic": [
    {
      "response_type": "text_to_speech",
      "command_info": {
        "type": "configure",
        "parameters" : {
          "synthesize": {
            "voice": "en-US_LisaVoice"
          }          
        }
      },
      "channels":[
        {
          "channel": "voice_telephony"
        }
      ]
    }
  ]
}
```
{: codeblock}

## `user_defined`
{: response-types-json-user-defined}

A custom response type containing any JSON data the client or integration knows how to handle. For example, you might customize the web chat to display a special kind of card, or build a custom application to format responses using a table or chart.

The user-defined response type is not displayed unless the channel has code to handle it. For more information about customizing the web chat, see [Applying advanced customizations](/docs/watson-assistant?topic=watson-assistant-web-chat-config). <!-- For more information about handling responses in a custom client app, see [Implementing responses](/docs/assistant?topic=assistant-api-dialog-responses).-->
{: note}

### Integration channel support
{: response-types-json-user-defined-integrations}

| Web chat                          | Phone                             | SMS                               | Slack                             | Facebook                          | Whatsapp                          |
|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg)*| ![Yes](images/checkmark-icon.svg)*| ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |

- With the phone integration, the `user_defined` response type is used to send legacy commands (for example, `vgwActForceNoInputTurn` or `vgwActSendSMS`). For more information, see [Handling phone interactions](/docs/watson-assistant?topic=watson-assistant-phone-actions).
- With the SMS with Twilio integration, the `user_defined` response type is used to send action commands (for example, `terminateSession` or `smsActSendMedia`). <!-- For more information, see XXXX -->

### Fields
{: response-types-json-user-defined-fields}

| Name          | Type   | Description        | Required? |
|---------------|--------|--------------------|-----------|
| response_type | string | `user_defined`     | Y         |
| user_defined  | object | An object containing any data the client or integration knows how to handle. This object can contain any valid JSON data, but it cannot exceed a total size of 5000 bytes. | Y |

### Example
{: response-types-json-user-defined-example}

This examples shows a generic example of a user-defined response. The `user_defined` object can contain any valid JSON data.

```json
{
  "generic":[
    {
      "response_type": "user_defined",
      "user_defined": {
        "field_1": "String value",
        "array_1": [
          1,
          2
        ],
        "object_1": {
          "property_1": "Another string value"
        }
      }
    }
  ]
}
```
{: codeblock}

## `video`
{: response-types-json-video}

Displays a video specified by a URL.

### Integration channel support
{: response-types-json-video-integrations}

| Web chat                          | SMS                               | Slack                             | Facebook                          | Whatsapp                          |
|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) | ![Yes](images/checkmark-icon.svg) |

- Some channel integrations do not video titles or descriptions.

### Fields
{: response-types-json-video-fields}

| Name          | Type   | Description                        | Required? |
|---------------|--------|------------------------------------|-----------|
| response_type | string | `video`                            | Y         |
| source        | string | The `https:` URL of the video. The URL can specify either a video file or a streaming video on a supported hosting service. <!-- For more information, see [Adding a *Video* response type](/docs/assistant?topic=assistant-dialog-overview#dialog-overview-add-video).--> | Y |
| title         | string | The title to show before the video.| N         |
| description   | string | The text of the description that accompanies the video. | N |
| alt_text      | string | Descriptive text that can be used for screen readers or other situations where the video cannot be seen. | N |
| channel_options.chat.dimensions.base_height | string | The base height (in pixels) to use to scale the video to a specific display size. | N |

The URL specified by the `source` property can be either of the following:

- The URL of a video file in a standard format such as MPEG or AVI. In the web chat, the linked video will render as an embedded video player.

    HLS (`.m3u8`) and DASH (MPD) streaming videos are not supported.

- The URL of a video hosted on a supported video hosting service. In the web chat, the linked video will render using the embeddable player for the hosting service.

    Specify the URL you would use to view the video in your browser (for example, `https://www.youtube.com/watch?v=52bpMKVigGU`). You do not need to convert the URL to an embeddable form; the web chat will do this automatically.

    You can embed videos hosted on the following services:
    - [YouTube](https://youtube.com){: external}
    - [Facebook](https://facebook.com){: external}
    - [Vimeo](https://vimeo.com){: external}
    - [Twitch](https://twitch.tv){: external}
    - [Streamable](https://streamable.com){: external}
    - [Wistia](https://wistia.com){: external}
    - [Vidyard](https://vidyard.com){: external}

### Example
{: response-types-json-video-example}

This example displays an video with a title and descriptive text.

```json
{
  "generic":[
    {
      "response_type": "video",
      "source": "https://example.com/videos/example-video.mp4",
      "title": "Example video",
      "description": "An example video returned as part of a multimedia response."
    }
  ]
}
```
{: codeblock}

