---

copyright:
  years: 2015, 2023
lastupdated: "2023-01-23"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Built-in variables
{: #expression-built-in-variables}

You can write expressions that access variables and properties of variables (for more information, see [Writing expressions](/docs/watson-assistant?topic=watson-assistant-expressions)). In addition to the variables you can select in the {{site.data.keyword.conversationshort}} user interface, with expressions you can also access a set of global system variables that provide information about the conversation, as well as variables set by integrations.

## Built-in global system variables
{: #expression-global-variables}

Global system variables provide information about the current conversation. Each variable returns a JSON object that is part of the `message` method input or output. For more information about these objects, see the [API Reference](/apidocs/assistant/assistant-v2#message){: external} information for the `message` method request and response.

These variables are special system objects that require syntax different from the standard variable notation. To reference any of these values in an expression, use the variable name by itself (not including `?` or `{}` characters).
{: important}

| Variable     | Description | Expression example |
|--------------|-------------|---------|
| `entities[]` | The `output.entities` array from the most recent `message` response.  | `entities[0].value` |
| `intents[]`  | The `output.intents` array from the most recent `message` response. | `intents[0].confidence` |
| `input`      | The `input` object from the most recent `message` request sent to the assistant. | `input.text` |
| `output`     | The `output` object from the most recent `message` response. Currently, only `output.debug` is included. | `output.debug.turn_events[0]` |
{: caption="Built-in global system variables" caption-side="top"}

## Integration variables
{: #expression-integration-variables}

Integration variables are context variables that are specific to integrations (such as the web chat and phone integrations). All integration variables are contained in the `system_integrations` JSON object, which you can access using the following expression:

```text
${system_integrations}
```

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

### `channel`
{: #expression-integration-variables-channel}

Always included. This object contains general information about the channel that is being used to communicate with the assistant.

| Name                                | Type   | Description |
|-------------------------------------|--------|-------------|
| `channel.name`                      | String | The name of the channel that is in use. One of the following values: \n - `Web chat` \n - `Phone` \n - `SMS` \n - `Whatsapp` \n - `Slack` \n - `Facebook Messenger` |
| `channel.private.user.id            | String | The ID of the user who is interacting with the assistant through the channel. Set by the channel. |
| `channel.private.user.phone_number` | String | The phone number associated with the user. Set by the phone, SMS, and WhatsApp integrations. |
{: caption="Fields of the channel object" caption-side="top"}

The `user.id` and `user.phone_number` properties are private variables. Private variables are not included in logs.
{: note}

### `chat`
{: #expression-integration-variables-chat}

Included only if the web chat integration is in use.

