---

copyright:
  years: 2023
lastupdated: "2023-02-13"

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

{{site.data.content.classiclink}}

# Integrating with Microsoft Teams
{: #deploy-microsoft-teams}

[IBM Cloud]{: tag-ibm-cloud}

Add a chatbot to Microsoft Teams to create and customize a productive hub where content, tools, and people come together to chat, meet, and collaborate. 
{: shortdesc}

After you [create an action](docs/watson-assistant?topic=watson-assistant-build-actions-overview), you can use this integration to connect your assistant with Microsoft Teams.

## Before you begin
{: #deploy-microsoft-teams-account}

Sign up for a Microsoft 365 Developer Administrator email address, if you don’t have one:

1.  Go to the [Microsoft Dev Center](https://developer.microsoft.com/en-us/microsoft-365/dev-program){: external}.

1.  Click **Join now** to become a member of the Microsoft 365 Developer program.

1.  On the Dashboard, click **Set up E5 subscription**, and select an **Instant** or a **Configurable** sandbox.

1. Copy the email address listed under **Administrator**. Your admin credentials will be required at several points of setup.

## Adding the Microsoft Teams integration
{: #deploy-microsoft-teams-setup}

1. Go to the **Integrations** page by clicking the integrations icon (![Integrations icon](images/integrations-icon.png)) in the left menu.

1. Click **Add** on the **Microsoft Teams** tile.

1. Click **Confirm**. The **Get Started** page provides a summary of the setup process.

1. Click **Next** to begin app registration.

### App registration 
{: #deploy-microsoft-teams-reg}

1. Go to the [Microsoft Azure portal](https://portal.azure.com/){: external}, and log in with your admin credentials.

1. On the **App registrations** page, click **New registration**. 

1. To **Register an application**, enter a **Name**, select the **Multitenant** option that applies to your application, then click **Register**.

1. Copy the **Application (client) ID** from your app **Overview** page and paste into **App registration** of your {site.data.keyword.conversationshort} Microsoft Teams integration.

1. On the same Microsoft Azure **Overview** page, click the hyperlink **Add a certificate or secret** next to Client Credentials. 

1. On the **Certificates & secrets** page for token creation, click **New client secret**. Enter a **description** and select **Recommended 180 days** from the dropdown, then **Add**.

1. Copy the string under **Value** and paste into **Client secret value** on the **App registration** page of your {site.data.keyword.conversationshort} Microsoft Teams integration. Note: You *must* generate a new value before the current one expires on day 180.

1. Click **Next** to create your bot.

### Create your bot
{: #deploy-microsoft-teams-bot}

1. Go to the [Microsoft Bot Framework developer portal](https://dev.botframework.com/bots/new){: external}, and log in with your admin credentials.

1. On the **Tell us about your bot** page, complete your bot profile. 

1. Copy the generated endpoint from the **Create your bot** page of your {site.data.keyword.conversationshort} Microsoft Teams integration and paste into the **Messaging endpoint** field of **Configuration**.

1. Select **Multi-Tenant** as app type from the dropdown. 

1. Copy and paste your **Application (client) ID**, and then click **Register**.

1. To **Connect to channels** and **Add a featured channel**, click **Configure Microsoft Teams channel**. 

1. To **Configure Microsoft Teams**, select options under **Messaging**, **Calling**, and **Publish** that fit your bot needs, and then click **Save**.

1. In your {site.data.keyword.conversationshort} Microsoft Teams integration, click **Next** to create your Teams app.

### Create your Teams app
{: #deploy-microsoft-teams-app}

1. Go to the [Microsoft Teams Developer Portal](https://dev.teams.microsoft.com/home){: external}, and log in with your admin credentials.

1. On the **Apps** tab, click **New App**. 

1. In the **Add app** popup, enter **Name** and click **Add**. 

1. On the **Basic information** page, enter app names, app ID, descriptions, developer information, and app URLs, and then copy and paste the **Application (client) ID**. Click **Save**.

1. Go to **App features** in the **Configure** section, select the feature called **Bot**. 

1. To **Identify your bot**, **Select an existing bot** from the dropdown. 

1. Tick the boxes **Personal**, **Team**, and **Group Chat** to **Select the scope in which people can use this command**, then click **Save**. Keep open.

1. In your {site.data.keyword.conversationshort} Microsoft Teams integration, click **Finish**.

1. Click **Publish** in the upper-right corner to publish your bot. 

## Publishing your Teams app
{: #deploy-microsoft-teams-publish}

1. In the Microsoft Teams Developer Portal where you created and saved your Teams app, which should still be open, click **Publish** to publish your bot.

1. Click **Download the app package**.

1. Go to [Microsoft Teams](https://teams.microsoft.com){: external}, and log in with your admin credentials.

1. Click **Apps** in the sidebar menu, then **Manage your apps** and **Upload an app**. 

1. Select **Upload a custom app** in the popup, and upload the app package .zip file you downloaded. 

1. Click **Add** to finish.

1. Test your actions and response types in **Chat** of your Teams app.

## Response types
{: #deploy-microsoft-teams-response-types}

These [response types](docs/watson-assistant?topic=watson-assistant-respond) are supported and displayed as expected when your assistant is deployed for Microsoft Teams direct messages, channels, or group chats.

- date
- image
- options/suggestions
- text 