---

copyright:
  years: 2015, 2023
lastupdated: "2023-07-07"

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
{:tag-ibm-cloud: .tag data-tag-color="blue"}
{:tag-cp4d: .tag data-tag-color="magenta"}



# Integrating with Slack
{: #deploy-slack}

[IBM Cloud]{: tag-ibm-cloud}

Slack is a cloud-based messaging application that helps people collaborate with one another.
{: shortdesc}

After you create an action, you can integrate your assistant with Slack.

When integrated, depending on the events that you configure the assistant to support, your assistant can respond to questions that are asked in direct messages or in channels where the assistant is directly mentioned.

An example and instructions on how to create a Slackbot using {{site.data.keyword.conversationshort}}, Slack, and Db2 are given in the solution tutorial, [Build a database-driven Slackbot](https://cloud.ibm.com/docs/solution-tutorials?topic=solution-tutorials-slack-chatbot-database-watson).

## Adding the Slack integration
{: #deploy-slack-task}

1. Go to the **Integrations** page by clicking the integrations icon (![Integrations icon](images/integrations-icon.png)) in the left menu.

1. Click **Add** on the **Slack** tile.

1. Click **Confirm**.

1.  You need to have a Slack app to connect to.

    If you don’t have a Slack app, create one now. See [Starting with Slack apps](https://api.slack.com/start){: external}.

1.  Go to the [Your Apps](https://api.slack.com/apps){: external} page on the Slack website, and then click the app you want to use.

    Open the Slack app in a new browser tab, so you can easily switch back and forth between the Slack app settings page and {{site.data.keyword.conversationshort}} Slack integration configuration page.
    {: tip}

1.  From the settings page for your Slack app, open the **App Home** page.

1.  Add access scopes for your Slack app.

    The button label might be *Review Scopes to Add* or *Update scopes* depending on whether you are creating a new app or editing an app that you created before February 2020.

    The method for Slack access changed. For more information about it, read the [Slack blog post](https://medium.com/slack-developer-blog/more-precision-less-restrictions-a3550006f9c3){: external} about it.
    {: note}

1.  Assign bot token scopes to your Slack app. At a minimum, apply the following scopes:

    - `app_mentions:read`
    - `chat:write`
    - `im:history`
    - `im:read`
    - `im:write`

1.  Click *Install App to Workspace*, and then allow the installation when prompted.

    If you are editing scopes for an existing application, reinstall it.

1.  From the Slack settings App Home page, enable the *Always Show My Bot As Online* setting.

1.  Go to the *OAuth and Permissions* page in Slack, copy the *Bot User OAuth Access Token*.

1.  From the {{site.data.keyword.conversationshort}} Slack integration configuration page, paste the token that you copied in the previous step into both the **OAuth access token** and **Bot user OAuth access token** fields.

1.  On the Slack app settings page, go to the *Basic Information* page, and then find the *App Credentials* section. Copy the app credential verification token.

1.  From the {{site.data.keyword.conversationshort}} Slack integration configuration page, paste the verification token that you copied in the previous step into the **Verification token** field.

1.  Click **Generate request URL**, and then copy the generated request URL.

1.  Return to the Slack app settings page. Open the *Event Subscriptions* page, and then turn on *Enable Events*. Paste the request URL that you copied in the previous step into the field.

1.  On the *Event Subscriptions* page in Slack, find the *Subscribe to Bot Events* section. Click *Add Bot User Event*, and then select the event types you want to subscribe to. You must select at least one of the following types:

    - `message.im`: Listens for message events that are posted in a direct message channel.
    - `app_mention`: Listens for only message events that mention your app or bot.

      Choose the *app_mention* entry in normal font, *not* the app_mention entry that is in bold font.
      {: note}

1.  Click *Save Changes*.

1.  Optional: To add support for showing buttons, menus, and disambiguation options in the Slack app, go to the *Interactive Components* tab and enable the feature. Paste your request URL in the provided text entry field, and then click *Enable Interactive Components*.

## Action considerations
{: #deploy-slack-action}

The rich responses that you add to an action are displayed in a Slack channel as expected, with the following exceptions:

- **Connect to live agent**: This response type is ignored.

- **Option**: This response type shows a list of options that the user can choose from.

  - After a user clicks one of the options, the choices disappear and are replaced by the user input that is generated by the user's choice. If you include multiple response types in a single response, position the option response type last. Otherwise, the output might contain a mix of responses and user inputs that can confuse the user.
  - If the options are displayed in a drop-down list, then each option value must be 75 characters or fewer in length. When a list includes 5 or more options, it is displayed in a drop-down list automatically.







## Chatting with the assistant
{: #deploy-slack-try}

To start a chat with the assistant, complete the following steps:

1.  Open Slack, and go to the workspace associated with your app.
1.  Click the application that you created from the Apps section.
1.  Chat with the assistant.

The welcome action is not processed by the Slack integration. The welcome message is not displayed in the Slack channel like it is in the assistant preview. It is not triggered from here because nodes with the `welcome` special condition are skipped in action flows that are started by users. Slack waits for the user to initiate the conversation.



The action flow for the current session is restarted after 60 minutes of inactivity (5 minutes for Lite and Standard plans). This means that if a user stops interacting with the assistant, after 60 (or 5) minutes, any context variable values that were set during the previous conversation are set to null or back to their default values.
