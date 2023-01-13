---

copyright:
  years: 2020, 2023
lastupdated: "2023-01-13"

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
{{site.data.keyword.attribute-definition-list}}

{{site.data.content.earlyaccess}}

# Autolearning 
{: #autolearn}

Use *autolearning* to enable your assistant to learn from interactions with your customers.
{: shortdesc}

This beta feature is available in English-language assistants only.
{: note}

When customers interact with your assistant, they often make choices. If your assistant pays attention, it can learn from these user decisions over time.

For example, a customer might ask a question that the assistant isn't sure it understands. The assistant asks a clarifying question so the customer can choose the right action from a list. If customers most often click the same action (option #2, for example) from a similar list of actions, your assistant can learn that option #2 is the best answer to that type of question. 

Next time, the assistant can list option #2 as the first choice, so customers can get to it more quickly. If the pattern persists over time, it can change its behavior even more. Your assistant can return option #2 immediately, rather than asking a clarifying question.

As your assistant learns over time, your customers get the best answer more often and in fewer clicks.

## How autolearning works
{: #autolearn-how-it-works}

Before your assistant can learn from customer behavior, it must observe real conversation data. The conversations take place in a channel, such as web chat, or in a custom application. 

Logs of completed conversations from your live environment are the data source for observation. Your assistant analyzes the logs to gain insights. (It doesn't watch real-time clicks during a conversation.)

The observed insights help improve your assistant, providing a better customer experience.

## Enabling autolearning
{: #autolearn-task}

You can enable autolearning when the following conditions are met:

- **Ask clarifying question** is enabled in **Global settings**. For more information, see [Global settings for actions](/docs/watson-assistant?topic=watson-assistant-actions-global-settings).

- You have published a version of your assistant to the live environment. For more information, see [Publishing your content](/docs/watson-assistant?topic=watson-assistant-publish).

- Your customers are interacting with a channel or custom application connected to the live environment. 

To enable autolearning:

1. On the **Actions** page, click **Global settings** ![Global settings](images/gear-icon-black.png).

1. Click the **Autolearning** tab.

1. Set the **Autolearning in live environment** switch to **On**.

## Learning from your data
{: #autolearn-data}

Observations are made of only your customers' choices to improve only your assistant. These observations are not reused by IBM or shared in any way.

This observed user choices data is separate from the log data for which metrics are displayed on the **Analyze** page. The observation data is also separate from the information that is collected in all but Enterprise plan service instances and used by IBM for general service improvements. You can opt out of such use by specifying an opt-out header in your `/message` API requests. For more information, see [Opting out of log data use](/docs/watson-assistant?topic=watson-assistant-admin-securing#securing-log-opt-out).

To prevent your own assistant from applying what it learns by observing user choices to your assistant, you must turn off the autolearning feature.

