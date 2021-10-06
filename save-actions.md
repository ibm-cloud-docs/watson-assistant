---

copyright:
  years: 2021
lastupdated: "2021-10-06"

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

# Saving your actions
{: #save-actions}

When working on actions, your assistant automatically saves changes when you do one of the following:

- Click on a new step
- Open Preview
- Reset Preview

You can also save changes by clicking the **Save** icon, for example, in these places when working on actions:

- Within each action
- Actions settings
- Renaming an action
- Editing a variable

When the system automatically saves or you click the **Save** icon, the following items are saved to all:
- Actions you have created
- Edits you made to a system action
- Variables you created
- Action settings

If you want to disable auto-save, you can toggle it off:

1. Open the **Actions** page.

1. Click the **Global settings** icon ![Gear icon](images/gear-icon-blue.png).

1. In the Global Settings window, click the **Auto-save** tab.

1. Toggle the switch to **Off**.

![Auto-save](/images/save-work-auto-save.png)

### Avoiding conflicts
{: #save-actions-conflicts}

To avoid conflicts when saving, we recommend dividing work so that one person works on one action at a time.

Also, {{site.data.keyword.conversationshort}} prevents two users from working in an action with unsaved edits. If one user saves changes before a second user, this `Unable to save action` message may appear:

![Unable to save action](images/manage-team-unable-to-save.png)

<!--## Hide in-progress work before publishing
{: #manage-team-hide-work}-->

<!--## Moving a group of actions from one assistant to another
{: #manage-team-moving-actions}

This will be via JSON import/export on the settings page.-->

