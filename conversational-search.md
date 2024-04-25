---

copyright:
  years: 2015, 2024
lastupdated: "2024-04-25"

keywords: conversational search

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Conversational search
{: #conversational-search}

[Plus]{: tag-green}[Beta]{: tag-cyan}

 This feature is currently not available in the AI assistant builder of IBM watsonx Orchestrate.{: note}

Use *Conversational search* with the {{site.data.keyword.discoveryfull}} search integration or Elasticsearch search integration to help your assistant extract an answer from the highest-ranked query results and return a text response to the user.

When you enable this feature, search results are provided to an IBM watsonx generative AI model that produces a conversational reply to a user's question. 
{: shortdesc}

This beta feature is available in English for evaluation and testing purposes only. The watsonx generative AI model is currently hosted only in the Dallas and Frankfurt regions. To sign up for the beta access to Conversational Search, use the form [here](https://wkf.ms/4bKDCUh){: external}.{: beta}

By default, assistants in all regions except `Frankfurt` use the model from the `Dallas` region. {: important}

To use conversational search, you must have a Plus or Enterprise plan and enroll in the early access program with this [signup form](https://wkf.ms/4bKDCUh){: external}.
Refer to the following topics to configure Conversational search in your assistant:

- [Before you begin](#conversational-search-requirements)
- [Enable Conversational search](#conversational-search-setup) 
- [Configure your assistant to use Conversational search](#conversational-search-assistant-configure)
- [Test Conversational search](#conversational-search-test)
- [Streaming response support](#conversational-search-streaming-response)

## Before you begin
{: #conversational-search-requirements}

You must configure the search integration to enable the Conversational search feature. For more information about configuring {{site.data.keyword.discoveryfull}} search integration, see [{{site.data.keyword.discoveryshort}} search integration setup](/docs/watson-assistant?topic=watson-assistant-search-add). For more information about configuring Elasticsearch integration, see [Elasticsearch search integration setup](/docs/watson-assistant?topic=watson-assistant-search-elasticsearch-add).

## Enable Conversational search 
{: #conversational-search-setup}

You can enable the **Conversational search** in the `Search Integration` window by setting the **Conversational search** toggle to `On`. 

You can type `How do we know?` as a default text in the **Define the text for the citation title**. The citation title in the Conversational search shows how the responses are generated from various sources and displays the sources of the searched responses. The text in the citation title appears in between the response and the citation titles. 

   Citation title feature is not supported in web chat integration.{: note}
 
The **Define the text for the citation title** is enabled only when **Conversational search** toggle is switched to `On`. In the **Tendency to say I don’t know**, `Less often` is selected by default because the Conversational search provides answers most of the times. 

Click `Save` to finish.


 ![ConversationalSearch](images/convo-search-citation-title.png) 
   
For more information about configuring {{site.data.keyword.discoveryshort}}, see [Discovery configure](/docs/watson-assistant?topic=watson-assistant-search-add#search-add-configure). For more information about configuring Elasticsearch, see [Elasticsearch configure](/docs/watson-assistant?topic=watson-assistant-search-elasticsearch-add#setup-elasticsearch).

## Configure your assistant to use Conversational search 
{: #conversational-search-assistant-configure}

After you enable Conversational search on **Search integration**, you can enable **Search routing** to use Conversational Search. For more information about search routing, see [Configuring the search routing when no action matches](/docs/watson-assistant?topic=watson-assistant-handle-errors#config-search-routing). 

## Test Conversational search
{: #conversational-search-test}

You can test the Conversational search in actions preview, the preview page, or by using the preview link.

In this example, the user asks, `Tell me about a custom extension`.
Search results are pulled from your knowledge base when the conversational search is `Off`. In this case, the answer is returned as a list of cards that are relevant to custom extensions.

   ![ConversationalSearchToggleOff](images/convo-search-test-toggle-off.png)

When the Conversational search is `On`, the same search results are pulled from your knowledge base. The results are passed to an IBM watsonx generative AI model. This model produces a conversational reply to the user's question, in the form of a text response about custom extensions.

   ![ConversationalSearchToggleOn](images/convo-search-test-toggle-on.png)


The citation title feature is not supported in the web chat integration. So, the default text in the citation title is not displayed in the preceding image.

## Streaming response support
{: #conversational-search-streaming-response}

Streaming response from the Conversational search uses watsonx.ai capabilities to provide continuous, real-time responses in your assistant. By default, the streaming response is disabled for the web chat and the assistant preview panels. 

By using the streaming response support feature, you can reduce the wait time for the response. 
{: shortdesc}

To enable streaming response, do the following:

1. Go to **Home** > **Preview** > **Customize web chat**.
1. Click the **Styles** tab.
1. Set the **Streaming** toggle button to `On`.
1. Click **Save and exit**.














