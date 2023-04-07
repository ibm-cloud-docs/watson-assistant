---

copyright:
  years: 2018, 2023
lastupdated: "2023-04-07"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Allowing your customers to change the topic of the conversation
{: #change-topic}

In general, an action is designed to lead a customer through a particular process without any interruptions. However, real conversations almost never follow such a simple flow. In the middle of a conversation, customers might get distracted, ask questions about related issues, misunderstand something, or change their minds about what they want to do.
{: shortdesc}

The **Change conversation topic** feature enables your assistant to handle these digressions, dynamically responding to the user by changing the conversation topic as needed.

## How changing the topic works
{: #change-topic-how}

This example shows a customer who changes the conversation topic while they are entering a credit card. When the assistant asks `What is your CVV number?`, the customer (who is new to credit cards) asks what a CVV is. The assistant is designed to handle this possibility, so it switches to a different action that answers the customer's question. It then continues where it left off.

![Example: changing the conversation topic](images/changing-topic-example.gif)

The assistant determines when to change the conversation topic as follows:

1. When the assistant asks a question and receives a response, it first validates the response to see whether it answers the question. In the CVV example, the assistant expects a number as a response.

1. If the input is not recognized as an answer to the question, the assistant then evaluates the input to see whether it matches another action. (Changing the topic cannot switch the conversation to a different assistant.)

    If the input does not answer the question, and it does not match any existing action of the assistant, a step validation error results. For more information about validation errors and how they are handled, see [Handling errors in the conversation](/docs/watson-assistant?topic=watson-assistant-handle-errors).
    {: note}

1. If the input matches a different action, the assistant switches to the matching action. The assistant changes to the new action if it has a confidence score match of 20% or higher. In the example, the customer's response (`What's a CVV number?`) is not a valid response, but it does match another action that is designed to answer this question. The matching action is triggered, answering the customer's question.

1. After the second action completes, the assistant asks the customer if they want to return to the original action. If they say `Yes`, the assistant continues with the step where the customer changed the topic. In the example, the assistant returns to the original action and repeats the question `What is your CVV number?`.

## Enabling and disabling changing the topic
{: #change-topic-enable}

By default, the **Change conversation topic** feature is enabled for all assistants and actions. (You need to enable the feature for steps that use a free text or regex response. For more information, see [Enabling changing the topic for free text and regex customer responses](#change-topic-free-text-regex).)

However, some processes are best completed without interruption, so you might want to disable this feature. You can disable for all actions, or just for an individual action.

To disable changing the topic for all actions:

1. From the **Actions** page of the assistant, click **Global settings** ![Gear icon](../../icons/settings.svg).

1. On the **Change conversation topic** tab, set the switch to **Off**.

1. Click **Save**, and then click **Close**.

To disable changing the topic for an individual action:

1. Edit an action, then click **Action settings** ![Gear icon](../../icons/settings.svg).

1. In the Action Settings window, toggle the **Change conversation topic** switch to **Off**.

### Disabling returning to the original topic
{: #change-topic-never-return}

Even when you allow changing the topic, you might not want a customer to return to the previous topic. If you need to do this:

1. Edit an action, then click **Action settings** ![Gear icon](../../icons/settings.svg).

1. Keep the **Change conversation topic** toggle switched to **On**.

1. Select the checkbox **Never return to original action after completing this action** to prevent the customer from returning to the previous action.

### Enabling changing the topic for free text and regex customer responses
{: #change-topic-free-text-regex}

By default, changing the conversation topic works differently for free text and regex responses. Customers can't change topics when:

- The assistant is asking for a free text response 
- An utterance matches the pattern in a regex response

 If you want a customer to be able to digress and change topics while entering a free text or regex answer:
 
 1. Within the step, click the **Settings** icon for the customer response.
 
 1. Enable the toggle **Allow customer to change topics during a free text response** or **Allow customer to change topics during a regex response**.

## Confirmation to return to previous topic
{: #change-topic-confirmation}

By default, new assistants are set to ask a "yes or no" question to confirm that the customers want to return to the previous action. You can modify these settings.

These settings aren't available when the assistant language is set to `Another language`, which uses the universal language model. For more information, see [Adding support for global audiences](/docs/watson-assistant?topic=watson-assistant-admin-language-support).
{: note}

To change the confirmation settings:

1. From the **Actions** page of the assistant, click **Global settings** ![Gear icon](../../icons/settings.svg).

1. On the **Change conversation topic** tab, click the **Confirmation** section.

Settings that you can change are:

| Setting | Description |
| --- | --- |
| Ask a confirmation question | Change the toggle to **Off** to disable the confirmation question for all actions. |
| Assistant says | By default, the assistant asks `Do you want to return to your previous topic?` and uses the system variable `Digressed from` to include the name of the previous action. Use the editor to modify the confirmation question. |
| Validation message | By default, the assistant says `Please reply back with yes or no` if the customer doesn't answer `Yes` or `No`. Use the editor to modify the validation message. |
| Show confirmation buttons | The assistant includes clickable `Yes` and `No` buttons with the confirmation question. Click the toggle to **Off** to disable the `Yes` and `No` buttons. |
{: caption="Confirmation settings" caption-side="top"}
