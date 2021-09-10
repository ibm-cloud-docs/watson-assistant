---

copyright:
  years: 2021
lastupdated: "2021-09-02"

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

# Publishing your content
{: #publish}

It's important to understand how publishing works to ensure proper lifecycle management process for your assistant. For customers to interact with your most up-to-date content, you must do two foundational things:

- Deploy a live channel
- Publish content to the live environment

## How to publish
1. Go to the **Publish** page.

1. From the **Publish** page, you see a table that contains all changes to actions that occurred since you last published. If changes are available to publish, click **Publish**. Enter an optional description of the version and click **Confirm**:

  ![Image of the Publish button](images/unpublished-content.png)

1. After you publish, no changes are available to publish because the live environment is up to date.

  ![Image of the no new changes to publish screen](images/no-new-changes-publish.png)

## What is being published?
When you publish content, a snapshot is taken of the current state of actions. The number of versions that can be maintained before they are deleted depends on the type of plan you have. If you reach the plan limit of versions you can have, the oldest version that isn't live is deleted when a new version is published.

All updates to actions content are published in a version, including the following updates:

- Creating an action
- Editing an action
- Editing actions settings
- Deleting actions
- Creating variables
- Editing variables
- Deleting variables

The following updates are not published in a version and must be configured manually for each environment:

- Channel configurations
- Environment settings

## Why publish?
Publishing is a way to maintain a healthy lifecycle management process. Publishing allows users to build and test in a separate environment than where the live content resides.
<!--- For more information, see [Manage your future iterations and launches](link). --->

## Changing the live version
{: #changing-live-version}
1. To change the live version, go to the **Publish** page and select a non-live version from the **Version history** panel.
1. Click **Revert**. Clicking **Revert** points the live environment to the version of content that you selected in the previous step.

  ![Image of the no new changes to publish screen with a version selected from Version history](images/unpublished-content-version-history.png)

1. From the **Replace live version** window, confirm that the requested changes look correct. If they do, click **Revert**.

  ![Image of the Replace live version dialog](images/replace-live-version-snippet.png)

## Managing the live environment
The **Connect** page shows the live environment and the content and channels that are attached to it.

From the **Connect** page, you can manage live channel configurations by clicking them. You can also change the content version that is connected to the live environment by clicking the version and following the instructions that are outlined in [Changing the live version](#changing-live-version).

Update environment-specific settings by clicking the gear icon next to **live** in the upper left. From this menu, API details, web hooks, and inactivity timeout can be accessed and managed.

![Image of the live environment channels](images/live-environment-channels.png)
