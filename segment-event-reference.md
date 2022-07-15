---

copyright:
  years: 2015, 2021
lastupdated: "2022-07-15"

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

# Segment event reference
{: #segment-event-reference}

The following tables show details of the events that {{site.data.keyword.conversationshort}} sends to Segment using the [Segment extension](/docs/watson-assistant?topic=watson-assistant-segment-add). These events appear as tables in your Segment warehouse, and as regular events in other Destinations.

Only events generated using the {{site.data.keyword.conversationshort}} v2 API and associated with a user ID are included.
{: note}

## Message Handled
{: #segment-event-reference-message-handled}

Sent when the assistant completes handling of a message.

| Property          | Type     | Description |
|-------------------|----------|-------------|
| `accountId`       | String   | The ID of the IBM account. |
| `assistantId`     | String   | The ID of the assistant. |
| `browser`         | String   | The browser that was used to send the message. |
| `channel`         | String   | The channel the customer used to send the message (for example, `phone` or `chat`). |
| `device`          | String   | The type of device that was used to send the message. |
| `environment`     | String   | The environment in which the message was handled (such as `draft` or `live`.) |
| `language`        | String   | The language of the assistant. |
| `pageUrl`         | String   | The URL of the web page from which the message was sent. |
| `serviceInstance` | String   | The IBM Watson Assistant service instance. |
| `sessionId`       | String   | The ID of the session during which the message was handled. |
| `skillsInvoked`   | String[] | An array of strings listing all skills that were invoked during handling of the message (for example, `main skill` or `actions skill`). |

The following properties are included only for messages that were handled by an actions skill:

| Property                | Type     | Description |
|-------------------------|----------|-------------|
| `action`                | String   | The unique identifier of the action that was visited during handling of the message (for example, `action_202`). |
| `actionCompleted`       | Boolean  | Whether the action completed during handling of the message. |
| `actionCompletedReason` | String   | The reason the action completed (for example, `all_steps_done` or `fallback`.) |
| `actionStarted`         | Boolean  | Whether processing of the action started during handling of the message. |
| `actionTitle`           | String   | The title of the action that was visited during handling of the message (for example, `I want to pay my bill`). |
| `actionsVisited`        | String[] | An array of strings listing the actions visited during handling of the message. |
| `fallbackReason`        | String   | The reason why the fallback action was visisted (for example, escalated to human agent or no action matches). |
| `handler`               | String   | The name of any handler that was called. |
| `stepsVisited`          | String[] | An array of strings listing the steps visited during handling of the message. Each step name is prefixed with the action name. |
| `subaction`             | String   | The name of any subaction that was called during handling of the message. |

The following properties are included only for messages that were handled by a dialog skill:

| Property             | Type     | Description |
|----------------------|----------|-------------|
| `branchExited`       | Boolean  | Whether the dialog branch was exited during handling of the message. |
| `branchExitedReason` | String   | The reason the dialog branch was exited (for example, `completed`). |
| `nodesVisited `      | String[] | An array of strings listing the dialog nodes visited during handling of the message. For each dialog node, the string specifies the node title (if any) or the node ID. |

## Action Started
{: #segment-event-reference-action-started}

Sent when processing of an action (including subactions) begins.

| Property                | Type     | Description |
|-------------------------|----------|-------------|
| `accountId`             | String   | The ID of the IBM account. |
| `action`                | String   | The unique identifier of the action (for example, `action_202`). |
| `actionTitle`           | String   | The title of the action  (for example, `I want to pay my bill`). |
| `actionCompleted`       | Boolean  | Whether the action completed during the same conversation turn. |
| `actionCompletedReason` | String   | The reason the action completed (for example, `all_steps_done` or `fallback`.) |
| `assistantId`           | String   | The ID of the assistant. |
| `browser`               | String   | The browser that was used to send the message that triggered the action. |
| `channel`               | String   | The channel the customer used to send the message that triggered the action (for example, `phone` or `chat`). |
| `device`                | String   | The type of device that was used to send the message that triggered the action. |
| `environment`           | String   | The environment in which the action was started (such as `draft` or `live`.) |
| `fallbackReason`        | String   | The reason why the fallback action started (for example, escalated to human agent or no action matches). |
| `handler`               | String   | The name of any handler that was called. |
| `language`              | String   | The language of the assistant. |
| `pageUrl`               | String   | The URL of the web page from which the message that triggered the action was sent. |
| `serviceInstance`       | String   | The IBM Watson Assistant service instance. |
| `sessionId`             | String   | The ID of the session during which the message that started the action was sent. |
| `skillsInvoked`         | String[] | An array of strings listing all skills that were invoked during handling of the message that started the action (for example, `main skill` or `actions skill`). |
| `stepsVisited`          | String[] | An array of strings listing the steps visited during processing of the action. |
| `subaction`             | String   | The name of any subaction that was called. |

## Action Completed
{: #segment-event-reference-action-completed}

Sent when processing of an action (including subactions) ends.

| Property                | Type     | Description |
|-------------------------|----------|-------------|
| `accountId`             | String   | The ID of the IBM account. |
| `action`                | String   | The unique identifier of the action (for example, `action_202`). |
| `actionCompletedReason` | String   | The reason the action completed (for example, `all_steps_done` or `fallback`.) |
| `actionStarted`         | Boolean  | Whether the action was started during the same conversation turn. |
| `actionTitle`           | String   | The title of the action  (for example, `I want to pay my bill`). |
| `assistantId`           | String   | The ID of the assistant. |
| `browser`               | String   | The browser that was used to send the message that triggered the action. |
| `channel`               | String   | The channel the customer used to send the message that started the action (for example, `phone` or `chat`). |
| `device`                | String   | The type of device that was used to send the message that triggered the action. |
| `environment`           | String   | The environment in which the action completed (such as `draft` or `live`.) |
| `fallbackReason`        | String   | The reason why the fallback action was called (for example, escalated to human agent or no action matches). |
| `handler`               | String   | The name of any handler that was called by the action. |
| `language`              | String   | The language of the assistant. |
| `pageUrl`               | String   | The URL of the web page from which the message that triggered the action was sent. |
| `serviceInstance`       | String   | The IBM Watson Assistant service instance. |
| `sessionId`             | String   | The ID of the session during which the message that started the action was sent. |
| `skillsInvoked`         | String[] | An array of strings listing all skills that were invoked during handling of the message that started the action (for example, `main skill` or `actions skill`). |
| `stepsVisited`          | String[] | An array of strings listing the steps visited during processing of the action. |
| `subaction`             | String   | The name of any subaction that was called by the action. |

## Session Started
{: #segment-event-reference-session-started}

Sent when a new session is started.

**Note:** The v2 stateless API does not generate events for starting sessions.

| Property          | Type     | Description |
|-------------------|----------|-------------|
| `accountId`       | String   | The ID of the IBM account. |
| `assistantId`     | String   | The ID of the assistant. |
| `browser`         | String   | The browser that was used to send the message that started the session. |
| `channel`         | String   | The channel that started the session (for example, `phone` or `chat`). |
| `device`          | String   | The type of device that was used to send the message that started the session. |
| `environment`     | String   | The environment in which the session was started (such as `draft` or `live`.) |
| `pageUrl`         | String   | The URL of the web page from which the message that started the session was sent. |
| `serviceInstance` | String   | The IBM Watson Assistant service instance. |
| `sessionId`       | String   | The ID of the session. |

