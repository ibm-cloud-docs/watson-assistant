---

copyright:
  years: 2015, 2024
lastupdated: "2024-05-01"

keywords: conversational search

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Conversational search
{: #conversational-search}

[Plus]{: tag-green} [Enterprise]{: tag-purple}

Use *conversational search* with the {{site.data.keyword.discoveryfull}} search integration or Elasticsearch search integration to help your assistant extract an answer from the highest-ranked query results and return a text response to the user.

When you enable this feature, search results are provided to an IBM watsonx generative AI model that produces a conversational reply to a user's question. 
{: shortdesc}

The watsonx generative AI model is currently hosted only in the Dallas and Frankfurt regions. By default, assistants in all regions except `Frankfurt` use the model from the `Dallas` region. {: important}

To use conversational search, you must have a Plus or Enterprise plan. 

If you enable the conversational search toggle to `on`, you agree to the add-on pricing and terms. Conversational search add-on usage charges will apply from 1 June 2024. For more information about pricing plans, see [Pricing plans](https://cloud.ibm.com/catalog/services/watsonx-assistant?catalog_query=aHR0cHM6Ly9jbG91ZC5pYm0uY29tL2NhdGFsb2c%2Fc2VhcmNoPXdhdHNvbnglMjUyMGFzc2lzdGFudCNzZWFyY2hfcmVzdWx0cw%3D%3D&planId=f0a3dd47-b693-4d73-a8df-aa6baf07a933){: external}. For more information about terms, see [Terms](https://www.ibm.com/support/customer/csol/terms/?id=i128-0038&lc=en){: external}.{: important}

Refer to the following topics to configure the conversational search in your assistant:

- [Before you begin](#conversational-search-requirements)
- [Enable conversational search](#conversational-search-setup) 
- [Configure your assistant to use conversational search](#conversational-search-assistant-configure)
- [Test conversational search](#conversational-search-test)
- [Streaming response support](#conversational-search-streaming-response)

## Before you begin
{: #conversational-search-requirements}

You must configure the search integration to enable the conversational search feature. For more information about configuring {{site.data.keyword.discoveryfull}} search integration, see [{{site.data.keyword.discoveryshort}} search integration setup](/docs/watson-assistant?topic=watson-assistant-search-add). For more information about configuring Elasticsearch integration, see [Elasticsearch search integration setup](/docs/watson-assistant?topic=watson-assistant-search-elasticsearch-add).

## Enable conversational search 
{: #conversational-search-setup}

You can enable the **Conversational search** in the `Search Integration` window by setting the **Conversational search** toggle to `On`. 

You can type `How do we know?` as a default text in the **Define the text for the citation title**. The citation title in the **Conversational search** shows how the responses are generated from various sources and displays the sources of the searched responses. The text in the citation title appears in between the response and the citation titles. 

   Citation title feature is not supported in web chat integration.{: note}
 
The **Define the text for the citation title** is enabled only when **Conversational search** toggle is switched to `On`. In the **Tendency to say I don’t know**, `Less often` is selected by default because the conversational search provides answers most of the times. 

Click `Save` to finish.


 ![ConversationalSearch](images/convo-search-citation-title.png) 
   
For more information about configuring {{site.data.keyword.discoveryshort}}, see [Discovery configure](/docs/watson-assistant?topic=watson-assistant-search-add#search-add-configure). For more information about configuring Elasticsearch, see [Elasticsearch configure](/docs/watson-assistant?topic=watson-assistant-search-elasticsearch-add#setup-elasticsearch).

## Configure your assistant to use the conversational search 
{: #conversational-search-assistant-configure}

After you enable **Conversational search** on **Search integration**, you can enable **Search routing** to use conversational Search. For more information about search routing, see [Configuring the search routing when no action matches](/docs/watson-assistant?topic=watson-assistant-handle-errors#config-search-routing). 

## Test conversational search
{: #conversational-search-test}

You can test the conversational search in actions preview, the preview page, or by using the preview link.

In this example, the user asks, `Tell me about a custom extension`.
Search results are pulled from your knowledge base when the conversational search is `Off`. In this case, the answer is returned as a list of cards that are relevant to custom extensions.

   ![ConversationalSearchToggleOff](images/convo-search-test-toggle-off.png)

When the conversational search is `On`, the same search results are pulled from your knowledge base. The results are passed to an IBM watsonx generative AI model. This model produces a conversational reply to the user's question, in the form of a text response about custom extensions.

   ![ConversationalSearchToggleOn](images/convo-search-test-toggle-on.png)


The citation title feature is not supported in the web chat integration. So, the default text in the citation title is not displayed in the preceding image.

## Streaming response support
{: #conversational-search-streaming-response}

This feature is currently not available in the AI assistant builder of IBM watsonx Orchestrate.{: note}

Streaming response from the conversational search uses watsonx.ai capabilities to provide continuous, real-time responses in your assistant. By default, the streaming response is disabled for the web chat and the assistant preview panels. 

By using the streaming response support feature, you can reduce the wait time for the response. 
{: shortdesc}

To enable streaming response, do the following:

1. Go to **Home** > **Preview** > **Customize web chat**.
1. Click the **Styles** tab.
1. Set the **Streaming** toggle button to `On`.
1. Click **Save and exit**.














