---

copyright:
  years: 2019, 2022
lastupdated: "2022-11-03"

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
{:video: .video}

{{site.data.content.classiclink}}

# Extending your assistant with webhooks
{: #webhook-overview}

A webhook is a mechanism that allows you to call out to an external program based on events in your program. You can use webhooks to make calls from your assistant to an external service or application during a conversation.
{: shortdesc}

{{site.data.keyword.conversationshort}} supports the following types of webhooks:

- [Premessage](/docs/watson-assistant?topic=watson-assistant-webhook-pre)
- [Postmessage](/docs/watson-assistant?topic=watson-assistant-webhook-post)
- [Logs](/docs/watson-assistant?topic=watson-assistant-webhook-log)

These webhooks are called with every exchange in a conversation between the customer and the assistant.
  
If you want to limit webhook processing so it happens only in certain situations, any condition to check for before taking an action must be defined in the external application code. For example, if your webhook performs a simple language translation, you might want to use a condition to check the language of the incoming message before sending the text to the translation service.
 
You don't need to define a condition for the log webhook unless you want to filter the messages somehow. In most cases, the goal is to write out every message that is submitted, so the messages can be stored for as long as you want, and analyzed by an external application or service.

Webhooks are configured separately for each environment:

1. Go to the **Environments** page and open the environment where you want to configure webhooks.

1. On the **Environments** page, click the ![Environment settings icon](images/gear-icon-black.png) icon beside the environment title to open the environment settings.
