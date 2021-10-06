---

copyright:
  years: 2015, 2021
lastupdated: "2021-10-04"

keywords: Watson Assistant frequently asked questions

subcollection: watson-assistant

content-type: faq

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
{:faq: data-hd-content-type='faq'}

{{site.data.content.classiclink}}

# FAQs for Watson Assistant
{: #watson-assistant-faqs}

Find answers to frequently-asked questions and quick fixes for common problems.
{: shortdesc}

## What do the draft and live tags mean?
{: #faqs-draft-live-tags}
{: faq}

A `Draft` tag indicates that the information is linked to your draft environment, which means that you can preview these updates but they are not visible to your users. For more information about the draft environment, see [Previewing and sharing your assistant](/docs/watson-assistant?topic=watson-assistant-preview-share). A `Live` tag indicates that the information is linked to your live environment, which means that the content is available to your users to interact with. For more information about publishing to your live environment, see [Managing the live environment](/docs/watson-assistant?topic=watson-assistant-publish#managing-the-live-environment).

## Why can't I log in?
{: #faqs-cannot-login}
{: faq}

If you are having trouble logging in to a service instance or see messages about tokens, such as `unable to fetch access token` or `400 bad request - header or cookie too large`, it might mean that you need to clear your browser cache. Open a private browser window, and then try again.

- If accessing the page by using a private browsing window fixes the issue, then consider always using a private window or clear the cache of your browser. You can typically find an option for clearing the cache or deleting cookies in the browser's privacy and security settings.
- If accessing the page by using a private browsing window doesn't fix the issue, then try deleting the API key for the instance and creating a new one.

## Why am I being asked to log in repeatedly?
{: #faqs-login-repeatedly}
{: faq}

If you keep getting messages, such as `you are getting redirected to login`, it might be due to one of the following things:

- The Lite plan you were using has expired. Lite plans expire if they are not used within a 30-day span. To begin again, log in to IBM Cloud and create a new service instance of Watson Assistant.
- An instance is locked when you exceed the plan limits for the month. To log in successfully, wait until the start of the next month when the plan limit totals are reset.

## Why don't I see the **Analytics** page?
{: #faqs-view-analytics}
{: faq}

To view the **Analytics** page, you must have a service role of Manager and a platform role of at least Viewer. For more information about access roles and how to request an access role change, see [Managing access to resources](/docs/watson-assistant?topic=watson-assistant-access-control).

## Why am I unable to view the API details, API key, or service credentials?
{: #faqs-view-api-details}
{: faq}

If you cannot view the API details or service credentials, it is likely that you do not have Manager access to the service instance in which the resource was created. Only people with Manager access to the instance can use the service credentials.
<!--- For more information, see [Getting API information](/docs/assistant?topic=assistant-assistant-settings#assistant-settings-api-details). --->

<!--- ## Where can I find an example for creating my first assistant?
{: #faqs-get-started}
{: faq}

Follow the steps in the [Getting started with {{site.data.keyword.conversationshort}}](/docs/assistant?topic=assistant-getting-started) tutorial for a product introduction and to get help creating your first assistant. --->

## Can I export the user conversations from the **Analytics** page?
{: #faqs-export-conversation}
{: faq}

You cannot directly export conversations from the conversation page. You can, however, use the `/logs` API to list events from the transcripts of conversations that occurred between your users and your assistant. For more information, see the [API reference](https://cloud.ibm.com/apidocs/assistant/assistant-v2#listlogs){: external}.

## Can I change my plan to a Lite plan?
{: #faqs-downgrade-plan}
{: faq}

No, you cannot change from a Trial, Plus, or Standard plan to a Lite plan. And you cannot upgrade from a Trial to a Standard plan.
<!--- For more information, see [Upgrading](/docs/assistant?topic=assistant-upgrade). --->

<!--- ## How long are log files kept for a workspace?
{: #faqs-assistant-logs}
{: faq}

The length of time for which messages are retained depends on your service plan. For more information, see [Log limits](/docs/assistant?topic=assistant-logs#logs-limits). --->

## How do I create a webhook?
{: #faqs-webhook-how}
{: faq}

To define a webhook and add its details, go to the **Connect** page and open the **Environment settings** page. From the **Environment settings** page, click **Webhooks > Pre-message webhook**. From this page, you can add details about your webhook. For more information, see [Making a call before processing a message](/docs/watson-assistant?topic=watson-assistant-webhook-pre).

## Can I have more than one entry in the URL field for a webhook?
{: #faqs-webhook-url}
{: faq}

No, you can define only one webhook URL for an action. For more information, see [Defining the webhook](/docs/watson-assistant?topic=watson-assistant-webhook-pre#webhook-pre-create).

<!--- ## Can I extend the webhook time limit?
{: #faqs-webhook-timeout}
{: faq}

No. The service that you call from the webhook must return a response in 8 seconds or less, or the call is canceled. You cannot increase this time limit. For more information about strategies for handling complex actions with a webhook, watch the video in [Making a programmatic call from dialog](/docs/assistant?topic=assistant-dialog-webhooks). --->

## Is there a range of IP addresses that are being used by a webhook?
{: #faqs-webhook-ip}
{: faq}

Unfortunately, the IP address ranges from which Watson Assistant may call a webhook URL are subject to change, which in turn prevent using them in any static firewall configuration. Please use the https transport and specify an authorization header to control access to the webhook.

## What do I do if the training process seems stuck?
{: #faqs-stuck-training}
{: faq}

If the training process gets stuck, first check whether there is an outage for the service by going to the [Cloud status page](https://cloud.ibm.com/status){: external}. You can start a new training process to stop the current process and start over.

## How do I see my monthly active users in Watson Assistant?
{: #faqs-see-mau}
{: faq}

To see your monthly active users (MAU) do the following:
1.  Sign in to https://cloud.ibm.com
1.  Click on the **Manage** menu, then choose **Billing and usage**.
1.  Click on **Usage**.
1.  For Watson Assistant, select **View Plans**.
1.  Under Time Frame, select the month you need.
1.  Select your Plus plans or Plus Trial plans to see monthly active users and the API calls.
