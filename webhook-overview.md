---

copyright:
  years: 2019, 2023
lastupdated: "2023-09-27"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Extending your assistant with webhooks
{: #webhook-overview}

A webhook is a mechanism that you can use to call out to an external program based on events in your program. You can use webhooks to make calls from your assistant to an external service or application during a conversation.
{: shortdesc}

You can use the following types of webhooks in your assistant. They are called with every exchange in a conversation between the customer and the assistant:

- [Premessage](/docs/watson-assistant?topic=watson-assistant-webhook-pre)
- [Postmessage](/docs/watson-assistant?topic=watson-assistant-webhook-post)
- [Logs](/docs/watson-assistant?topic=watson-assistant-webhook-log)

If you are using dialog, you can add a dialog webhook. When used in a dialog skill, a webhook is triggered when the assistant processes a node with a webhook that is enabled. For more information, see [Making a programmatic call from dialog](/docs/assistant?topic=watson-assistant-dialog-webhooks).

| Type | Frequency | Conditions |
| --- | --- | --- |
| Premessage and Postmessage | The message processing webhooks are called with every exchange in a conversation between the customer and the assistant. | For the message processing webhooks, the conditions to check for must be defined in the external application code. For example, even if your webhook performs a simple language translation, you'd want to use a condition to check the language of the incoming message before you send the text to the translation service. |
| Log | The log webhook is called with each message and its corresponding response. | You don't need to define a condition for the log webhook unless you want to filter the messages somehow. In most cases, the goal is to write out every message that is submitted, so the messages can be stored for as long as you want, and analyzed by an external application or service. |
| Dialog | The dialog webhook is called on the rare occasion that the dialog node from which it is triggered is processed. | For a dialog webhook, the conditions to meet is defined in the dialog. If the node condition is not met, then the dialog webhook is never called. |
{: caption="Webhook comparison" caption-side="bottom"}
