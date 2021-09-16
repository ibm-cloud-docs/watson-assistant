---

copyright:
  years: 2018, 2021
lastupdated: "2021-09-01"

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

# Changing the topic of the conversation
{: #change-topic}

In general, an action is designed to lead a customer through a particular process without any interruptions. In real life, however, conversations almost never follow such a simple flow. In the middle of a conversation, customers might get distracted, ask questions about related issues, misunderstand something, or just change their minds about what they want to do.
{: shortdesc}

The **Change conversation topic** feature enables your assistant to handle these digressions, dynamically responding to the user by changing the conversation topic as needed.

## How changing the topic works

This example shows a customer changing the conversation topic while entering credit-card information. When the assistant asks `What is your CVV number?`, the customer (who is new to credit cards) asks what a CVV is. The assistant is designed to handle this possibility, so it switches to a different action that answers the customer's question. It then continues where it left off.

![Example: changing the conversation topic](images/changing-topic-example.gif)

The assistant determines when to change the conversation topic as follows:

1. When the assistant asks a question and receives a response, it first validates the response to see if it answers the question. In the CVV example, the assistant expects a number as a response.

1. If the input is not recognized as an answer to the question, the assistant then evaluates the input to see if it matches the **Customer starts with** examples of any other action of the assistant. (Changing the topic cannot switch the conversation to a different assistant.)

    If the input does not answer the question, and it does not match any existing action of the assistant, a step validation error results. For more information about validation errors and how they are handled, see [Handling errors in the conversation](/docs/watson-assistant?topic=watson-assistant-handle-errors).
    {: note}

1. If the input matches a different action, the assistant switches to the matching action. The assistant will only change to the new action if it has a confidence score match of 20% or higher. In the example, the customer's response (`What's a CVV number?`) is not a valid response, but it does match another action that is designed to answer this question. The matching action is triggered, answering the customer's question.

1. After the second action completes, the assistant returns to the original action, continuing with the step where the customer changed the topic. In the example, after answering the customer's question, the assistant returns to the original action and repeats the question `What is your CVV number?`.

## Enabling and disabling changing the topic

By default, the **Change conversation topic** feature is enabled for all assistants and actions. You don't have to do anything to take advantage of this feature.

However, some processes are best completed without interruption, so you might want to disable this feature. You can do this either for the entire assistant, or just for an individual action.

To disable changing the topic for the entire assistant:

1. From the **Build** page of the assistant, click the **Settings** icon ![Gear icon](images/gear-icon.png).

1. In the settings window, click the **Change conversation topic** tab.

1. Toggle the switch to **Off**.

To disable changing the topic for an individual action:

1. While editing the action, click the click the **Settings** icon ![Gear icon](images/gear-icon.png).

1. In the Action Settings window, toggle the **Change conversation topic** switch to **Off**.
