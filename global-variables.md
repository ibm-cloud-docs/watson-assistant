---

copyright:
  years: 2015, 2023
lastupdated: "2023-10-24"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Built-in global variables
{: #expression-built-in-variables}

By writing expressions, you can access a set of global system variables that provide information about the conversation.

Each variable contains a JSON object that is taken from the `message` method input or output. For more information about these objects, see the [API Reference](https://{DomainName}/apidocs/assistant/assistant-v2#message){: external} information for the `message` method request and response.

These variables are special system objects that require syntax different from the standard variable notation. To reference any of these values in an expression, use the variable name by itself (not including `?` or `{}` characters).
{: important}

| Variable     | Description | Expression example |
|--------------|-------------|---------|
| `input`      | The `input` object from the most recent `message` request sent to the assistant. | `input.text` |
| `output`     | The `output` object from the most recent `message` response. Currently, only `output.debug` is included. | `output.debug.turn_events[0]` |
{: caption="Built-in global system variables" caption-side="top"}

