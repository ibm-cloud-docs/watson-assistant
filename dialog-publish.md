---

copyright:
  years: 2018, 2022
lastupdated: "2022-03-09"

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

# Publishing dialog and actions
{: #dialog-publish}

If the dialog feature is enabled, the publishing and deployment processes remain the same. However, some slight differences in functionality exist.
{: shortdesc}

To learn about the overall publishing and deployment model for {{site.data.keyword.conversationshort}}, see the [Publishing and deploying your assistant overview](/docs/watson-assistant?topic=watson-assistant-publish-overview). For more information about the **Publish** page and how the publishing process works, see [Publishing your content](/docs/watson-assistant?topic=watson-assistant-publish). The following slight differences exist when the dialog feature is enabled in an assistant:

- On the **Publish** page, the information in the **Content type** column lists whether your content changes contain a dialog.
- The version tiles on the **Publish** and **Environment** pages show whether the published content contains actions, or actions and a dialog. For example, if the dialog feature is enabled in your assistant, the version tile displays `Contains actions & dialog`.
- When you export a version of your content from the **Publish** page, two JSON files are downloaded. One file is for actions and one file is for the dialog.
