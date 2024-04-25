---

copyright:
  years: 2018, 2024
lastupdated: "2024-04-25"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}



# Publishing dialog and actions
{: #dialog-publish}

This feature is currently not available in the AI assistant builder of IBM watsonx Orchestrate.{: note}

If the dialog feature is enabled, the publishing and deployment processes remain the same. However, some slight differences in functionality exist.
{: shortdesc}

To learn about the overall publishing and deployment model for {{site.data.keyword.conversationshort}}, see the [Publishing and deploying your assistant overview](/docs/watson-assistant?topic=watson-assistant-publish-overview). For more information about the **Publish** page and how the publishing process works, see [Publishing your content](/docs/watson-assistant?topic=watson-assistant-publish). The following slight differences exist when the dialog feature is enabled in an assistant:

- On the **Publish** page, the information in the **Content type** column lists whether your content changes contain a dialog.
- The version tiles on the **Publish** and **Environments** pages show whether the published content contains actions, or actions and a dialog. For example, if the dialog feature is enabled in your assistant, the version tile displays `Contains actions & dialog`.
- When you export a version of your content from the **Publish** page, two JSON files are downloaded. One file is for actions and one file is for the dialog.
