---

copyright:
  years: 2024
lastupdated: "2024-04-12"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Copying an action to another assistant
{: #copy-action}


You can copy an action from one assistant to another. When you copy an action, references to other actions, variables, and saved responses are also copied.

To copy an action to another assistant:

1. Click the overflow menu on the action that you want and select **Copy to an assistant**.

   ![Copy to an assistant](images/manage-actions-copy.png){: caption="Copy to an assistant" caption-side="bottom"}

1. Choose the destination assistant for the copy. If the action doesn't exist in the destination assistant, it copies as new. If the action exists and there is a conflict, the copy overwrites the existing one.

   ![Copy to an assistant](images/manage-actions-copy-destination.png){: caption="Copy to an assistant" caption-side="bottom"}

1. If there are references to other actions, variables, or saved responses, you can review the list. References without a conflict are saved as new. If there are conflicts, you can choose to overwrite the existing reference, or skip copying it. If there are no references, this step doesn't appear.

   ![Copy to an assistant](images/manage-actions-copy-references.png){: caption="Copy to an assistant" caption-side="bottom"}

1. Click **Apply** to finish copying the action to the other assistant.

You can copy an action from one assistant to another when you want to reuse the action content and configuration in the destination assistant.

When you copy the action to the destination assistant, references to actions, saved responses, and variables in the source assistant are copied.

To copy an action to another assistant:

1. Click the **Overflow** menu on the action that you want and select **Copy to an assistant**.

   ![Copy to an assistant](images/manage-actions-copy.png){: caption="Copy to an assistant" caption-side="bottom"}

1. Click the **drop-down** icon to select the destination assistant for the copy.

   ![Copy to an assistant](images/manage-actions-copy-destination.png){: caption="Copy to an assistant" caption-side="bottom"}

1. In the review references page, you can see the list of actions, variables, and saved responses. 
See 'Table. Conflict status for references' for an explanation of conflicting and non-conflicting references and their respective outcomes.

| Type of references | Conflict status | Outcome |
| --- | --- | --- |
| * Actions \n * Variables \n * Saved responses | No | By default, it saves a new reference to the target assistant. |
| * Actions \n * Variables \n * Saved responses | Yes | You can select one of the following options:  \n * Overwrite:  \n Overwrites the existing action in the destination assistant.  \n * Skip:  \n Skips copying the action to the destination assistant. |

{: caption="Conflict status for references" caption-side="bottom"}

   If you want to overwrite all the conflicting items in the destination assistant, click the **Overwrite all** button. {: tip}
   If you want to skip copying all the conflicting items to the destination assistant, click the **Skip all** button.
   {: tip}

   ![Copy to an assistant](images/copy-action-assistant.svg){: caption="Copy to an assistant" caption-side="bottom"}

1. Click **Apply** to finish copying the action to the other assistant.
