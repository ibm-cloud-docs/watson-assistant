---

copyright:
  years: 2018, 2022
lastupdated: "2022-10-17"

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

# Review customer conversations
{: #analytics-conversations}

The **Conversations** page of {{site.data.keyword.conversationshort}} provides a history of conversations between users and a deployed assistant. You can use this history to improve how your assistants understand and respond to user requests.
{: shortdesc}

Each timestamp represents a single conversation. The **Actions** column shows you how many actions, search queries, or unrecognized requests are included in that conversation. The **Requests** column includes the questions or requests the user entered that initiated an action, started a search query, or weren't recognized.

If you have activated dialog in your assistant, the **Actions** column is replaced by a **Topics** column.
{: note}

![Conversations page](images/analytics-conversations.png)

## Choosing the environment and time period
{: #analytics-conversations-time-period}

To get started, choose the [environment](/docs/watson-assistant?topic=watson-assistant-publish-overview#environments) and date range you want to analyze. All conversations reflect data based on the environment and the date range you select. When you change the environnment or the date range, the conversations on the page update to reflect the new date range. You can also use **Refresh** ensure the latest data is shown.

![Time period](images/analytics-conversations-time-period.png)

## Filtering conversations
{: #analytics-conversations-filtering}

You can locate specific conversations by filtering the list of conversations. This lets you explore specific areas where your assistant might need improvement or updates to properly handle what your customers are asking about.

You can filter by:

- **Actions**: Select specific actions. You can choose one or more actions to review.
- **Keyword**: Search by session ID or for specific key terms, phrases, or words in the conversations. For more information about session IDs, see [session_id](/docs/watson-assistant?topic=watson-assistant-admin-managing-plan#admin-managing-plan-no-userid).

- **Recognition**: Choose between recognized or unrecognized user questions or requests.
- **Search**: Choose between requests that initiated a search or requests that produced no search results.

The Actions and Keyword filters always appear at the top of the page. To show the Recognition and Search filters, click the **Additional filters** icon.

If you have activated dialog in your assistant, the **Actions** filter is replaced by a **Topics** filter.
{: note}

![Conversation filters](images/analytics-conversations-filters.png)

If you search for a specific session ID, enclose your search in quotation marks to ensure you receive an exact match on the full ID with its numbers and hyphen characters, for example: `"9015ab9a-2e13-4627-ae33-4179b1125cb5"`.
{: note}

## Exploring conversations in detail
{: #analytics-conversations-exploring}

To explore individual conversations in detail, you can click on any of the utterances or conversation time stamps.  A panel opens showing the full back and forth between your customer and the assistant, including step interactions. The panel also provides a summary of how many requests there were, how many were recognized, whether search was initiated, and the duration of the conversation.

![Conversation detail](images/analytics-conversations-side.png)
