---

copyright:
  years: 2021, 2022
lastupdated: "2022-02-03"

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

# Overview
{: #publish-overview}

After you have built an assistant, you can test to make sure it works as you intended before you make it available to customers. The {{site.data.keyword.conversationshort}} workflow makes it straightforward to preview your assistant in a closed environment and manage exactly what you make available to customers.
{: shortdesc}

An assistant consists of three core elements:

- **Content**: The conversation logic and words that are used to respond to your customer. Content is required for every assistant.
- **Channels**: The location where your assistant interacts with your users, such as the web chat interface on your website. At least one channel is required for every assistant.
- **Extensions**: Add-ons to the end experience that help solve specific user problems, for example, searching existing help content.

In general, you follow this high-level process throughout the life of your assistant:

1. Build your initial content into an assistant.
1. Review content and gain approval from team members.
1. Publish the approved content so it can be made available to customers.
1. Deploy your assistant on your website (or using another channel).
1. Iteratively improve your assistant and republish the content as needed.

## Environments
{: #environments}

You can group your work in separate containers that are called _environments_. You can think of an environment as a space within the product that contains a version of your work. Each environment can contain its own content, channels, and extensions. As you build and evolve your assistant, you can take snapshots of these items and move them from one environment to another. Environments also have their own IDs, URLs, and service credentials that can be referenced by external services.

Each new assistant comes with two environments: the draft environment and the live environment. The draft environment can be managed from the **Draft environment** page, and the live environment can be managed from the **Live environment** page. Your users interact with assistants on the live environment and cannot interact with assistants on the draft environment. The separation of these two environments allows you to ensure that any in-progress updates to the assistant do not get published. You do not want users to stumble upon an incomplete action that leads them to a dead end.

## The draft environment

Use the **Draft environment** page to manage the draft environment. Your draft content is permanently connected to the draft environment, and you can preview this content from your customers' perspective on the **Preview** page. From the **Preview** page, you can also manage your draft web chat channel. All other draft environment integrations are managed from the **Draft environment** page. Use your draft integrations for testing, not for going live. These integrations are unique to the draft environment, and changes to draft integrations don't affect live integrations.

![Image of the Draft environment page](images/draft-environment-page.png)

The **Assistant preview** pane on the **Preview** page shows what the web chat channel looks like on a sample webpage. This preview pane shows draft content, draft integrations, and any changes to the web chat settings. To share a preview of your draft content, copy and paste the share link on the left side of the **Preview** page.

For more information about previewing your assistant in the draft environment, see [Previewing and sharing your assistant](/docs/watson-assistant?topic=watson-assistant-preview-share).

## Publishing

When your content is ready to be exposed to your customers, you can publish from the **Publish** page. When you publish, you use the **Publish** page to move saved content from the draft environment to the live environment. Each time you publish, you create a new version name, such as V1 or V2.

![Image of the Publish page](images/publish-page.png)

When you publish your content, Watson Assistant creates a snapshot of the draft content and connects that snapshot to the live environment. This snapshot contains all of the content from actions, including settings and variables. Snapshots do not contain integration configurations or environment settings. Integration configurations and environment settings must be configured manually in each environment.

You can make edits to your live environment either by editing your draft environment and publishing or by switching the version of your content on your live environment to another version. By default, the most recently published version of your content is connected to the live environment. The number of versions that can be maintained before they are deleted depends on the type of plan you have. If you reach the plan limit of versions you can have, the oldest version that isn't live is deleted when a new version is published.

## The live environment
Use the **Live environment** page to manage the live environment. This page indicates which content is live in the assistant and which channels that content is connected to. The left side of the page displays the channels where content is deployed, or where customers can interact with the assistant. The right side of the page displays the resolution methods, or how the assistant responds to customer questions or requests.

![Image of the Live environment page](images/live-environment-page.png)

The version of content displayed under **Published content** is the version that is connected to the live environment. You can change this version from the **Publish** page, or by clicking **Edit content** from the **Live environment** page and selecting a different version.

For more information about publishing, see [Publishing your content](/docs/watson-assistant?topic=watson-assistant-publish).
