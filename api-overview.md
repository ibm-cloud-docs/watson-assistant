---

copyright:
  years: 2015, 2024
lastupdated: "2024-12-20"

subcollection: watson-assistant


---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.conversationshort}} API overview
{: #api-overview}

You can use the {{site.data.keyword.conversationshort}} REST APIs, and the corresponding SDKs, to develop applications that interact with the service.

## Client applications
{: #api-overview-client-applications}

To build a virtual assistant or other client application that communicates with an assistant at run time, use the v2 API. You can develop a customer-facing client that can be deployed for production use, an application that brokers communication between an assistant and another service, or a testing application.

By using the v2 runtime API to communicate with your assistant, your application can take advantage of the following features:

- **Automatic state management.** The v2 runtime API manages each session with a user, storing and maintaining all of the context data your assistant needs for a complete conversation.

- **Ease of deploying assistants.** In addition to supporting custom clients, an assistant can be easily deployed to popular messaging channels such as Slack and Facebook Messenger.

- **Versioning.** You can save a snapshot of your content and link your assistant to that specific version. You can then continue to update your development version without affecting the production assistant.

- **Search capabilities.** The v2 runtime API can be used to receive responses from the search integration. When a query is submitted that your assistant can't answer, the search integration can find the best answer from the configured data sources.

For more information, see the [{{site.data.keyword.conversationshort}} v2 API reference](/apidocs/assistant-v2){: external}.

The {{site.data.keyword.conversationshort}} v1 API supports the `/message` method that sends user input directly to the workspace used by a dialog. The v1 runtime API is supported primarily for compatibility. If you use the v1 `/message` method, you must implement your own state management, and you cannot take advantage of versioning or any of the other features of an assistant.
{: note}

## Authoring applications
{: #api-overview-authoring-applications}

The v1 API provides methods that enable an application to create or modify dialog skills, as an alternative to building a skill graphically by using the classic {{site.data.keyword.assistant_classic_short}} user interface. An authoring application uses the API to create and modify skills, intents, entities, dialog nodes, and other artifacts that make up a dialog skill. For more information, see the [v1 API Reference](/apidocs/assistant-v1){: external}.

The v1 authoring methods create and modify workspaces rather than skills. A workspace is a container for the dialog and training data (such as intents and entities) within a dialog skill. If you create a new workspace by using the API, it appears as a new dialog skill in the classic {{site.data.keyword.assistant_classic_short}} user interface.
{: note}

For a list of the available API methods, see [API methods summary](/docs/watson-assistant?topic=watson-assistant-api-methods).
