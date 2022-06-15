---

copyright:
  years: 2021
lastupdated: "2022-06-15"
keywords: export, import
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
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

{{site.data.content.classiclink}}

# Backing up and restoring data
{: #admin-backup-restore}

Back up and restore your {{site.data.keyword.conversationshort}} data by downloading, and then uploading the data. 
{: shortdesc}

You can download the following data from a {{site.data.keyword.conversationshort}} service instance:

- Actions

You cannot download the following data:

- Search
- Assistant, including any configured integrations

## Retaining logs
{: #backup-retain-logs}

If you want to store logs of conversations that users have had with your assistant, you can use the `/logs` API to export your log data. See [API reference](https://cloud.ibm.com/apidocs/assistant/assistant-v1#listlogs){: external} for details.

Logs are stored for a different amount of time depending on your service plan. For example, Lite plans provide logs from the past 7 days only. See [Log limits](/docs/assistant?topic=assistant-logs#logs-limits){: external} for more information.

## Downloading
{: #backup-restore-export}

To back up actions, download a JSON file and store it.

1.  On the **Actions** page, click **Global settings** ![Gear icon](images/gear-icon-black.png).

1.  On the **Upload/Download** tab, click the **Download** button.

## Uploading
{: #backup-restore-import}

To reinstate a backup copy of actions that you exported from another service instance or environment, import the JSON file of the actions you exported.

If the {{site.data.keyword.conversationshort}} service changes between the time you export the actions and import it, due to functional updates that are regularly applied to instances in cloud-hosted continuous delivery environments, your imported actions might function differently than before.
{: important}

1.  On the **Actions** page, click **Global settings** ![Gear icon](images/gear-icon-black.png).

1.  On the **Upload/Download** tab, drag and drop a JSON file onto the tab or click to select a file from your local system, then click **Upload**.

    The imported JSON file must use UTF-8 encoding, without byte order mark (BOM) encoding. The JSON file cannot contain tabs, newlines, or carriage returns.
    {: important}

    The maximum size for a skill JSON file is 10MB. If you need to import a larger skill, consider using the REST API. For more information, see the [API Reference](https://cloud.ibm.com/apidocs/assistant/assistant-v1#createworkspace){: external}.
    {: tip}

