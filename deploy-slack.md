---

copyright:
  years: 2015, 2025
lastupdated: "2025-01-03"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}


# Integrating with Slack
{: #deploy-slack}

[IBM Cloud]{: tag-ibm-cloud}

Slack is a cloud-based messaging application that helps people collaborate with one another.
{: shortdesc}

After you create an action, you can integrate your assistant with Slack.

When integrated, depending on the events that you configure the assistant to support, your assistant can respond to questions that are asked in direct messages or in channels where the assistant is directly mentioned.

An example and instructions on how to create a Slackbot using {{site.data.keyword.conversationshort}}, Slack, and Db2 are given in the solution tutorial, [Build a database-driven Slackbot](/docs/solution-tutorials?topic=solution-tutorials-slack-chatbot-database-watson).

## Before you begin
{: #deploy-slack-before}

To integrate Slack with your assistant, you must have a Slack app and the necessary roles and permissions:

| Roles | Permissions |
| ----------- | ---------------------- |
| Workspace or <br> Org owner | View information <br> Post information <br> Perform actions |

To create a slack app, see [Quickstart: Start a workflow](https://api.slack.com/automation/quickstart){: external}.

For more information on roles and permissions, see [Slack-Getting started](https://slack.com/intl/en-gb/help/categories/360000049043){: external}.

## Adding the Slack integration
{: #deploy-slack-task}

1.  Go to the **Integrations** page by clicking the integrations icon (![Integrations icon](images/integrations-icon.png)) in the left menu.

1.  Click **Add** on the **Slack** tile.

1.  Then, click **Add** again.

### Get started
{: #deploy-slack-get-started}

There are four steps to setting up Slack:

-   Set up your Slack bot
-   Connect watsonx Assistant to Slack
-   Configure your Slack bot
-   Connect your assistant

### Set up your Slack bot
{: #deploy-slack-set-up}

1.  Go to the [Your Apps](https://api.slack.com/apps){: external} page on the Slack website, and then click the app you want to use or create a new one.

### Connect {{site.data.keyword.conversationshort}} to Slack
{: #deploy-slack-connect}

1.  On the **Slack app settings** page, go to the **Basic Information** tab and scroll down to the **App Credentials** section.

1.  Copy your verification token and paste it in the **Assistant setup** page.

1.  On the **Slack app settings** page, go to **Features** > **OAuth & Permissions** and scroll down to the **Bot Token Scopes** section.

1.  Click **Add an OAuth Scope** and select the following scopes:

    - `app_mentions:read`
    - `chat:write`
    - `im:history`
    - `im:read`
    - `im:write`

1.  Scroll up the page to the **OAuth Tokens for Your Workspace** section and click **Install App to Workspace**, and then click **Allow**.

    You should be redirected back to the OAuth & Permissions page. 

1.  Copy and paste your Bot user OAuth access token in the **Assistant setup** page.

1.  Click **Next** to continue.

### Configure your Slack bot
{: #deploy-slack-configure}

1.  Copy the **Generated request URL**.

1.  On the **Slack app settings** page, go to **Features** > **Event Subscriptions** and switch the **Enable Events** toggle `on`.

1.  Paste the URL link under **Request URL**.

    Wait until the you see **Verified** with a green tick next to **Request URL**.

1.  Scroll down and click **Subscribe to bot events**.

1.  Select the event types you want to subscribe to. You must select at least one of the following types:

    - `message.im`: Listens for message events that are posted in a direct message channel.
    - `app_mention`: Listens for only message events that mention your app or bot.

      Choose the *app_mention* entry in normal font, *not* the app_mention entry that is in bold font.
      {: note}

1.  Click **Save Changes**.

1.  On the **Assistant setup** page, click **Next**.

### Connect your assistant
{: #deploy-slack-connect-assistsnt}

1.  On the **Slack app settings** page, go to **Features** > **AppHome** and click **Edit** next to **App Display Name**.

1.  Click **Save** once you have made the changes.

1. Switch the toggle **Always Show My Bot as Online** toggle to `on`.

1. Go to the **Show Tabs** section and switch the **Messages Tab** toggle to `on`. 
1. Check the **Allow users to send Slash commands and messages from the messages tab** checkbox.

1.  If you want to add support for showing buttons, menus, and disambiguation options in the Slack app, do the following steps:

    1. Go to the **Interactivity & Shortcuts** tab and enable the feature
    1. Paste your request URL in the provided text entry field.
    1. Click **Save Changes**.

1. On the **Assistant setup** page, click **Finish**.

If a `token` field required for authentication is changed, then all entries in related fields must be filled and validated again.
{: note}

## Action considerations
{: #deploy-slack-action}

The rich responses that you add to an action are displayed in a Slack channel with the following exceptions:

- **Connect to live agent**: This response type is ignored.

- **Option**: This response type shows a list of options that the user can choose from.

  - After a user clicks one of the options, the existing selections disappear and replaces the selections with the user input that is generated by the user's selection. If you include multiple response types in a single response, you must position the option response type at the end to avoid confusions due to mix of responses and user inputs.

  - If the options are displayed in a drop-down list, then each option value must be 75 characters or fewer in length. When a list includes 5 or more options, it is displayed in a drop-down list.





## Chatting with the assistant
{: #deploy-slack-try}

To start a chat with the assistant, complete the following steps:

1.  Open Slack, and go to the workspace associated with your app.
1.  Click the application that you created from the Apps section.
1.  Chat with the assistant.

The welcome action is not processed by the Slack integration. The welcome message is not displayed in the Slack channel like it is in the assistant preview. It is not triggered from here because nodes with the `welcome` special condition are skipped in action flows that are started by users. Slack waits for the user to initiate the conversation.

The action flow for the current session is restarted after 60 minutes of inactivity (5 minutes for Lite and Standard plans). This means that if a user stops interacting with the assistant, after 60 (or 5) minutes, any context variable values that were set during the previous conversation are set to null or back to their default values.
