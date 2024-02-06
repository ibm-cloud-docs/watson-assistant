---

copyright:
  years: 2023, 2024
lastupdated: "2024-02-06"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Adding search
{: #search-overview}

Put your subject matter expertise to work by adding search. Search gives your assistant access to corporate data collections that it can mine for answers.
{: shortdesc}

Your assistant can route complex customer inquiries as a search query. It finds information that is relevant to the query from an external data source and returns it to the assistant.

Add search to your assistant to prevent the assistant from having to say things like, `I'm sorry. I can't help you with that`. Instead, the assistant can query existing company documents or data to see whether any useful information can be found and shared with the customer.

You have three options to add search to your assistant:
- The search integration for {{site.data.keyword.discoveryfull}}. For more information, see [Add the search integration for {{site.data.keyword.discoveryfull}}](#search-overview-integration).
- The search integration for Elasticsearch. For more information, see [Add the search integration for Elasticsearch](#elasticsearch-integration-overview).
- A search extension for Coveo, Google, or NeuralSeek. For more information, see [Add a search extension](#search-overview-extension).

You can enhance the search integration by using the assistant capabilities such as [Search trigger](/docs/watson-assistant?topic=watson-assistant-search-integration-enhancement#search-add-trigger),  [No action matches](/docs/watson-assistant?topic=watson-assistant-handle-errors#no-action-matches) and [Conversational search](/docs/watson-assistant?topic=watson-assistant-conversational-search#conversational-search-setup). 

For more information about implementing the enhancements for search integration, see [Search integration enhancement](/docs/watson-assistant?topic=watson-assistant-search-integration-enhancement).

## Add the search integration for {{site.data.keyword.discoveryfull}}
{: #search-overview-integration}

Plus and Enterprise plans of {{site.data.keyword.conversationshort}} include a built-in search integration that you can use with your additional, separate instance of {{site.data.keyword.discoveryfull}}. You can embed your existing help content by integrating your assistant with search that is provided by {{site.data.keyword.discoveryfull}}. This gives your assistant access to your organization's data collections that it can mine for answers. Customer questions are used as search queries to find relevant answers for your users.

For instructions on adding the built-in search integration, see [{{site.data.keyword.discoveryfull}} search integration setup](/docs/watson-assistant?topic=watson-assistant-search-add).

## Add the search integration for Elasticsearch
{: #elasticsearch-integration-overview}

You can add the search integration for Elasticsearch if you have Plus or Enterprise plans of {{site.data.keyword.conversationshort}}. Embedding your assistant with the search from Elasticsearch improves the data collection to provide accurate responses to customer queries. 

You can add Elasticsearch from the Environments page or the Integrations page. For instructions on adding search integration for Elasticsearch, see [Elasticsearch search integration setup](/docs/watson-assistant?topic=watson-assistant-search-elasticsearch-add).

## Add a search extension
{: #search-overview-extension}

With a search extension, you can "bring your own search" and use content from your website, knowledge base, or content management system.

For instructions on adding a search extension, see:
- [Coveo search extension setup](/docs/watson-assistant?topic=watson-assistant-search-extension-coveo)
- [Google custom search extension setup](/docs/watson-assistant?topic=watson-assistant-search-extension-google)
- [NeuralSeek extension setup](/docs/watson-assistant?topic=watson-assistant-search-extension-neuralseek)

