---

copyright:
  years: 2018, 2022
lastupdated: "2022-03-09"

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

# Analyzing dialog and actions
{: #dialog-analyze}

The **Analyze** page provides a summary of the interactions between users and your assistant. If the dialog feature is enabled, the **Analyze** page remains the same, but some slight differences in functionality exist.
{: shortdesc}

## Overview tab
{: #dialog-analyze-overview}

When you view the **Overview** page, you can see action completion information in the **Action completion** diagram if a dialog node triggers an action. The **Action completion** diagram is empty if you are using only a dialog in your assistant. The three cards that display information about the most frequent actions, least frequent actions, and least completed actions are not available if your assistant uses only a dialog.

For more information about the **Analyze** page and how to use analytics with actions, see [Use analytics to review your entire assistant at a glance](/docs/watson-assistant?topic=watson-assistant-analytics-overview).

## Action completion tab
{: #dialog-analyze-action-completion}

The **Action completion** page of Watson Assistant provides an overview of how all your assistant's actions are doing. If the dialog feature is enabled, the **Action completion** tab is relevant only if a dialog node triggers an action. If your assistant uses only a dialog, then this tab will be empty.

For more information about understanding action completion with actions, see [Understand your most and least successful actions](/docs/watson-assistant?topic=watson-assistant-analytics-action-completion).

## Conversations tab
{: #dialog-analyze-conversations}

The **Conversations** page of Watson Assistant provides a history of conversations between users and a deployed assistant. You can use this history to improve how your assistants understand and respond to user requests.

From the **Conversations** page, an intent that directly calls an action is displayed in the **Topics** column. For example, you might set up an intent called `#buy_takeout` in the dialog, and that intent calls the `order pizza` action. This conversation topic is listed as `#buy_takeout > order pizza` in the **Topics** column.

You might also see **Dialog called action** listed in the **Requests** column next to a conversation. In this case, customer input triggered an intent. Then, the customer engaged with the assistant before an action was eventually called.

For more information about analyzing conversations with actions, see [Review customer conversations](/docs/watson-assistant?topic=watson-assistant-analytics-conversations).
