---

copyright:
  years: 2023
lastupdated: "2023-02-22"

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
{:preview: .preview}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:table: .aria-labeledby="caption"}
{:video: .video}

# Adding search
{: #search-overview}

Put your subject matter expertise to work by adding search. Search gives your assistant access to corporate data collections that it can mine for answers.
{: shortdesc}

Your assistant can route complex customer inquiries as a search query. It finds information that is relevant to the query from an external data source and returns it to the assistant.

Add search to your assistant to prevent the assistant from having to say things like, `I'm sorry. I can't help you with that`. Instead, the assistant can query existing company documents or data to see whether any useful information can be found and shared with the customer.

You have two options to add search to your assistant:
- The search integration for {{site.data.keyword.discoveryfull}}. For more information, see [Add the search integration for {{site.data.keyword.discoveryfull}}](#search-overview-integration).
- A search extension for Coveo, Google, or NeuralSeek. For more information, see [Add a search extension](#search-overview-extension).

## Add the search integration for {{site.data.keyword.discoveryfull}}
{: #search-overview-integration}

Plus and Enterprise plans include a built-in search integration. You can embed your existing help content by integrating your assistant with search that is provided by {{site.data.keyword.discoveryfull}}. This gives your assistant access to your organization's data collections that it can mine for answers. Customer questions are used as search queries to find relevant answers for your users.

For instructions on adding the built-in search integration, see [{{site.data.keyword.discoveryfull}} search integration setup](/docs/watson-assistant?topic=watson-assistant-search-add).

## Add a search extension
{: #search-overview-extension}

With a search extension, you can "bring your own search" and use content from your website, knowledge base, or content management system.

For instructions on adding a search extension, see:
- [Coveo search extension setup](/docs/watson-assistant?topic=watson-assistant-search-extension-coveo)
- [Google custom search extension setup](/docs/watson-assistant?topic=watson-assistant-search-extension-google)
- [NeuralSeek extension setup](/docs/watson-assistant?topic=watson-assistant-search-extension-neuralseek)
