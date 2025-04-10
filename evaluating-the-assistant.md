---
copyright:
  years: 2015, 2025
lastupdated: "2025-04-09"

keywords: evaluation

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Evaluating the assistant
{: #evaluating-the-assistant}

[Plus]{: tag-green} [Enterprise]{: tag-purple} [IBM Cloud Pak for Data]{: tag-cp4d} [{{site.data.keyword.IBM_notm}} Software Hub]{: tag-teal}

## Overview
{: #evaluating-the-assistant-overview}

You can evaluate and analyze the performance of your assistant by uploading a comprehensive, relevant collection of utterances and sending the utterances to your assistant in a test run.

You can use the **Evaluate** page of {{site.data.keyword.conversationshort}} to upload a collection of sample utterances and run through the utterances on your assistant in one test run. 

Each test utterance within a test run starts a new conversation session.{: note}

When a test run completes, you can view a comprehensive evaluation result. It includes the response routing metrics, conversational search scores (if conversational search is enabled), and response details for any utterance in the uploaded collection. It also includes your assistant settings relevant to the test run.

Evaluation is supported for the draft environment only.

## Before you begin
{: #evaluating-the-assistant-before}

To evaluate the Conversational search performance, in the **Search Integration** window, set the **Conversational search** toggle to `On`. For more information see, [Enabling Conversational search](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-conversational-search#conversational-search-setup).

You can run a maximum of 250 messages per test.
{: note}

### Required format for the CSV file to upload
{: #evaluating-the-assistant-csv-format}

You must follow these criteria for the CSV file to be uploaded. 

- The CSV file must have a single column that includes the text of the utterance to be sent.
- Each row is sent to your assistant sequentially. 
- The CSV has no heading row. 

### Things to consider in writing a CSV
{: #evaluating-the-assistant-csv-writing}

- If your utterance is plain text, it can be written as is. For example, `This is a test utterance` can be written as:
   `This is a test utterance`

- If your utterance contains a comma, you must wrap the line in quotation marks. For example:
   `Hi, this is a second utterance` must be written as `"Hi, this is a second utterance"`

- If your quoted utterance contain quotation marks, those quotation marks must themselves be prefixed by another quotation mark. For example:
   `I have the "best" plan` must be written as `"I have the ""best"" plan"`

## Procedure
{: #evaluating-the-assistant-procedure}

To evaluate the response settings of your assistant, perform the following steps.

1. In the {{site.data.keyword.conversationshort}} home page, click **Evaluate** to open the **Evaluate response settings**.

1. Click **Add file** to select the data. You can upload test data set in .csv format.

1. Click **Start**.

### Conversational search scores
{: #evaluating-the-assistant-conversational-search-scores}

Under **Conversation search scores**, you can view the scores for extractiveness, retrieval confidence, response confidence, average citations per response and average response length of the whole dataset. For more information, see [Conversational search analytics](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-conversational-search-analytics).

### Settings
{: #evaluating-the-assistant-settings}

Under **Settings**, you can view your assistant's settings.

### Filtering the results
{: #evaluating-the-assistant-filter-results}

You can filter the results based on the type of response routing. Click **filter** icon(![Filter icon](images/filter-response.png)) and choose the type of response you want to display from the drop-down menu.

On the **Response details** table, by default you can see the response confidence for each message. Click the **settings** icon(![Settings icon](images/response-details-settings.png)) and choose to display the extractiveness and retrieval confidence for each message from the drop-down menu.

### Exporting the results
{: #evaluating-the-assistant-export-results}

You can export and save the result of the evaluation. Click the **export** icon ![filter icon](images/export-evaluation-results.png) to export the evaluation result table to a .csv file. 

The test result of the latest test run is preserved as per the same retention policy of the chat logs. You can also click the **reset** icon ![Reset icon](images/reset-evaluation-results.png) to delete the result at any time before the test result expires. The result is deleted for all the users.
