---

copyright:
  years: 2019, 2023
lastupdated: "2023-09-21"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Managing workflow with versions
{: #versions}

[Plus]{: tag-green}[Enterprise]{: tag-purple}

In the classic experience only, skill versions help you manage the workflow of a dialog skill development project. In the new experience, dialog can be included in your published versions of your content. For more information, see [Publishing your content](/docs/watson-assistant?topic=watson-assistant-publish).
{: Important}

Create a skill version to capture a snapshot of the training data (intents and entities) and dialog in the skill at key points during the development process. Being able to save an in-progress skill at a specific point in time is especially useful as you start to fine-tune your assistant. You often need to make a change and see the impact before you can determine whether the change improves or lessens the effectiveness of the assistant. Based on your findings from a test environment deployment, you can make an informed decision about whether to deploy a change to an assistant that is deployed in a production environment.

## Creating a version
{: #versions-create}

You can edit only one version of the dialog skill at a time. The in-progress version is called the *development* version.

When you save a version, any skill settings that you applied to the development version are saved also.

To create a dialog skill version, follow these steps:

1.  From the header of the skill, click **Save new version**, and then describe the current state of the skill.

    Adding a good description helps you to distinguish multiple versions from one another later.

    Add the date that you deploy the version to its description to make it easier to filter logs by version from the Analytics page later. For more information, see [Picking a data source](/docs/watson-assistant?topic=watson-assistant-logs#logs-pick-data-source).
    {: tip}

1.  Click **Save**.

A snapshot is taken of the current skill and saved as a new version. You remain in the development version of the skill. Any changes that you make continue to be applied to the development version, not the version you saved. To access the version you saved, go to the **Versions** page.

If you have trouble, check that your skill does not have any entities with large numbers of values (such as 10,000 or more synonyms for a single entity). If it does, try to break the entity into many, more categorized entities, or consider using a contextual entity instead.

## Deploying a skill version
{: #versions-deploy}

1.  Click **Versions**.

1.  Click the ![Click to view actions](images/overflow-menu--vertical.svg) icon from the version that you want to deploy, and then choose **Assign**.

    A list of assistants to which you can link this version is displayed. The list is limited to those assistants without any skills, or that are associated with a different version of this skill.

1.  Click the checkbox for one or more of the assistants, and then click **Assign**.

Track when this version is deployed to an assistant and for how long. It is likely that you want to analyze user conversations that occur between users and this specific version of the skill. You can get this information from the **Analytics** page. However, when you pick a data source, versions are not listed. You must choose the name of the assistant to which you deployed this version. You can then filter the metrics data to show only those conversations that occurred between the start and end dates during which this skill version was deployed to the assistant.
{: important}

## Skill version limits
{: #versions-limits}

The number of versions you can create for a single skill depends on your plan.

| Plan | Versions per skill |
| --- | --- |
| Enterprise | 50 |
| Premium (legacy) | 50 |
| Plus | 10 |
| Trial | 10 |
| Lite |  0 |
{: caption="Service plan details" caption-side="bottom"}

## Swapping skills
{: #versions-swap-skills}

If the earlier version did a better job of recognizing and addressing customer needs than a later version, you can swap the skill to use the earlier version.

Follow the same steps that you use to [deploy a skill version](#versions-deploy) to change the version that is linked to an assistant.

## Accessing a saved version
{: #versions-view}

The only way to view a saved version is to overwrite the in-progress development version of the skill with the saved version. (But not before you save any work that you did in the current development version.)

You cannot edit a saved version. To achieve the same goal, you can use a saved version as the basis for a new version in which you incorporate any changes you want to make. To start development work from a saved version, overwrite the in-progress development version of the skill with the saved version.

1.  Save any changes that you made to the skill since the last time you created a version.

    Save a version of the skill now. Otherwise, your work is lost when you follow these steps.
    {: important}

1.  From the version you want to edit, click the **Click to view actions** ![Click to view actions](images/overflow-menu--vertical.svg) icon, and then choose **Revert** and confirm the action.

    The page refreshes to revert to the state that the skill was in when the version was created.

If you want to save any changes that you make to this version, you must save the skill as a new version. You cannot apply changes to an already-saved version.

When you open a skill by clicking the skill tile from the assistant page, the development version of the skill is displayed. Even if you associated a later version with the assistant, when you access the skill, its development version opens.
{: important}

## Downloading a skill version
{: #versions-export}

You can download a dialog skill version in JSON format. You might want to download a skill version if you want to use a specific version of a dialog skill in a different instance. You can download the version from one instance and import it to another instance as a new dialog skill.

To download a dialog skill version, complete the following steps:

1.  From the skill menu, click **Versions**.
1.  Click the **Click to view actions** ![Click to view actions](images/overflow-menu--vertical.svg) icon from the version that you want to download, and then choose **Download**.
1.  Specify a name for the JSON file and where to save it, and then click **Save**.

