---

copyright:
  years: 2021, 2023
lastupdated: "2023-10-25"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Adding and using multiple environments
{: #multiple-environments}

[Enterprise]{: tag-purple}

Each assistant has a draft and live environment. For Enterprise plans, you can add up to three environments as a staging area to test your assistant before deployment. You can build content in the draft environment and test versions of your content in the extra environments.
{: shortdesc}

For more information about environments, see [Environments](/docs/watson-assistant?topic=watson-assistant-publish-overview#environments).

## Adding environments
{: #multiple-environments-add}

Each new environment appears as an extra tab on your **Environments** page. You can't reorder these environments, so add them to match your test-to-deploy lifecycle.

To add an environment:

1. Open the **Environments** page and click **Add Environment**.

   ![Add environment](images/multiple-env-add-button.png){: caption="Add environment" caption-side="bottom"}

1. Enter a name and a description, then click **Save**. Names can't contain spaces or use any special characters.

   ![Add an environment](images/multiple-env-add-modal.png){: caption="Add an environment" caption-side="bottom"}

The new environment appears as an extra tab on your **Environments** page.

![Environment tab](images/multiple-env-tab.png){: caption="Environment tab" caption-side="bottom"}

## Using your environments
{: #multiple-environments-using}

You can use extra environments in your development and test process before you deploy an assistant for customer use.

Add extra environments to match your existing test-to-deploy process. For example, you might name and use five environments in a scenario like this:

| Environment | Used for |
| --- | --- |
| Draft | Conversation authors build actions and test as they work |
| Review | Conduct an initial content review with stakeholders |
| Test | Test assistant content on a configured channel |
| Staging | Use a staging website to test assistant content and channel configurations |
| Live | Deploy for customer use |
{: caption="Example" caption-side="top"}

### Access control to environments
{: #multiple-environments-access}

You can control who can work in each environment. Each environment has an ID that you can use in IBM Cloud Identity and Access Management (IAM) and set access by resource. For more information on access control, see [Managing access with Identity and Access Management](/docs/watson-assistant?topic=watson-assistant-access-control#access-control-iam). For more information on settings, see [Environment settings](#multiple-environments-settings).

## Publishing content to an environment
{: #multiple-environments-publish}

For more information, see [Publishing your content](/docs/watson-assistant?topic=watson-assistant-publish).

To publish new changes from the draft environment to an environment:

1. If changes are available to publish, click **Publish**. 

1. Enter a description of the version.

1. Choose an environment.

1. Click **Publish**.

To publish an existing version to an environment:

1. On the **Environments** page, click the environment tab.

1. In Resolution Methods, click **Switch version**.

1. Choose a version to publish, then click **Switch version**.

### Moving a version through multiple environments
{: #multiple-environments-move}

This example explains moving a content version through multiple environments to build, test, iterate, and deploy. 

| Environment | Activity |
| --- | --- |
| Draft | Publish version V3 to Review environment |
| Review | Conduct initial testing of V3 |
| Test | Switch to version V3 for further testing with a configured channel |
| Staging | Switch to version V3 for testing with an internal staging website |
| Live | Switch to version V3 for customer use |
| Live | Switch to version V2 after a bug is found in version V3 |
| Draft | Revert to version V3 to fix the bug. For more information, see [Reverting to a previous version](/docs/watson-assistant?topic=watson-assistant-publish#publish-revert) |
| Draft | Publish version V4 to Review environment for retesting |
| Test | Switch to version V4 for further retesting |
| Staging | Switch to version V4 for testing with an internal staging website |
| Live | Switch to version V4 for customer use |
{: caption="Example" caption-side="bottom"}

## Previewing an environment
{: #multiple-environments-preview}

On each environment tab, you can click **Preview this environment** to open another browser tab and preview your assistant as an interactive web chat widget. 

![Preview](images/multiple-env-preview.png){: caption="Preview" caption-side="bottom"}

You can share this unauthenticated version of your assistant with your team by sending them the link to the environment preview. Your subject-matter experts can test your in-progress assistant without needing access to {{site.data.keyword.conversationshort}} itself.

## Environment settings
{: #multiple-environments-settings}

Each environment has its own settings. Click the **Settings** gear icon ![Gear icon](../../icons/settings.svg) to open the settings. 

| Setting | Description |
| --- | --- |
| API Details | Environment name and ID, session URL, and a link to the IBM Cloud console to see the service credentials for your instance |
| Webhooks | Settings for pre-message, post-message, and log webhooks. For more information, see [Extending your assistant with webhooks](/docs/watson-assistant?topic=watson-assistant-webhook-overview). |
| Inactivity timeout | Specify the amount of time to wait after the customer stops interacting with the assistant before the session ends. The maximum inactivity timeout differs by service instance plan type. For more information, see [Inactivity timeout](/docs/watson-assistant?topic=watson-assistant-publish-overview#publish-overview-environment-settings-inactivity). |
| Session history | For each environment, you can record the recent messages from the conversation for each customer, for use with the [`session_history` variable](/docs/watson-assistant?topic=watson-assistant-manage-info#built-in-variables). For more information, see [Session history](/docs/watson-assistant?topic=watson-assistant-publish-overview#publish-overview-environment-settings-session-history). |
| Edit environment | Change the name or description of the environment. Names can't contain spaces or use any special characters. |
| Delete environment | If necessary, you can remove the environment. Any channel or extension configurations are removed. Deleting an environment doesn't delete any published content versions. They remain in your list of published versions. |
{: caption="Example" caption-side="bottom"}
