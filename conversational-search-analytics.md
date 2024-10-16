---
copyright:
  years: 2015, 2024
lastupdated: "2024-10-15"

keywords: conversational search

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Conversational search analytics
{: #conversational-search-analytics}

[Plus]{: tag-green} [Enterprise]{: tag-purple} [IBM Cloud Pak for Data]{: tag-cp4d}

## Overview

You can analyze the performance of your conversational search by using a holistic routing graph of your assistant. In the {{site.data.keyword.conversationshort}} home page, go to **Analyze** > **Conversational search** to open the conversational search statistics as a preview.

## Analyzing data and Conversational search scores



![Conversational search analytics](images/conversational-search-analytics-overview.png)

For a single utterance-response pair, you can view the following metrics:

### Response confidence score
The estimated probability that the response correctly answers the user's inquiry given the available content.

### Retrieval confidence score
The estimated probability that the search results have the information that is needed to correctly answer the user's inquiry.

### Extractiveness
The fraction of the response that consists of sequences of words that are in the search results. A high score indicates that much of the response is directly quoted from the sources. A low score indicates that the response is abstracted or paraphrased from the sources. However, it might also mean that the response is not supported by the sources.

### Citations
The number of citations associated with the response.

### Response length
The number of characters in the response.

For all the metrics, the average is the average among all questions for which we generated a response, regardless of whether we provided it or not.
{: note}
