---

copyright:
  years: 2018, 2024
lastupdated: "2024-12-29"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Review customer conversations
{: #analytics-conversations}

The **Analyze** page of {{site.data.keyword.conversationshort}} provides a history of conversations between users and a deployed assistant. You can use this history to improve how your assistants understand and respond to user requests.
{: shortdesc}

In the **Analyze** page, you can see the summary of the conversations at the topic level in **View by recognition type** tab. 

![Conversations page](images/analytics-conversation-recognition-type-view.png)


In the **Message log** tab, you see the complete history of conversation between user and the assistant by turns. 

If you have activated dialog, you see the Entities column in the **Message log** tab.{: note}

 ![Conversation detail Message log](images/analytics-message-log-view.png)


## Choosing the environment and time period
{: #analytics-conversations-time-period}

To get started, choose the [environment](/docs/watson-assistant?topic=watson-assistant-publish-overview#environments) and date range you want to analyze. All conversations reflect data based on the environment and the date range you select. When you change the environment or the date range, the conversations on the page update to reflect the new date range. You can also use **Refresh** to ensure the latest data is shown.

![Time period](images/analytics-conversations-time-period.png)


## Filtering conversations
{: #analytics-conversations-filtering}

You can locate specific conversations by filtering the list of conversations. This lets you explore specific areas where your assistant might need improvement or updates to properly handle what your customers are asking about.

You can filter the conversations by:

- **Recognition type**: Select one or more from different type of actions, recognized or unrecognized user requests, search, intents.
- **Action**: Select one or more from user created actions, system created actions or intents.
- **Entity**: Select specific entities. You can choose one or more entities to review.

    The Entities filter appears in the **Message log** tab only if you have activated dialog in your assistant. {: note}


## Exploring conversations in detail
{: #analytics-conversations-exploring}

To explore individual conversations in detail, you can go to one of the following tabs in the **Analyze** page based on the level of details you want to analyze:

- **View by recognition type** 
  Displays the list of conversations with the topic-level details such as request, recognition type, and conversation timestamp and session ID. In the **View by recognition type** tab you see the following columns: 
  - The **Requests** column includes the questions or requests the user entered that initiated an action, started a search query, or weren't recognized. 
  - The **Recognition type** column shows you the type of action that got triggered from user requests.
  - The **Details** column shows the timestamp of a single conversation and its session ID.

  When you click on a request or timestamp, a panel opens showing the summary of requests, recognition status, and the duration of the conversation. 

- **Message log view**
  Displays the list of conversations between the users and assistant with the details such as consumer input, topic, assigned entity, timestamp, and session ID. In the **Message log** tab you see the following columns: 
  - The **Customer input** column shows you the customer responses or input. 
  - The **Recognition type** column shows you the type of action that got triggered from user requests.
  - The **Entities** column shows the entities assigned to each customer input.
     The Entities filter appears in the **Message log** tab only if you have activated dialog in your assistant. 
  - The **Details** column shows timestamp of a single conversation and its session ID.

  When you click on customer input or timestamp, a panel opens showing the conversation between the user and the assistant by turns along with duration and number of recognized input, customer input and searches.

 
