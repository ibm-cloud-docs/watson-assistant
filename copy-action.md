---

copyright:
  years: 2024
lastupdated: "2024-04-09"

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


