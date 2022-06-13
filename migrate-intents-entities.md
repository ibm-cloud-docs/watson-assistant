---

copyright:
  years: 2022
lastupdated: "2022-05-12"

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

# Migrating intents and entities
{: #migrate-intents-entities}

You can migrate your intents and entities from the classic {{site.data.keyword.conversationshort}} experience to the new {{site.data.keyword.conversationshort}} experience. In the new experience, intents are known as *example phrases* in an action, and entities are known as *saved customer responses*.
{: shortdesc }

## Downloading intents
{: #migrate-intents-download}

You can download an intent to a CSV file, so you can then upload and reuse the examples as example phrases in the new {{site.data.keyword.conversationshort}} experience.

1. Go to the **Intents** page.

1. Select the intent that you want to download, and then click the **Download** icon ![Download icon](images/download-icon.png).

    Only one intent can be uploaded per action in the new experience, so download only the examples for a single intent at a time.
    {: important}

1. Specify the name and location in which to store the CSV file that is generated, and then click **Save**.

1. Upload the examples from the intent as example phrases for a specific action in the new {{site.data.keyword.conversationshort}}. For more information, see [Uploading phrases](/docs/watson-assistant?topic=watson-assistant-understand-questions#understand-questions-uploading-examples).

## Downloading entities
{: #migrate-entities-download}

You can download a number of entities to a CSV file, so you can then upload and reuse them as saved customer responses in the new {{site.data.keyword.conversationshort}} experience.

1. Go to the **Entities** page.

1. Select the entities that you want to download, and then click the **Download** icon ![Download icon](images/download-icon.png).

1. Specify the name and location in which to store the CSV file that is generated, and then click **Save**.

1. Upload the entities as saved customer responses in the new {{site.data.keyword.conversationshort}}. For more information, see [Uploading saved customer responses](/docs/watson-assistant?topic=watson-assistant-collect-info#uploading-saved-customer-response).
