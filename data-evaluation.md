---
copyright:
  years: 2015, 2024
lastupdated: "2024-12-09"

keywords: evaluation

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Evaluating the assistant
{: #evaluating-the-assistant}

[Plus]{: tag-green} [Enterprise]{: tag-purple} [IBM Cloud Pak for Data]{: tag-cp4d}

## Overview

You can evaluate and analyze the performance of your assistant by uploading a comprehensive, relevant collection of utterances and sending the utterances to your assistant in a test run.

You can use the **Evaluate** page of watsonx Assistant to upload a collection of sample utterances and run through the utterances on your assistant in one test run. 

When a test run completes, you can view a comprehensive evaluation result. It includes the response routing metrics, conversational search scores(if conversational search is enabled), and response details for any utterance in the uploaded collection. It also includes your assistant settings relevant to the test run.

Evaluation is supported for the draft environment only.



### Conversational search scores

Under **Conversation search scores**, you can view the scores for extractiveness, retrieval confidence, response confidence, average citations per response and average response length of the whole dataset. For more information, see [Conversational search analytics](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-conversational-search-analytics).

### Settings

Under **Settings**, you can view your assistant's settings.

### Filtering the results

You can filter the results based on the type of response routing. Click **filter** icon(![Filter icon](images/filter-response.png)) and choose the type of response you want to display from the drop-down menu.

On the **Response details** table, by default you can see the response confidence for each message. Click the **settings** icon(![Settings icon](images/response-details-settings.png)) and choose to display the extractiveness and retrieval confidence for each message from the drop-down menu.

### Exporting the results

You can export and save the result of the evaluation. Click the **export** icon(![filter icon](images/export-evaluation-results.png)) to export the evaluation result table to a .csv file. 

The test result of the latest test run is preserved as per the same retention policy of the chat logs. You can also click the **reset** icon(![Reset icon](images/reset-evaluation-results.png)) to delete the result at any time before the test result expires. The result is deleted for all the users.
