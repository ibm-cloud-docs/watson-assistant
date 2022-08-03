---

copyright:
  years: 2020, 2022
lastupdated: "2022-05-26"

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
{:preview: .preview}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:table: .aria-labeledby="caption"}

{{site.data.content.classiclink}}

# Comparing actions and dialog
{: #comparing-actions-dialog}

Choose the right type of conversation for your use case.
{: shortdesc}

## Actions benefits
{: #comparing-benefits-actions}

Using actions is the best choice when you want to approach the assistant with a focus on content. Actions offers the following benefits:

- The process of creating a conversational flow is easier. People who have expertise with customer care can write the words that your assistant says. With a simplified process anyone can build a conversation. You don't need knowledge about machine learning or programming.
- Actions provide better visibility into the customer's interaction and satisfaction with the assistant. Because each task is discrete and has a clear beginning and ending, you can track user progress through a task and identify snags.
- The conversation designer doesn't have to manage data collected during the conversation. By default, your assistant collects and stores information for the duration of the current action. You don't need to take extra steps to delete saved data or reset the conversation. But if you want, you can store certain types of information, such as the customer's name, for the duration of a conversation.
- Many people can work at the same time in separate, self-contained actions. The order of actions within a conversation doesn't matter. Only the order of steps within an action matters. And the action author can use drag and drop to reorganize the steps in the action for optimal flow.

## Dialog benefits
{: #comparing-benefits-dialog}

A dialog-based conversation is the best choice when you want greater control over the logic of the flow. The dialog editor exposes more of the underlying artifacts (such as intents and entities) used to build the AI models. The dialog flow uses an if-then-else style structure that might be familiar to developers, but not to content designers or customer-care experts.

## How actions are different from dialog
{: #comparison}

If you are already familiar with dialog-based conversations, learn more about how actions compares.

| Feature | Actions | Dialog |
|---------|---------------|--------------|
| Automatic reset of context | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Keep track of context | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Collect info, as with slots | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Contextual entities | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Collect numbers (@sys-number detection) | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Detection of other system entities | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Connect to human agent response type | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Free text response type | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Image response type | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Options response type | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Search skill response type | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Rich text editor for text responses | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| User input validation | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Step logic validation | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Support multiple users by notifying them when simultaneous edits are made to the skill | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Use SpEL expressions | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Disambiguation | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Digression support | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Spelling correction | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Webhook (before or after every message) support | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Webhook (from a node) support | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Webhook (log all messages) support | | ![checkmark icon](../../icons/checkmark-icon.svg) |
{: row-headers}
{: class="comparison-table"}
{: caption="Conversational flow skill feature support" caption-side="top"}
{: summary="This table has row and column headers. The row headers identify features. The column headers identify the different skill types. To understand which features are supported by a skill, go to the row that describes the feature, and find the columns for the skill you are interested in."}

For some functions, there is parity but you follow different steps to implement the behavior you want.

- **Jump-to**: In actions, you can jump from one step to another. In a dialog, you use a jump-to to skip to a specific dialog node in the same branch of the conversation. With actions, you can jump to a different step within an action also. However, to do so, you use conditions on the intervening steps to prevent them from being processed, rather than using an explicit jump-to. The benefit of this approach is that it's easier to anticipate the path of a conversation and follow it later if there are not multiple jump-tos sprinkled throughout the flow.
- **Slots**: In a dialog, you add slots to a dialog node to call out a set of values that you want to collect from the user, and that you will take and store in any order. In actions, every step in the action acts like a slot. If the user provides information that address step 10 when answering the question to step 1, both step 1 and step 10 are filled. In fact, if you want step 10 to ask the question explicitly, you must select the **Always ask for this** option on step 10.

*Want to get started with actions, but need features that are available from a dialog?* Use both. Dialog is your primary conversation with users, but you can call an action from your dialog to perform a discrete task. For more information, see [Calling an actions from a dialog](/docs/watson-assistant?topic=watson-assistant-dialog-call-action).
{: tip}
