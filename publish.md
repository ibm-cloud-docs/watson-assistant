---

copyright:
  years: 2021, 2025
lastupdated: "2025-04-04"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Publishing your content
{: #publish}

Publishing is a way to maintain a healthy lifecycle management process. You can create incremental versions of your content over time, making it easier to manage deployment of changes and roll back (revert) to prior versions if necessary.
{: shortdesc}

When you are ready to create a snapshot of your content and settings, you can publish from the **Publish** page. Each time that you publish, you create a new version, such as V1 or V2.

![Publish page](images/publish-page.png){: caption="Publish page screen." caption-side="bottom"}

When you publish your content, {{site.data.keyword.conversationshort}} creates a snapshot of the draft content, resulting in a version. This version contains all of the content from actions, including settings and variables. Versions do not contain integration configurations or environment settings. Integration configurations and environment settings must be configured manually in each environment.

The three most recent published versions appear in a list on the **Publish** page itself. If you have more than three versions, you can click **View all** to see a list of all published versions.

![All versions](images/published-versions.png){: caption="All versions" caption-side="bottom"}

The number of versions that can be maintained depends on the type of plan you have. If you reach the plan limit of versions you can have, you need to delete a version before you can publish another one. 

| Service plan | Published versions |
|---|---:|
| Enterprise | 50 |
| Premium (legacy) | 50 |
| Plus | 10 |
| Trial | 10 |
| Lite | 2 | 2 |
{: caption="Service plan published versions" caption-side="top"}

## How to publish
{: #publish-how}

1. If changes are available to publish, click **Publish**. 

1. Enter a description of the version.

1. Choose to publish to the live environment, or to create a version without publishing. If you choose to create a version, you can use the environment tab to publish that version later. 

   With the Enterprise plan, you can publish to an environment you added. For more information, see [Adding and using multiple environments](/docs/watson-assistant?topic=watson-assistant-multiple-environments).

1. Click **Publish**:

    ![Publish all content](images/publish-modal.png){: caption="Publish all content" caption-side="bottom"}

1. After you publish, the list is clear until you make more edits to your content.

   ![No changes](images/no-new-changes-publish.png){: caption="No changes" caption-side="bottom"}

## What is being published?
{: #publish-what}

When you publish, a snapshot is taken of the current state of actions. All updates to actions content are published in a version, including the following updates:

- Creating an action
- Editing an action
- Editing actions settings
- Deleting actions
- Creating variables
- Editing variables
- Deleting variables

If you are using [dialog with actions](/docs/watson-assistant?topic=watson-assistant-migrate-overview), these updates are published:
- Activating dialog
- Creating a dialog
- Editing a dialog
- Editing dialog settings
- Deleting a dialog

The following updates are not published in a version and must be configured manually for each environment:

- Channel configurations
- Environment settings

## Publishing or switching versions in the live environment
{: #publish-switch}

There are two ways to publish a version to the live environment:

- When you publish a version from the draft environment
- Use the **Live environment** tab and click **Publish version**.

After a version is published to the live environment, there are two ways you can switch to a different version:

- When you publish a version from the draft environment, you have the option of assigning it to the live environment, replacing the one that's already there
- Use the **Live environment** tab and click **Switch version**.

## Reverting to a previous version
{: #publish-revert}

Use the revert function if you need to update a version of content that is already published to a version. For example, if you publish V1 of your content and then notice an error, you can revert your actions to V1 and use the draft environment to correct the error. 

If you revert to a previous version, your published content isn't affected, but the content on the **Actions** page is overwritten with the version that you revert to. For example, if you decide to revert to V1 of your content, all content on the **Actions** page is overwritten with the V1 content so you can continue to work on it. 

To revert to a previous version:

1. On the **Publish** page, click **Revert**.

1. On the **Publish content** tab, choose whether you want to save your in-progress actions as a content version so that you don't lose your current work. For example, if you are reverting to V1 and you choose to create a version, V2 is created so you can resume work on it later.

   To create a version, check **Publish content** and add a description.

   ![Publish content](images/revert-publish.png){: caption="Publish content" caption-side="bottom"}

1. Next, select the version of content that you want to revert to, then click **Publish & Revert**. 

   ![Revert to a prior version](images/revert-version.png){: caption="Revert to a prior version" caption-side="bottom"}

1. After you revert, you can go to the **Actions** page to make any fixes or updates. When you're ready to publish, go to the **Publish** page and publish your updated content as a new version (for example, V3).
