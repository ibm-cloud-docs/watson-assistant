---

copyright:
  years: 2019, 2025
lastupdated: "2025-04-07"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Defining the authentication method for pre-message and post-message webhooks
{: #define-webhook-auth}

This document shows the process for configuring authentication for pre-message webhooks and post-message webhooks in {{site.data.keyword.conversationshort}}. It covers the available authentication methods and how to set them up.

## Overview
{: #webhook-overview}

Webhooks allow external systems to communicate with {{site.data.keyword.conversationshort}}. Authentication ensures that only authorized sources can trigger webhooks. This documentation describes the process for configuring and managing webhook authentication, which introduces an updated method for authenticating webhooks.


## Before you begin
{: #webhook-before-you-begin}


Before you configure the webhook authentication:

- You must have write permissions in the environment.
- You must have authentication details of the target server, including token request URLs (if needed) and any secrets, such as a password or token.

## Procedure
{: #webhook-procedure}

1. Go to **Home** > **Environments**.

1. Select **Settings** ![Gear icon](images/gear-icon-black.png) from either the **Draft** tab > **Draft environment** or the **Live** tab > **Live environment**.

1. Select from either **Pre-message webhook** or **Post-message webhook**, according to what you want to define.

1. Scroll down to **Webhook setup**, and paste the API URL.

1. Click **Edit authentication** to open the **Authentication set up** page.

1. In the dropdown, choose one of the following options:
    * [No authentication](#no-authentication)
    * [Basic auth](#basic-auth)
    * [Bearer auth](#bearer-auth)
    * [API key auth](#api-key-auth)
    * [OAuth 2.0](#oauth-20)

1. Click **Save**.

### No authentication
{: #no-authentication}

This is the default option.

### Basic auth
{: #basic-auth}

1. Enter a username and password.

### Bearer auth
{: #bearer-auth}

1. Enter the bearer token.

### API key auth
{: api-key-auth}

1. Enter the **API key name** and **API key**.

### OAuth 2.0
{: #oauth-20}

If you use the **Scope string**, it must be a space-delimited set of one or more authentication scopes defined by the target server. For example, write, read+write, email-read, and so on.
{: note}

1. In **Grant type**, choose one of the following options:
    * [Password](#password)
    * [Client credentials](#client-credentials)
    * [Authorization code](#authorization-code)
    * [Custom](#custom)

1. Click **Save**.

## Password
{: password}

1. Enter the **Username** of your webhook.

1. Enter the **Password** for your webhook service.

1. Enter the **Client ID** for your webhook authentication service.

1. Enter the **Client secret** to authenticate your webhook.

1. Enter the **Token URL**.

1. Enter the **Refresh token URL**.

1. **Optional:** If your service needs a scope string, enter the **Scope string** as defined by the target server.

1. In **Client authentication**, you must choose one of the following options:

    * **Send as Basic Auth header:** Authentication credentials will be sent in the HTTP header.
    * **Send as Body:** Authentication credentials will be sent in the request body.

1. Enter the **Header prefix**, for example: Bearer.

## Client credentials
{: client-credentials}

1. Enter the **Client ID** for your webhook authentication service.

1. Enter the **Client secret** to authenticate your webhook.

1. Enter the **Token URL**.

1. Enter the **Refresh token URL**.

1. **Optional:** If your service needs a scope string, enter the **Scope string** as defined by the target server.

1. In **Client authentication**, you must choose one of the following options:

    * **Send as Basic Auth header:** Authentication credentials will be sent in the HTTP header.
    * **Send as Body:** Authentication credentials will be sent in the request body.

1. Enter the **Header prefix**, for example: Bearer.

## Authorization code
{: authorization-code}

1. Enter the **Client ID** for your webhook authentication service.

1. Enter the **Authorizing server URL**.

1. Enter the **Token URL**.

1. Enter the **Refresh token URL**.

1. **Optional:** If your service needs a scope string, enter the **Scope string** as defined by the target server.

1. In **Client authentication**, you must choose one of the following options:

    * **Send as Basic Auth header:** Authentication credentials will be sent in the HTTP header.
    * **Send as Body:** Authentication credentials will be sent in the request body.

1. Enter the **Header prefix**, for example: Bearer.

1. **Optional:** Depending on the target server, copy the Redirect url to your OAuth app's 'Callback URL' field.

1. Click **Grant Access**.

1. Complete the steps on the page that presents by the granting server.

1. You are redirected back to the Assistant, and the edit modal re-opens.

1. Enter the **Client secret** under **Client ID** now that the field is visible.

## Custom
{: custom}

1. Enter the **Custom grant type name** of your webhook.

1. Enter the **Token URL**.

1. Enter the **Refresh token URL**.

1. **Optional:** If your service needs a scope string, enter the **Scope string** as defined by the target server.

1. In **Client authentication**, you must choose one of the following options:

    * **Send as Basic Auth header:** Authentication credentials will be sent in the HTTP header.
    * **Send as Body:** Authentication credentials will be sent in the request body.

1. Enter the **Header prefix**, for example: Bearer.

If you need to add custom secrets to your application, follow these steps:

1. Click **Add secret +**.

1. Type the **Secret name** and the **Secret value**.

1. **Optional:** If you want to add more secret names and secret values, click **Add secret +**.

1. Click **Add parameter +**.

1. Type the **Parameter name**, and the **Parameter value**.

1. **Optional:** If you want to add more parameter names and parameter values, click **Add parameter +**.
