---

copyright:
  years: 2021, 2024
lastupdated: "2024-05-02"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Elasticsearch search integration set up 
{: #search-elasticsearch-add}

[Plus]{: tag-green} [Enterprise]{: tag-purple}





1. Click **Finish**.

## Configure your assistant to use Elasticsearch
 {: #search-assistant-configure}

After you configure Elasticsearch integration, you must configure your assistant to use Elasticsearch when the customer response matches no action. For more information about updating **No matches** to use search, see [Use search when no action matches](/docs/watson-assistant?topic=watson-assistant-search-integration-enhancement#search-no-action-matches). 

## Test Elasticsearch
{: #elasticsearch-test}

You can test search integration for Elasticsearch in actions preview, the preview page, or by using the preview link.

In this example, the user asks, `Tell me about a custom extension`.

Search results are pulled from your knowledge base when conversational search is `off`. The answer is, `I searched my knowledge base and found this information which might be useful`.

   ![ConversationalSearchToggleOff](images/convo-search-test-toggle-off.png)

A text-based reply from the best results in your knowledge base displays when conversational search is `on`. 

   ![ConversationalSearchToggleOn](images/convo-search-test-toggle-on.png)

</review>


