---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-25"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}



# Migrating intents and entities
{: #migrate-intents-entities}

This feature is currently not available in the AI assistant builder of IBM watsonx Orchestrate.{: note}

You can migrate your intents and entities from the classic experience to {{site.data.keyword.conversationshort}}.
{: shortdesc }

## Downloading intents
{: #migrate-intents-download}

You can download intents to a CSV file, so you can then upload and reuse them as actions or example phrases in {{site.data.keyword.conversationshort}}.

1. Go to the **Intents** page.

1. Select the intents that you want to download, and then click the **Download** icon ![Download icon](images/download-icon.png).

    If you plan to use a downloaded intent file to upload example phrases for a specific action, download only a single intent. In {{site.data.keyword.conversationshort}}, only one intent can be uploaded per action.
    {: important}

1. Specify the name and location in which to store the CSV file that is generated, and click **Save**.

You can now perform the following tasks to migrate information to {{site.data.keyword.conversationshort}}:
- Upload intents as actions. For more information, see [Uploading intents as actions](/docs/watson-assistant?topic=watson-assistant-upload-download-actions#upload-download-actions-upload-intents).
- Upload the examples from a single intent as example phrases for a specific action. For more information, see [Uploading phrases](/docs/watson-assistant?topic=watson-assistant-understand-questions#understand-questions-uploading-examples).

## Downloading entities
{: #migrate-entities-download}

You can download a number of entities to a CSV file, so you can then upload and reuse them as saved customer responses in {{site.data.keyword.conversationshort}}.

1. Go to the **Entities** page.

1. Select the entities that you want to download, and then click the **Download** icon ![Download icon](images/download-icon.png).

1. Specify the name and location in which to store the CSV file that is generated, and click **Save**.

You can now upload the entities as saved customer responses in {{site.data.keyword.conversationshort}}. For more information, see [Uploading saved customer responses](/docs/watson-assistant?topic=watson-assistant-collect-info#uploading-saved-customer-response).
