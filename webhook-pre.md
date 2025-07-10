---

copyright:
  years: 2019, 2025
lastupdated: "2025-07-10"

keywords: pre webhook, prewebhook, pre-webhook

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Making a call before processing a message
{: #webhook-pre}

A pre-message webhook makes a call to an external service or application every time a customer submits input. The external service can process the message before your assistant processes it.
{: shortdesc}

Add a pre-message webhook to your assistant if you want the webhook to be triggered before each incoming message is processed by your assistant.

If you are using a custom channel, the pre-message webhook works with the version 2 of the `/message` API only, stateless and stateful. For more information, see the [API reference](https://cloud.ibm.com/apidocs/assistant-v2#message). All built-in channel integrations use this API.
{: important}

You can use pre-message webhooks for the following use cases:

- Translate the customer's input to the language that your assistant uses.

- Check for and remove any personally identifiable information, such as an email address or social security number that a customer might submit.

You can use this webhook in coordination with the post-message webhook. For example, the post-message webhook can do things like translate the response back into the customer's language or add back information that was removed for privacy reasons. For more information, see [Making a call after processing a message](/docs/watson-assistant?topic=watson-assistant-webhook-post).

For environments where private endpoints are in use, keep in mind that a webhook sends traffic over the internet.{: note}

Use a dialog webhook if you need to perform a one-time action when needed during a conversation. For example, conditions are met when the assistant collects all required details, such as the account number, user ID, and account secret. For more information, see [Making a programmatic call from dialog](/docs/watson-assistant?topic=watson-assistant-dialog-webhooks#dialog-webhooks).

## Defining the webhook
{: #webhook-pre-create}

You can define one webhook URL to use for preprocessing every incoming message.

## Before you begin

The programmatic call to the external service must meet the following requirements:

- Do not set up and test your webhook in a production environment where the assistant is deployed and is interacting with customers.
- The call must be a POST HTTP request.
- The request body must be a JSON object (`Content-Type: application/json`).
- The call must return in 30 seconds or less.

If your external service supports GET requests only, or if you need to specify URL parameters dynamically at run time, consider creating an intermediate service that accepts a POST request with a JSON payload that contains any runtime values. The intermediate service can then make a request to the target service, passing these values as URL parameters, and then return the response to the dialog.
{: note}

## Choosing your deployment method

Select the deployment method that you use to view the correct steps for setting a pre-message webhook.

To identify which deployment type you are using, click the **Manage** menu ![Manage menu](images/user--avatar.svg). If you see **Switch to classic experience**, you are using the **new experience**. If you see **Switch to new experience**, you are using the **classic experience**.

Use the following links to know about the procedures based on your deployment type:

 - [**{{site.data.keyword.cpd_full_notm}}**](/docs/watson-assistant?topic=watson-assistant-webhook-pre-cp4d#pre-procedure-cp4d)

 - [**{{site.data.keyword.cpd_full_notm}} - classic experience**](/docs/watson-assistant?topic=watson-assistant-webhook-pre-cp4d-classic#pre-procedure-cp4d-classic)

 - [**{{site.data.keyword.conversationshort}}**](/docs/watson-assistant?topic=watson-assistant-webhook-pre-watson-assistant#pre-procedure-watson-assistant)

 - [**{{site.data.keyword.conversationshort}} - classic experience**](/docs/watson-assistant?topic=watson-assistant-webhook-pre-watson-assistant-classic#pre-procedure-watson-assistant-classic)
