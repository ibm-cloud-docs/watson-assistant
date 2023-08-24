---

copyright:
  years: 2018, 2023
lastupdated: "2023-08-24"

keywords: import workspace, import JSON, export JSON, upload JSON, download JSON, collaborate

subcollection: assistant

---

{{site.data.keyword.attribute-definition-list}}

# Adding dialog
{: #skill-dialog-add}

You can add one dialog skill to an assistant.

- If you are using the new experience, you need to [activate dialog](#activate-dialog-activating).
- If you are using the classic experience, you [create a dialog skill](#skill-dialog-add-task).

## Activating dialog
{: #activate-dialog-activating}

To activate the dialog feature in the new experience:

1.  Create or open an assistant where you want to use a dialog as the primary conversation with users.

1.  Open **Assistant settings** ![Gear icon](../../icons/settings.svg).

1.  Click **Activate dialog**.

    ![Activate dialog](images/activate-dialog.png){: caption="Activate dialog" caption-side="bottom"}

1.  In the confirmation that displays, click **Activate dialog** again.

    ![Activate dialog](images/activate-dialog-modal.png){: caption="Activate dialog" caption-side="bottom"}

Once you activate the dialog feature, it takes precedence over actions. You can use actions to supplement a dialog-based conversation, but the dialog drives the conversation with users to match their requests. For more information, see [Calling actions from a dialog](/docs/watson-assistant?topic=watson-assistant-dialog-call-action).

## Create the dialog skill
{: #skill-dialog-add-task}

To add a skill in the classic experience, complete the following steps:

1.  On the Skills page, click **Create skill**.

1. Choose **Dialog skill**.

1.  Do one of the following:

    - To create a new dialog skill, remain on the *Create skill* tab.
    
    - To add the dialog sample skill that is provided with the product as a starting point for your own skill or as an example to explore before you create one yourself, open the *Use sample skill* tab, and then click the sample labeled **TYPE: Dialog**. You can skip the remaining steps.

    - To add a skill that was downloaded previously, you can upload it as a JSON file. Open the *Upload skill* tab. Drag a file or click **Drag and drop file here or click to select a file** and select the JSON file you want to upload.

      The uploaded JSON file must use UTF-8 encoding, without byte order mark (BOM) encoding. The JSON cannot contain tabs, newlines, or carriage returns.
      {: important}

      The maximum size for a skill JSON file is 10 MB. If you need to upload a larger skill, consider using the REST API. For more information, see the [API Reference](https://cloud.ibm.com/apidocs/assistant/assistant-v1?curl=#createworkspace){: external}.
      {: tip}

      Click **Upload**.

1.  Specify the details for the skill:

    - **Name**: A name no more than 64 characters in length. A name is required.
    - **Description**: An optional description no more than 128 characters in length.
    - **Language**: The language of the user input the skill will be trained to understand. The default value is English.

1.  For **Skill type**, choose Dialog.

1.  Click **Create skill**.

After you create the dialog skill, it appears as a tile on the Skills page. Now, you can start identifying the user goals that you want the dialog skill to address.

### Adding the skill to an assistant
{: #skill-dialog-add-to-assistant}

You can add one dialog skill to an assistant. You must open the assistant tile and add the skill to the assistant from the assistant configuration page; you cannot choose the assistant that will use the skill from within the skill configuration page. One dialog skill can be used by more than one assistant.

1.  From the Assistants page, click to open the tile for the assistant to which you want to add the skill.

1.  Click **Add an actions or dialog skill**.

1.  Click **Add existing skill**.

    Click the skill that you want to add from the available skills that are displayed.

When you add a dialog skill from here, you get the development version. If you want to add a specific skill version, add it from the skill's *Versions* page instead.
