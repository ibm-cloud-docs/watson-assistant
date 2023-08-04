---

copyright:
  years: 2022, 2023
lastupdated: "2023-08-04"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Response modes
{: #action-response-modes}

[IBM Cloud]{: tag-ibm-cloud}

You can choose a response mode for each action to set how it behaves. The modes are *clarifying* and *confident*.
{: shortdesc}

**Clarifying mode**: Start here. In the clarifying mode, your assistant is eager to ask questions so you can ensure that your customer gets to the action they need. An assistant is more likely to ask questions to be sure an action matches what a customer is asking. A new or untested action gets the training that it needs.

**Confident mode**: Take the next step. After you use analytics to improve your assistant, use the confident mode. Your assistant solves customer issues with authority and accuracy. An assistant is less likely to ask questions and is more likely to trigger actions that match. Use confident mode after you test and train actions.

Response modes are a beta feature that is available for evaluation and testing purposes on IBM Cloud only.
{: beta}

## Settings
{: #action-response-modes-settings}

Settings for the two modes are in the global settings. For more information, see [Global settings for actions](/docs/watson-assistant?topic=watson-assistant-actions-global-settings).

You can choose what mode to use when you create a new action. Clarifying mode is the default and is designed for use with new, untested actions that need training.

The settings are:

**Clarify when one action matches**: If an assistant prioritizes one action that it thinks matches the customer's request, it can clarify the match by asking the customer to confirm. This clarification helps you ensure that the action is the right one and allows the customer to give input before proceeding. For example, if the assistant thinks that a single action named `Pay Bill` is the right one, it can clarify the choice by asking the customer `Did you mean: Pay Bill`.

**Clarify when more than one action matches**: When your assistant finds that more than one action might fulfill a customer's request, it can automatically ask for clarification. Instead of guessing which action to use, your assistant shows a list of the possible actions to the customer and asks the customer to pick the right one.

**Offer support option when asking a clarifying question**: The assistant can include a choice to connect to other support. If the customer picks this choice, the assistant uses your Fallback action.

**Step validation attempts before offering support**: If a customer provides invalid answers for a step in an action, the assistant can offer to connect to other support in the Fallback action. The step validation count measures how many invalid answers can occur before the assistant provides this choice.

This table shows the default settings for each mode. 

|  | Clarifying | Confident |
| --- | --- | --- |
| Clarify when one action matches | More often | Sometimes |
| Clarify when more than one action matches | More often | Sometimes |
| Offer support option when asking a clarifying question | More often | Sometimes |
| Step validation attempts before offering support | 1 time | 3 times |
{: caption="Default settings" caption-side="bottom"}

## Choosing a mode for individual actions
{: #action-response-modes-individual-actions}

When you edit an action, you can see the mode that it uses and change it if you need to.

1. Click the Action response mode icon ![Action response mode icon](images/response-mode-icon.svg). The mode in use is checked.

   ![Action response mode](images/response-mode-modal.png){: caption="Action response mode" caption-side="bottom"}

1. Click the other mode if you want to change it, and then click **Save response mode**.

## Override system defaults
{: #action-response-modes-customize}

[Enterprise]{: tag-purple}

For Lite and Plus plans, the default settings can’t be changed. For Enterprise plans, you can override system defaults to customize each mode.

To override system defaults:

1. On the **Actions** page, click **Global settings** ![Gear icon](../../icons/settings.svg).

1. On the **Clarifying questions** tab, click **Customize modes**.

1. Set the **Override System Defaults** toggle to **On**. This toggle is available only for Enterprise plans.

1. Use the menu to modify any of the settings for either mode.

If you customize, the choices for each setting are;

| Setting | Choices |
| --- | --- |
| Clarify when one action matches | More often, Sometimes, Less often |
| Clarify when more than one action matches | More often, Sometimes, Less often |
| Offer support option when asking a clarifying question | More often, Sometimes, Less often |
| Step validation attempts before offering support | 1 time, 2 times, 3 times |
{: caption="Mode customization choices" caption-side="bottom"}

If you customize modes, be sure to test any changes.
{: note}
