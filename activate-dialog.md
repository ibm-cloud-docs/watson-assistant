---

copyright:
  years: 2018, 2023
lastupdated: "2023-10-24"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Activating dialog and migrating skills
{: #activate-dialog}

To use an existing dialog skill, you need to activate the dialog feature in your assistant. Then you can upload your existing skill.

## Activating dialog
{: #activate-dialog-activating}

To activate the dialog feature:

1.  Create or open an assistant where you want to use a dialog as the primary conversation with users.

1.  Open **Assistant settings** ![Gear icon](../../icons/settings.svg).

1.  Click **Activate dialog**.

    ![Activate dialog](images/activate-dialog.png){: caption="Activate dialog" caption-side="bottom"}

1.  In the confirmation that displays, click **Activate dialog** again.

    ![Activate dialog](images/activate-dialog-modal.png){: caption="Activate dialog" caption-side="bottom"}

Once you activate the dialog feature, it takes precedence over actions. You can use actions to supplement a dialog-based conversation, but the dialog drives the conversation with users to match their requests. For more information, see [Calling actions from a dialog](/docs/watson-assistant?topic=watson-assistant-dialog-call-action).

## Migrating existing skills
{: #activate-dialog-upload}

Once the dialog feature is activated, you can start a new dialog conversation from scratch if you want. But, you probably have an existing dialog skill that you want to migrate into {{site.data.keyword.conversationshort}}.

To migrate an existing dialog skill:

1.  Use the classic experience to [download your dialog skill](/docs/watson-assistant?topic=watson-assistant-admin-backup-restore#backup-restore-classic) in JSON format. 

1.  In {{site.data.keyword.conversationshort}}, open the **Dialog** page.

1.  In **Options**, choose **Upload / Download**.

    ![Upload dialog](images/dialog-upload.png){: caption="Upload dialog" caption-side="bottom"}

1.  On the **Upload** tab, upload the JSON file for your dialog skill.
