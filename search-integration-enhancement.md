---

copyright:
  years: 2023, 2024
lastupdated: "2024-04-02"

subcollection: watson-assistant

---
{{site.data.keyword.attribute-definition-list}}

# Search integration enhancement
{: #search-integration-enhancement}

Use the following enhancements for the search integration to enhance the assistant responses to customer queries.

- [Search trigger](#search-add-trigger)
- [Use search when no action matches](#search-no-action-matches)
- [Use Conversational search](#conversational-search-integration)

## Search trigger 
{: #search-add-trigger}

The search integration is triggered from an action step. By default, the action sends the most recently submitted user message as the search query. However, you can use the search settings within the action step to change the custom search query and custom results filter, which helps you to get accurate results.

For example, the conversational flow might collect information about the type of device a customer wants to buy. When you know the device model, you can then send a model keyword in the query that is submitted to the search integration to get better results.

To configure the search query, complete the following steps:

1. In the *And then* field of the step where you want the search to be triggered, choose **Search for the answer**.

1. Click **Edit settings**.

1. Add values to one or both of the following fields:

    - **Custom search query**. Add a word or phrase that you want to submit to search integration as the query string for the search.

      For example, you can specify a string such as, `What cities do you fly to?`.

      For a more dynamic string, you can include a variable. For example, `Do you have flights to ${destination}?`

      You are effectively defining the value that is used by the search integration API as the `natural_language_query` parameter. For more information about defining query values for {{site.data.keyword.discoveryfull}}, see [Query parameters {{site.data.keyword.discoveryshort}}](/docs/discovery-data?topic=discovery-data-query-parameters){: external}. For more information about defining query values for Elasticsearch, see [Query parameters Elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-filter-context.html#query-context){: external}. 

      If you don't specify a text string, the action sends the most recently submitted user message as the search string.

      If you want to use the original customer message that triggered the action as the query string instead, you need to plan ahead. You can follow these steps:

      1. Create a session variable to store the initial user input. For example, named `original message`.
      1. In Step 1, meaning the first step after the action trigger, set the value of the session variable. For more information about session variables, see [Creating a session variable](/docs/watson-assistant?topic=watson-assistant-manage-info#create-session-variable).
      1. Set the value of the variable by using an expression that looks like this: `<? input.text ?>`.

        This expression captures the complete message that was submitted by the customer. As a result, your variable captures the customer message that triggered this action.
      1. Add the session variable to the *Custom query* field (for example, `${original_message}`).

    - **Custom results filter**: Add a text string that defines information that must be present in any of the search results that are returned.

      You are effectively defining the value that is used by the search integration API as the `filter` parameter. For more information about defining filter values for {{site.data.keyword.discoveryfull}}, see [{{site.data.keyword.discoveryshort}} filter](/docs/discovery-data?topic=discovery-data-query-parameters#filter){: external}. For more information about defining filter values in Elasticsearch, see [Elasticsearch filter](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-filter-context.html#filter-context){: external}

      The syntax to use for the filter value is not intuitive. Here are a few examples of common use cases:

      - To indicate that you want to return only documents with positive sentiment, for example, specify `enriched_text.sentiment.document.label:positive`.

      - To filter results to include only documents that mention `Boston, MA`, specify `enriched_text.entities.text:"Boston, MA"`.

    If you add both a query and a filter value, the filter parameter is applied first to filter the data collection documents and cache the results. The query parameter then ranks the cached results.

    1.  If you want the search for an answer to be the last step in the action, select **End the action after returning results**.

1.  Click **Apply**.

## Use search when no action matches
{: #search-no-action-matches}

You can use the search integration with the built-in [No action matches](/docs/watson-assistant?topic=watson-assistant-handle-errors#no-action-matches) capability. By adding search to *No action matches*, you can have your assistant refer to search when a customer asks a question that isn't addressed by an existing action.



## Use Conversational search
{: #conversational-search-integration}

Conversational search uses the large language models (LLMs) to recognize and respond to customer queries. You can enable this feature in the search integration to improve the assistant responses by using simple conversations.

For more information about Conversational Search, click [Conversational search](/docs/watson-assistant?topic=watson-assistant-conversational-search#conversational-search-setup) 

