---

copyright:
  years: 2015, 2024
lastupdated: "2024-12-27"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Advanced analysis and log-related tasks
{: #logs-resources}

## Classic experience only
This information applies to dialog skill analytics in the classic experience. For information about analytics in {{site.data.keyword.conversationshort}}, see [Use analytics to review your entire assistant at a glance](/docs/watson-assistant?topic=watson-assistant-analytics-overview). 
{: attention}

Learn about notebooks and APIs that you can use to access and analyze log data.
{: shortdesc}

## Using Jupyter notebooks for analysis
{: #logs-resources-jupyter-notebooks}

IBM created Jupyter notebooks that you can use to analyze the behavior or your assistant. A Jupyter notebook is a web-based environment for interactive computing. You can run small pieces of code that process your data, and you can immediately view the results of your computation.

You can use the notebooks with English-language skills only.
{: note}

### Analysis notebooks
{: #logs-resources-jupyter-logs}

Analysis notebooks are available for:
- {{site.data.keyword.DSX_full}}
- Standard Python tools

{{site.data.keyword.DSX_short}} provides an environment where you can:
- Choose the tools that you need to analyze and visualize data.
- Cleanse and shape data.
- Ingest streaming data.
- Create, train, and deploy machine learning models. 

For more information, see the [product documentation](https://dataplatform.cloud.ibm.com/docs/content/svc-welcome/wsl.html?context=cpdaas){: external}.

The [{{site.data.keyword.conversationshort}} Continuous Improvement Best Practices Guide](https://raw.githubusercontent.com/watson-developer-cloud/assistant-improve-recommendations-notebook/master/notebook/IBM%20Watson%20Assistant%20Continuous%20Improvement%20Best%20Practices.pdf){: external} describes how to get the most out of these notebooks.

### Using the notebooks with {{site.data.keyword.DSX}}
{: #logs-resources-notebooks-studio}

The following notebooks are available:

- [Dialog skill analysis for {{site.data.keyword.conversationshort}}](https://dataplatform.cloud.ibm.com/exchange/public/entry/view/4d77701840fcb2f21587e39fdb887049){: external}
- [Measure {{site.data.keyword.conversationshort}} Performance](https://dataplatform.cloud.ibm.com/exchange/public/entry/view/133dfc4cd1480bbe4eaa78d3f635e568){: external}.
- [Analyze {{site.data.keyword.conversationshort}} Effectiveness](https://dataplatform.cloud.ibm.com/exchange/public/entry/view/133dfc4cd1480bbe4eaa78d3f636921c){: external}
- [Dialog Flow Analysis for {{site.data.keyword.conversationshort}}](https://dataplatform.cloud.ibm.com/exchange/public/entry/view/013c690997e27f3a8d9133265327a9e5){: external}

If you choose to use the notebooks that are designed for use with {{site.data.keyword.DSX}}, the steps are:

1.  Create a {{site.data.keyword.DSX}} account, [create a project](https://dataplatform.cloud.ibm.com/docs/content/wsj/getting-started/projects.html){: external}, and add a Cloud Object Storage account to it.

1.  From the {{site.data.keyword.DSX}} community, choose a notebook.

    Early in the development process, use the **Dialog skill analysis for {{site.data.keyword.conversationshort}}** notebook to help you get started. The notebook: 

    - Examines the terms that are correlated with each intent in your training data to find anomalies that might identify problems that you can investigate.
    - Uses a blind test set that you provide to calculate performance on statistical metrics like Accuracy, Precision, Recall, and F1.
    - Offers advanced features that you can use to find the causes of common issues, such as why some sentences are often misidentified.

    To learn more about how this notebook can help you improve your dialog, read [Dialog skill analysis](https://medium.com/ibm-watson/announcing-dialog-skill-analysis-for-watson-assistant-83cdfb968178){: external}.

1.  After you deploy a version of the assistant and collect conversation log data, run the **Measure {{site.data.keyword.conversationshort}} Performance** notebook.

1.  Follow the step-by-step instructions provided with the notebook to analyze a subset of the dialog exchanges from the logs.

    Run the following notebook first:

    - **Measure**: Gathers metrics that focus on coverage (how often the assistant is confident enough to respond to users) and effectiveness (when the assistant does respond, whether the responses are satisfying user needs).

    The insights are visualized in ways that make it easier to understand areas for improvement in your assistant.

1.  Export a sample set of the logs from ineffective conversations, and then analyze and annotate them.

    For example, indicate whether a response is correct. If correct, mark whether it is helpful. If a response is incorrect, then identify the root cause, the wrong intent or entity was detected, for example, or the wrong dialog node was triggered. After you identify the root cause, indicate what is the correct choice.

1.  Feed the annotated spreadsheet to the **Analyze {{site.data.keyword.conversationshort}} Effectiveness** notebook.

    - **Effectiveness**: Provides a deeper analysis of your logs to help you understand the steps that you can take to improve your assistant.
1.  Use the **Dialog Flow Analysis for {{site.data.keyword.conversationshort}}** notebook to review your dialog. The notebook can help you pinpoint the dialog nodes where customers most frequently abandon the conversation. 

    For more information about how this notebook can help you analyze and assess abandonment, see [Do you know where and why users drop off the conversation?](https://medium.com/ibm-data-ai/do-you-know-where-and-why-users-drop-off-the-conversation-6246e99baddc){: external}.

This process helps you to understand the steps you can take to improve your assistant.

### Using the notebooks with standard Python tools
{: #logs-resources-notebooks-python}

If you choose to use standard Python tools to run the notebooks, you can get the notebooks from GitHub.

- [Dialog Skill Analysis for {{site.data.keyword.conversationshort}}](https://github.com/watson-developer-cloud/assistant-skill-analysis){: external}
- [{{site.data.keyword.conversationfull}} Recommendation notebooks (Measure and Analyze Effectiveness)](https://github.com/watson-developer-cloud/assistant-improve-recommendations-notebook){: external}
- [{{site.data.keyword.conversationfull}} Dialog Flow Analysis notebook](https://github.com/watson-developer-cloud/assistant-dialog-flow-analysis){: external}

The [{{site.data.keyword.conversationshort}} Continuous Improvement Best Practices Guide](https://raw.githubusercontent.com/watson-developer-cloud/assistant-improve-recommendations-notebook/master/notebook/IBM%20Watson%20Assistant%20Continuous%20Improvement%20Best%20Practices.pdf){: external} outlines which notebook to use at each stage of your improvement process.

## Using the logs API
{: #logs-resources-api}

You can use the `/logs` API to list events from the transcripts of conversations that occurred between your users and your assistant. For conversations created with the v2 `/message` API, use the instance-level endpoint to [list log events in all workspaces](https://{DomainName}/assistant/assistant-v1#listalllogs){: external}, and then filter by Assistant ID. For more information, see [Filter query reference](/docs/watson-assistant?topic=watson-assistant-filter-reference).

The API logs messages that are exchanged in conversations that are defined by a dialog skill only.
{: important}

The number of days that logs are stored differs by service plan type. For more information, see [Log limits](/docs/watson-assistant?topic=watson-assistant-logs#logs-limits).

For a Python script you can run to export logs and convert them to CSV format, download the `export_logs_py.py` file from the [{{site.data.keyword.conversationshort}} GitHub repository)](https://github.com/watson-developer-cloud/community/blob/master/watson-assistant/export_logs_py.py){: external}.

## Understanding terminology
{: #logs-resources-terminology}

First, review the definitions of terms that are associated with {{site.data.keyword.assistant_classic_short}} logs.

| Term | Definition |
| --- | --- |
| Assistant |  An application - sometimes referred to as a 'chat bot' - that implements your {{site.data.keyword.assistant_classic_short}} content. |
| Assistant ID |  The unique identifier of an assistant. |
| Conversation |  A set of messages that an individual user sends to your assistant, and the messages your assistant sends back. |
| Conversation ID |  Unique identifier that is added to individual message calls to link related message exchanges together. App developers that use the V1 version of the {{site.data.keyword.assistant_classic_short}} API add this value to the message calls in a conversation by including the ID in the metadata of the context object. |
| Customer ID |  A unique ID that can be used to label customer data such that it can be deleted if the customer requests the removal of their data. |
| Deployment ID |  A unique label that app developers of the {{site.data.keyword.assistant_classic_short}} API V1 version pass with each user message to help identify the deployment environment that produced the message. |
| Instance |  Your deployment of {{site.data.keyword.assistant_classic_short}}, accessible with unique credentials. A {{site.data.keassistant_classic_shortnshort}} instance might contain multiple assistants. |
| Message |  A message is a single utterance that a user sends to the assistant. |
| Skill ID |  The unique identifier of a skill. |
| User |  A user is anyone who interacts with your assistant. |
| User ID |  A unique label that is used to track the level of service usage of a specific user. |
{: caption="Terminology" caption-side="bottom"}

The **User ID** property is not equivalent to the **Customer ID** property, though both can be passed with the message. The **User ID** field is used to track levels of usage for billing purposes. The **Customer ID** field is used to support the labeling and subsequent deletion of messages that are associated with users. Customer ID is used consistently across all Watson services and is specified in the `X-Watson-Metadata` header. User ID is used exclusively by the {{site.data.keyword.assistant_classic_short}} service and is passed in the context object of each `/message` API call.
{: important}

## Associating message data with a user for deletion
{: #logs-resources-customer_id}

There may be cases when you want to completely remove a set of your user's data from a {{site.data.keyword.assistant_classic_short}} instance. When the delete feature is used, the Overview metrics don't include those deleted messages, and results in fewer Total Conversations.

### Before you begin
{: #logs-resources-delete-customer-id-prereqs}

To delete messages for one or more individuals, you first need to associate a message with a unique **Customer ID** for each individual. To specify the **Customer ID** for any message that is sent with the `/message` API, include the `X-Watson-Metadata: customer_id` property in your header. You can pass multiple **Customer ID** entries with semicolon separated `field=value` pairs, by using `customer_id`, as in the following example:

```sh
curl -X POST -u "apikey:3Df... ...Y7Pc9" \
 --header \
   "Content-Type: application/json" \
   "X-Watson-Metadata: customer_id={first-customer-ID};customer_id={second-customer-ID}" \
 --data "{\"input\":{\"text\":\"hello\"}}" \
 "{url}/v2/assistants/{assistant_id}/sessions/{session_id}/message?version=2019-02-28"
```
{: pre}

where {url} is the appropriate URL for your instance. For more information, see [Endpoint URLs](/apidocs/assistant-v2#service-endpoint){: external}.

The `customer_id` string cannot include the semicolon (`;`) or equal sign (`=`) characters. You are responsible for ensuring that each `Customer ID` parameter is unique across your customers.
{: note}

For instructions on how to delete messages that use `customer_id` values, see the [Labeling and deleting data in {{site.data.keyword.conversationshort}}](/docs/watson-assistant?topic=watson-assistant-admin-securing#securing-gdpr-wa).
