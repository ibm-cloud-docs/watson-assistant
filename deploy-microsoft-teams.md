---

copyright:
  years: 2024
lastupdated: "2024-12-23"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Integrating with Microsoft Teams
{: #deploy-microsoft-teams}

[IBM Cloud]{: tag-ibm-cloud}

Add a chatbot to Microsoft Teams to create and customize a productive hub where content, tools, and people come together to chat, meet, and collaborate. 
{: shortdesc}

After you [create an action](/docs/watson-assistant?topic=watson-assistant-build-actions-overview), you can use this integration to connect your assistant with Microsoft Teams.

## Before you begin
{: #deploy-microsoft-teams-account}

To integrate your assistant with Microsoft Teams, you must have the `Global Administrator`, or `Teams Administrator` roles. For more information, see [App permission policies](https://learn.microsoft.com/en-us/microsoftteams/teams-app-permission-policies){: external}.

Sign up for a Microsoft 365 Developer Administrator email address, if you don’t have one:

1.  Go to the [Microsoft Dev Center](https://developer.microsoft.com/en-us/microsoft-365/dev-program){: external}.

1.  Click **Join now** to become a member of the Microsoft 365 Developer program.

1.  On the Dashboard, click **Set up E5 subscription**, and select an **Instant** or a **Configurable** sandbox.

1. Copy the email address listed under **Administrator**. Your admin credentials are required at several points of setup.

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

1. On the **Register an application** page, enter a name, select the multi-tenant option that applies to your app, and then click **Register**.

1. Copy the application ID from the **Overview** page of your app, and paste it into the **App registration** field of your {{site.data.keyword.conversationshort}} Microsoft Teams integration.

1. On the same Microsoft Azure **Overview** page, click the hyperlink **Add a certificate or secret** next to Client Credentials. 

1. On the **Certificates & secrets** page for token creation, click **New client secret**. Enter a description and then select **Recommended 180 days**. Click **Add**.

1. Copy the string under **Value** and paste into **Client secret value** on the **App registration** page of your {{site.data.keyword.conversationshort}} Microsoft Teams integration. Note: You *must* generate a new value before the current one expires on day 180.

1. Click **Next** to create your bot.

### Create your bot
{: #deploy-microsoft-teams-bot}

1. Go to the [Microsoft Bot Framework developer portal](https://dev.botframework.com/bots/new){: external}, and log in with your admin credentials.

1. On the **Tell us about your bot** page, complete your bot profile. 

1. Copy the generated endpoint from the **Create your bot** page of your {{site.data.keyword.conversationshort}} Microsoft Teams integration and paste into the **Messaging endpoint** field of the **Configuration** section.

1. Select **Multi-Tenant** as the app type. 

1. Copy and paste your app ID, and then click **Register**.

1. On the **Connect to channels** page, click **Configure Microsoft Teams channel** in the **Add a featured channel** section.

1. On the **Configure Microsoft Teams** page, specify options in the **Messaging**, **Calling**, and **Publish** tabs that fit your bot needs, and then click **Save**.

1. In your {{site.data.keyword.conversationshort}} Microsoft Teams integration, click **Next** to create your Teams app.

### Create your Teams app
{: #deploy-microsoft-teams-app}

1. Go to the [Microsoft Teams Developer Portal](https://dev.teams.microsoft.com/home){: external}, and log in with your admin credentials.

1. On the **Apps** tab, click **New App**. 

1. Enter a name, and click **Add**. 

1. On the **Basic information** page, enter app names, app ID, descriptions, developer information, and app URLs, and then copy and paste your app ID into **Application (client) ID**. Click **Save**.

1. In the **Configure** section, select **App features**, and then **Bot**. 

1. On the **Identify your bot** page, select your bot. 

1. In the **Select the scope in which people can use this command** section, select **Personal**, **Team**, and **Group Chat**.

1. Click **Save**, but keep the window open.

1. In your {{site.data.keyword.conversationshort}}  Microsoft Teams integration, click **Finish**.

1. Click **Publish** to publish your bot. 

## Publishing your Teams app
{: #deploy-microsoft-teams-publish}

1. In the Microsoft Teams Developer Portal window where you created and saved your Teams app, click **Publish** to publish your bot.

1. Click **Download the app package**.

1. Go to [Microsoft Teams](https://teams.microsoft.com/v2/){: external}, and log in with your admin credentials.

1. Click **Apps** in the sidebar menu, and then click **Manage your apps** and **Upload an app**. 

1. Select **Upload a custom app** and specify the app package .zip file you downloaded. 

1. Click **Add** to finish.

1. Test your actions and responses in the **Chat** section of your Teams app.

## Response types
{: #deploy-microsoft-teams-response-types}

These [response types](/docs/watson-assistant?topic=watson-assistant-respond) are supported and displayed as expected when your assistant is deployed for Microsoft Teams direct messages, channels, or group chats.

- date
- image
- option
- suggestion
- text 
