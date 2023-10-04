---

copyright:
  years: 2015, 2023
lastupdated: "2023-10-04"

keywords: conversational search

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Conversational search
{: #conversational-search}

Use *conversational search* with the {{site.data.keyword.discoveryfull}} search integration setup to help your assistant extract an answer from the highest-ranked query results and return a text response to the user.

When you enable this feature, search results are provided to an IBM watsonx generative AI model that produces a conversational reply to a user's question. 

This beta feature is available for evaluation and testing purposes, and is not to be used in production environments. The watsonx generative AI model is currently hosted in the US.
{: important}

## Before you begin
{: #conversational-search-requirements}

To use conversational search, you need to have the {{site.data.keyword.discoveryshort}} search integration. For more information, see [{{site.data.keyword.discoveryfull}} search integration setup](/docs/watson-assistant?topic=search-add).

## Conversational search setup
{: #conversational-search-setup}

After you create the search integration or search skill, connect to an existing {{site.data.keyword.discoveryshort}} instance, and create a project, you can enable the conversational search feature when you configure your search. 

1. Follow steps 1-3 in [Configure the search](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-search-add#search-add-configure).

1. Click the **Conversational search** toggle to turn on.

   ![ConversationalSearch](images/convo-search-toggle-on.png)

1. Follow steps 4-8 in [Configure the search](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-search-add#search-add-configure).

1. Add a trigger to call out to search. For more information, see [Search trigger](/docs/watson-assistant?topic=watson-assistant-search-add#search-add-trigger).

## Test Conversational search
{: #conversational-search-test}

You can test conversational search in actions preview, the preview page, or by using the preview link.

In this example, the user asks, "Am I liable for taxes?" 

   ![ConversationalSearchQuestion](images/conversational-search-question.png)

Search results are pulled from your knowledge base when conversational search is off.

   ![ConversationalSearchResults](images/convo-search-results.png)

A text-based reply from the best results in your knowledge base displays when conversational search is on. The answer is, "Yes, you are liable for taxes." 

   ![ConversationalSearchAnswer](images/conversational-search-answer.png)

