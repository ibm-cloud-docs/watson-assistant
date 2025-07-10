---

copyright:
  years: 2019, 2025
lastupdated: "2025-07-10"

keywords: post webhook, postwebhook, post-webhook

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Making a call after processing a message
{: #webhook-post}

A post-message webhook calls an external service or application every time that the assistant renders a response. The external service can process the assistant's output before it is sent to the channel.
{: shortdesc}

You can add a post-message webhook to your assistant if you want to trigger the webhook before each message response is shown to the customer.

You can use a post-message webhook to do things like extract custom responses from an external content repository. For example, you can define actions with custom IDs in the responses instead of text. The post-message webhook can pass these IDs to an external database to retrieve stored text responses.

You can use this webhook in coordination with the pre-message webhook. For example, if you use the pre-message webhook to strip personally identifiable information from the customer's input, you can use the post-message webhook to add it back. If you use the pre-message webhook to translate the customer's input to the assistant's language, you can use the post-message webhook to translate the response into the customer's language before returning it. For more information, see [Making a call before processing a message](/docs/watson-assistant?topic=watson-assistant-webhook-pre).

For environments where private endpoints are in use, keep in mind that a webhook sends traffic over the internet.
{: note}

## Defining the webhook
{: #webhook-post-create}

You can define one webhook URL to use for processing every message response before it is sent to the channel and shown to the customer.

## Before you begin

The programmatic call to the external service must meet these requirements:

- Do not set up and test your webhook in a production environment where the assistant is deployed and is interacting with customers.
- The call must be a POST HTTP request.
- The call must be completed in 30 seconds or less.
- The format of the request and response must be in JSON. For example, `Content-Type: application/json`.

Use a dialog webhook if you need to perform a one-time action when needed during a conversation. For example, conditions are met when the assistant collects all required details, such as the account number, user ID, and account secret. For more information, see [Making a programmatic call from dialog](/docs/watson-assistant?topic=watson-assistant-dialog-webhooks#dialog-webhooks).
{: note}

## Choosing your deployment method

Select the deployment method that you use to view the correct steps for setting a post-message webhook.

To identify which deployment type you are using, click the **Manage** menu ![Manage menu](images/user--avatar.svg). If you see **Switch to classic experience**, you are using the **new experience**. If you see **Switch to new experience**, you are using the **classic experience**.


Use the following links to know about the procedures based on your deployment type:

 - [**{{site.data.keyword.cpd_full_notm}}**](/docs/watson-assistant?topic=watson-assistant-webhook-post-cp4d#post-procedure-cp4d)

 - [**{{site.data.keyword.cpd_full_notm}} - classic experience**](/docs/watson-assistant?topic=watson-assistant-webhook-post-cp4d-classic#post-procedure-cp4d-classic)

 - [**{{site.data.keyword.conversationshort}}**](/docs/watson-assistant?topic=watson-assistant-webhook-post-watson-assistant#post-procedure-watson-assistant)

 - [**{{site.data.keyword.conversationshort}} - classic experience**](/docs/watson-assistant?topic=watson-assistant-webhook-post-watson-assistant-classic#post-procedure-watson-assistant-classic)
