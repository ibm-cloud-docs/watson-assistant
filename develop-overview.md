---

copyright:
  years: 2020, 2022
lastupdated: "2022-05-29"

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

# Overview: Customizing and developing
{: #develop-overview}

The {{site.data.keyword.conversationshort}} user interface makes it easy to build an assistant and deploy it to your customers without writing any code. For advanced users and developers, there are powerful ways you can further customize and extend the capabilities of your assistant.
{: shortdesc}

A deployed assistant includes numerous components that work together to deliver the help your customers need over the channels they use.

![{{site.data.keyword.conversationshort}} architecture diagram](images/arch-detail.png)

- Customers interact with the assistant using a **channel** such as the web chat or phone integration.

- Based on natural language understanding, the assistant makes a decision about how to route the customer's request to the appropriate resolution mechanism, which might be an action or a search of existing content.

- The assistant might also need to communicate with external services or hand off the conversation to a human agent.

There are multiple points at which a developer can customize and extend how the assistant behaves, or how it interacts with external services. These customization points include the following:

- Customizing actions: By writing expressions and editing JSON data, you can extensively customize how an action evaluates step conditions, how it stores data, how it responds to customer input, and how it interacts with channels. (More information coming soon.)

- [Web chat development overview](/docs/watson-assistant?topic=watson-assistant-web-chat-develop): You can use the web chat API to extensively customize the appearance and behavior of the web chat.

- Customizing the phone integration: You can use commands and context variables to extensively configure how your assistant interacts with users using the phone integration. (More information coming soon.)

- Customizing the SMS with Twilio integration: You can use commands and context variables to customize how your assistant interacts with users using text messages. (More information coming soon.)

- [Extending your assistant using webhooks](/docs/watson-assistant?topic=watson-assistant-webhook-overview): You use webhooks to call external services that extend the capabilities of your assistant or log activity.

- Developing a custom channel: If none of the built-in channel integrations meet your needs, you can use the {{site.data.keyword.conversationshort}} REST API and SDKs to develop a custom client application that interacts with your assistant. (More information coming soon.)
