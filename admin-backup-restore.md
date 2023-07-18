---

copyright:
  years: 2023
lastupdated: "2023-07-18"
keywords: export, import
subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Backing up and restoring data
{: #admin-backup-restore}

Back up and restore your {{site.data.keyword.conversationshort}} data by downloading, and then uploading the data. 
{: shortdesc}

You can download:
- Actions or dialog from the draft environment
- Published versions of actions or dialog
- Skills from the classic experience

You can upload:
- Actions or dialog to the draft environment
- Skills to the classic experience

## Downloading from the draft environment
{: #backup-restore-draft-environment}

To download your actions from the draft environment:

1. On the **Actions** page, click **Global settings** ![Gear icon](../../icons/settings.svg).

1. On the **Upload/Download** tab, click **Download**. The download includes your actions in a JSON file.

To download your dialog from the draft environment:

1. On the **Dialog** page, click **Upload/Download**.

1. On the **Download** tab, click **Download**. The download includes your dialog in a JSON file.

## Downloading a published version
{: #backup-restore-published}

You can download a published version from the **Publish** page or from **Assistant settings**.

To download from the Publish page:

1. On the **Publish** page, click the **Download** icon ![Download](../../icons/download.svg). for a recent version. The download includes your actions in a JSON file. If you are using dialog, the download also includes your dialog in a separate JSON file.

To download from Assistant settings:

1. Open **Assistant settings**.

1. In the **Download/Upload** section, click **Download/Upload files**. 

1. On the **Download** tab, select a published version, then click **Download**. You need at least one version for the download to be available. The .zip file includes your actions in an `action-skill.json` file. If you're using dialog, the .zip file also includes a `dialog-skill.json` file.

   You can also enable a *multilingual download* to download your training and responses in CSV files, which you can use with a translation service. For more information, see [Using multilingual downloads for translation](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-multilingual).
   {: note}

## Downloading a skill from the classic experience
{: #backup-restore-classic}

If you are using the classic experience, you can download a skill.

1.  On the **Skills** page, locate the skill that you want to download.

1.  Click the ![open and close list of options](../../icons/download.svg) icon, and then choose **Download**.

## Uploading to the draft environment
{: #backup-restore-import}

You can upload actions or dialog to the draft environment. The upload replaces any actions or dialog that you're currently working on, so make sure you back up your content or publish a version before you upload. 

If the {{site.data.keyword.conversationshort}} service changes between the time you export the actions and import it, due to functional updates that are regularly applied to instances in cloud-hosted continuous delivery environments, your imported actions might function differently than before. The imported JSON file must use UTF-8 encoding, without byte order mark (BOM) encoding. The JSON file cannot contain tabs, newlines, or carriage returns.
{: important}

To upload your actions to the draft environment:

1. On the **Actions** page, click **Global settings** ![Gear icon](../../icons/settings.svg).

1. On the **Upload/Download** tab, drag a JSON file onto the tab or click to select a file from your local system, then click **Upload**.

To upload your dialog to the draft environment:

1. On the **Dialog** page, click **Upload/Download**.

1. On the **Upload** tab, drag a JSON file onto the tab or click to select a file from your local system, then click **Upload**.

As an alternative, you can use **Assistant settings** to upload to the draft environment:

1. Compress your JSON file into a .zip file. You can include an actions JSON file and a dialog JSON file in the same .zip file if you want.

1. Open **Assistant settings**.

1. In the **Download/Upload** section, click **Download/Upload files**.

1. On the **Upload** tab, choose **Assistant only**.

1. Attach your .zip file package, then click **Upload**. 

## Uploading a skill to the classic experience
{: #backup-import-skill}

In the classic experience, to reinstate a backup copy of a dialog skill that you exported from another service instance or environment, create a new skill by importing the JSON file of the skill you exported.

If the {{site.data.keyword.conversationshort}} service changes between the time you export the skill and import it, due to functional updates that are regularly applied to instances in cloud-hosted continuous delivery environments, your imported skill might function differently than it did before.
{: important}

1.  On the **Skills** page, click **Create skill**.

1.  Choose to create a dialog skill, then click **Next**.

1. Click the **Upload skill** tab.

1.  Select the JSON file you want to import, then click **Upload**.

    The imported JSON file must use UTF-8 encoding, without byte order mark (BOM) encoding. The JSON file cannot contain tabs, newlines, or carriage returns.
    {: important}

    The maximum size for a skill JSON file is 10MB. If you need to import a larger skill, consider using the REST API. For more information, see the [API Reference](https://cloud.ibm.com/apidocs/assistant/assistant-v1#createworkspace){: external}.
    {: tip}

1.  Specify the details for the skill:

    - **Name**: A name no more than 100 characters in length. A name is required.
    - **Description**: An optional description no more than 200 characters in length.
    - **Language**: The language of the user input the skill will be trained to understand. The default value is English.

After you create the skill, it appears as a tile on the Skills page.

## Retaining logs
{: #backup-retain-logs}

If you want to store logs of conversations, you can use the `/logs` API to export your log data. See [API reference](https://cloud.ibm.com/apidocs/assistant/assistant-v1#listlogs){: external} for details.

Your service plan determines how long logs are available.

| Service plan | Chat message retention |
| --- | --- |
| Enterprise with Data Isolation | Last 90 days |
| Enterprise | Last 30 days |
| Premium (legacy) | Last 90 days |
| Plus | Last 30 days |
| Trial | Last 30 days |
| Lite | Last 7 days |
{: caption="Log retention by plan" caption-side="top"}
