---

copyright:
  years: 2022
lastupdated: "2022-08-12"

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

{{site.data.content.earlyaccess}}

# Trigger phrases
{: #trigger-phrases}

Use the *Trigger phrases* action to add words or phrases to two separate groups. The first group connects customers with an agent. The second group shows customers a customizable warning message.
{: shortdesc}

By default, this action has two steps&mdash;the *Connect to agent* step and the *Show warning* step. To see how this action works, click **Set by assistant** in the list of actions, and then click *Trigger phrases*.

## Connect to agent
{: #connect-to-agent}

The first step of the *Trigger phrases* action is the *Connect to agent* step. The *Connect to agent* step connects a customer with an agent if any trigger phrases are detected in the customer's input. Use this step to capture any key phrases where it’s important to connect a customer with another person rather than activate any further actions.

For example, you might add `hurt` and `harm` as trigger phrases for the *Connect to agent* step:

![Adding trigger phrases to the Connect to agent step](images/connect-to-agent-phrases.png)

In this example, if a customer enters `hurt` or `harm`, they are automatically connected with an agent.

## Show warning
{: #show-warning}

The second and final step of the *Trigger phrases* action is the *Show warning* step. The *Show warning* step shows a customizable warning message to your customer if any trigger phrases are detected in the customer's input. Use this step to discourage customers from interacting with your assistant in potentially harmful ways, such as using profanity.

For example, you might add `darn`, `dang`, and `heck` as trigger phrases for the *Show warning* step:

![Adding trigger phrases to the Show warning step](images/show-warning-phrases.png)

In this example, you can customize your warning message to `Please do not swear.`:

![Warning message for trigger phrases](images/assistant-warning-messsage.png)

Then, if a customer enters `darn`, `dang`, or `heck`, the assistant responds, `Please do not swear.`
