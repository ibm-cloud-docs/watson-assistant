---

copyright:
  years: 2018, 2022
lastupdated: "2022-01-20"

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

# Creating an assistant
{: #assistant-add}

The first step in building your chatbot is creating a new assistant.
{: shortdesc}

When you add an instance of {{site.data.keyword.conversationshort}}, you create an assistant before doing anything else. If you want to add more assistants, follow these steps:

1.  In the top navigation, click the name of your current assistant, then choose **Create New**:

    ![Create new](images/assistant-add-create-new.png).

1.  Add details about the new assistant:

    - **Assistant name**: A name no more than 100 characters in length. A name is required.
    - **Description**: An optional description no more than 200 characters in length.
    - **Assistant language**: The language the assistant uses in conversations. Learn more about [language support](/docs/watson-assistant?topic=watson-assistant-admin-language-support).

1.  Click **Create assistant**.

The number of assistants you can create depends on your {{site.data.keyword.conversationshort}} [plan type](https://www.ibm.com/products/watson-assistant/pricing/){: external}. There is also a limit of 100 assistants per service instance.

Once you have created an assistant, you can start with the next topic in [Building your assistant](/docs/watson-assistant?topic=watson-assistant-build-actions-overview).

## Renaming an assistant
{: #assistant-add-rename}

You can change the name and description of an assistant after you create it. You can't change its language.

To rename an assistant, follow these steps:

1.  Open **Assistant settings**.

1.  Enter a new name or description.

1.  Click **Save**.

## Deleting an assistant
{: #assistant-add-delete}

To delete an assistant, follow these steps:

1.  Open **Assistant settings**.

1. Click the **Delete assistant** button on the settings page. A confirmation question displays.

1. To confirm, type the word `DELETE`, then click **Delete**.
