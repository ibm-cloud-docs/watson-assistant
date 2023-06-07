---

copyright:
  years: 2018, 2022
lastupdated: "2022-01-13"

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



# Skipping steps
{: #skip-steps}

Even if the conditions for a step are true, the step might not have anything to do.

Many steps ask the customer to answer a question (such as selecting which account to withdraw money from, or specifying the amount to withdraw). But if your customer has already answered this question, you don't want your assistant to ask for it again. For example, if the customer's initial input was `I want to withdraw money from my checking account`, the step that asks the user to select an account can (and probably should) be skipped.

Using this option means that the value for the step can be provided in the user's input elsewhere in the action, either before or after the step itself. Therefore, another benefit of choosing not to ask is that you give customers the ability to change their minds. If skipping is enabled for a step, the assistant can recognize responses that apply to that step at any point in the conversation. Therefore, the customer can change a previous choice by specifying a different option in a later response.

However, if your action asks for the same type of data in more than one step, use the **Allow skipping** setting to prevent the assistant from making incorrect assumptions. For example, you might have an action in which one step asks for a hotel check-in date and another step asks for the check-out date. If you skip asking, the assistant can mistake the check-in date for the check-out date.

To allow skipping on a step, click the **Settings** icon, select **Always ask for this information, regardless of earlier messages**, and then click **Apply**.
