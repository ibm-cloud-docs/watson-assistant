---

copyright:
  years: 2021, 2025
lastupdated: "2025-01-08"

keywords: billing, data centers, MAU, monthly active users, service plans

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Managing your plan
{: #admin-managing-plan}

Learn about:
- [Plan information](#admin-managing-plan-information)
- [Upgrading your plan](#admin-managing-plan-upgrade)

## Plan information
{: #admin-managing-plan-information}

Billing for the use of {{site.data.keyword.conversationshort}} is managed through your {{site.data.keyword.cloud}} account.

The metrics that are used for billing purposes differ based on your plan type. You can be billed based on the number of API calls made to a service instance or on the number of active users who interact with the instance.

For answers to common questions about subscriptions, see [How you're charged](/docs/account?topic=account-charges){: external}.

Explore the {{site.data.keyword.conversationshort}} [service plan options](https://www.ibm.com/products/watsonx-assistant/pricing){: external}.

### Paid plan features
{: #admin-managing-plan-paid}

The following features are available only to users of a Plus plan or higher. [Plus]{: tag-green}

- [Phone integration](/docs/watson-assistant?topic=watson-assistant-deploy-phone)
- [Private endpoints](/docs/watson-assistant?topic=watson-assistant-admin-securing#security-private-endpoints)
- [Search](/docs/watson-assistant?topic=watson-assistant-search-add)
- [{{site.data.keyword.conversationshort}} v2 API](/apidocs/assistant-v2#listlogs){: external}
- [Log webhook](/docs/watson-assistant?topic=watson-assistant-webhook-log)

The [v2 Logs API](/apidocs/assistant-v2#listlogs){: external} is available with a free trial of the Plus plan.
{: note}

The following features are available only to users of Enterprise plans. [Enterprise]{: tag-purple}

- [Activity tracking](/docs/watson-assistant?topic=watson-assistant-at-events)
- [Multiple environments](/docs/watson-assistant?topic=watson-assistant-multiple-environments)
- [Override system defaults for response modes](/docs/watson-assistant?topic=watson-assistant-action-response-modes#action-response-modes-customize)
- [Sending events to Segment](/docs/watson-assistant?topic=watson-assistant-segment-add)

The plan type of the service instance you are currently using is displayed in the page header. You can upgrade from one plan type to another. For more information, see [Upgrading](#admin-managing-plan-upgrade).

### User-based plans explained
{: #admin-managing-plan-user-based}

Unlike API-based plans, which measure usage by the number of API calls made during a month, the Plus and Enterprise plans measure usage by the number of monthly active users.

A monthly active user (MAU) is any unique user who has at least one interaction with your assistant or custom application over the calendar billing month.

A unique user is recognized by the user ID that is associated with the person that interacts with your assistant. The web chat and other built-in integrations set this property for you automatically.

You can calculate MAUs on your own, for both {{site.data.keyword.cloud_notm}} and {{site.data.keyword.icp4dfull_notm}}. To calculate MAUs, use the [logs](/apidocs/assistant-v2#listlogs){: external} endpoint to export conversations. For a particular month, count the number of unique user IDs found in the results. User IDs with more than 50 messages (API calls) in a month are counted more than once for every 50 messages. In a common use case, where each user ID represents a customer conversing with an assistant, the average number of messages per user are typically much fewer than 50 messages, so it's unusual to count a user ID more than once.

### Specifying the user ID with the REST API
{: #admin-managing-plan-userid-api}

If you are using a custom client with the {{site.data.keyword.conversationshort}} API, you must set the `user_id` property in the message payload your client sends to the `message` method. The `user_id` property is specified at the root of the request body, as in this example:

```json
{
  "input": {
    "message_type": "text",
    "text": "I want to cancel my order"
  },
  "user_id": "my_user_id"
}
```

In some older SDK versions, the `user_id` property is not supported as a top-level method parameter. As an alternative, you can specify `user_id` within the nested `context.global.system` object.
{: important}

For more information about the `user_id` property, see the API reference documentation:
  
- [v2 stateless `/message`](/apidocs/assistant-v2#messagestateless){: external}
- [v2 stateful `/message`](/apidocs/assistant-v2#message){: external}

### If the user ID is not specified
{: #admin-managing-plan-no-userid}

If you are using a custom client application and do not set a `user_id` value, the service automatically sets it to one of the following values:

- **session_id (v2 API only)**: A property defined in the v2 API that identifies a single conversation between a user and the assistant. A session ID is provided in `/message` API calls that are generated by the built-in integrations. The session ends when a user closes the chat window or after the inactivity time limit is reached.

    If you use the stateless v2 message API, you must specify the session_id with each message in an ongoing conversation (in `context.global.session_id`).
    {: note}

- **conversation_id (v1 API only)**: A property defined in the v1 API that is stored in the context object of a `/message` API call. This property can be used to identify multiple `/message` API calls that are associated with a single conversational exchange with one user. However, the same ID is only used if you explicitly retain the ID and pass it back with each request that is made as part of the same conversation. Otherwise, a new ID is generated for each new `/message` API call.

If the same person chats with your assistant on three separate occasions over the same billing period, how you represent that user in the API call impacts how the interactions are billed. If you identify the user interaction with a `user_id`, it counts as one use. If you identify the user interaction with a `session_id`, then it counts as three uses because a separate session is created for each interaction.

Design any custom applications to capture a unique `user_id` or `session_id` and pass the information to {{site.data.keyword.conversationshort}}. Choose a non-human-identifiable ID that doesn't change throughout the customer lifecycle. For example, don't use a person's email address as the user ID. In fact, the `user_id` syntax must meet the requirements for header fields as defined in [RFC 7230](https://datatracker.ietf.org/doc/html/rfc7230#section-3.2){: external}.

The built-in integrations derive the user ID in the following ways: 

- For Facebook integrations, the `user_id` property is set to the sender ID that Facebook provides in its payload.
- For Slack integrations, the `user_id` property is a concatenation of the team ID, such as `T09LVDR7Y`, and the member ID of the user, such has `W4F8K9JNF`. For example, `T09LVDR7YW4F8K9JNF`.
- For web chat, you can set the value of the `user_id` property.

Billing is managed per monthly active user per service instance. If a single user interacts with assistants that are hosted by different service instances that belong to the same plan, each interaction is treated as a separate use. You are billed for the user's interaction with each service instance separately.

### Handling anonymous users
{: #admin-managing-plan-billing-anonymous}

If your custom application or assistant interacts with users who are anonymous, you can generate a randomized universally unique ID to represent each anonymous user. For more information about UUIDs, see [RFC 4122](https://datatracker.ietf.org/doc/html/rfc4122.html){: external}.

- For web chat, if you do not pass an identifier for the user when the session begins, the web chat creates one for you. It creates a first-party cookie with a generated anonymous ID. The cookie remains active for 45 days. If the same user returns to your site later in the month and chats with your assistant again, the web chat integration recognizes the user. And you are charged only once when the same anonymous user interacts with your assistant multiple times in a single month.

If an anonymous user logs in and later is identified as being the same person who submitted a request with a known ID, you are charged twice. Each message with a unique user ID is charged as an independent active user. To avoid this situation, you can prompt users to log in before you initiate a chat. Or, you can use the anonymous user ID to represent the user consistently.

### Data centers
{: #admin-managing-plan-regions}

{{site.data.keyword.cloud_notm}} has a network of global data centers that provide performance benefits to its cloud services. See [{{site.data.keyword.cloud_notm}} global data centers](https://www.ibm.com/cloud/data-centers/){: external} for more details.

You can create {{site.data.keyword.conversationshort}} service instances that are hosted in the following data center locations:

| Location    | Location code | API location     |
|-------------|---------------|--------------    |
| Dallas      | `us-south`      | N/A            |
| Frankfurt   | `eu-de`         | `fra`          |
| Sydney      | `au-syd`        | `syd`          |
| Tokyo       | `jp-tok`        | `tok`          |
| London      | `eu-gb`         | `lon`          |
| Washington DC  | `us-east`    | `wdc`          |
{: caption="Data center locations" caption-side="bottom"}

## Upgrading your plan
{: #admin-managing-plan-upgrade}

You can explore the {{site.data.keyword.conversationshort}} [service plan options](https://www.ibm.com/products/watsonx-assistant/pricing){: external} to decide which plan is best for you.

The page header shows the plan that you are using today. To upgrade your plan, complete these steps:

1. Do one of the following things:

   - **Trial plan only**: The number of days that are left in your trial is displayed in the page header. To upgrade your plan, click **Upgrade** from the page header before your trial period ends.

   - For all other plan types, click **Manage** ![user icon](/images/user--avatar.svg), and then choose **Upgrade** from the menu.

1. From here, you can see other available plan options. For most plan types, you can step through the upgrade process yourself.

    - If you upgrade to an Enterprise with Data Isolation plan, you cannot do an in-place upgrade of your service instance. An Enterprise with Data Isolation plan instance must be provisioned for you first.
    - You cannot change from a Trial plan to a Lite plan.

For answers to common questions about subscriptions, see the [How you're charged](/docs/account?topic=account-charges){: external}.
