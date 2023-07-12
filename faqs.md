---

copyright:
  years: 2015, 2023
lastupdated: "2023-07-12"

keywords: Watson Assistant frequently asked questions

subcollection: watson-assistant

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# FAQs for {{site.data.keyword.conversationfull}}
{: #watson-assistant-faqs}

Find answers to frequently-asked questions and quick fixes for common problems.
{: shortdesc}

## FAQs about the new {{site.data.keyword.conversationfull}} experience
{: #faqs-new-experience}
{: faq}

### What is the new {{site.data.keyword.conversationfull}} experience?
{: faq-what-is-the-new-experience}
{: faq}

The new {{site.data.keyword.conversationshort}} is an improved way to build, publish, and improve virtual assistants. In the new experience, you use actions to build conversations. Actions are a simple way for anyone to create assistants. For more information, see the [Getting Started guide](https://www.ibm.com/blogs/watson/2021/12/getting-started-with-the-new-watson-assistant-part-i-the-build-guide/){: external} or the [documentation](/docs/watson-assistant) for the new experience.

### Why can't I see the assistants that I made with classic {{site.data.keyword.conversationshort}} in the new experience?
{: #faq-classic-assistants}
{: faq}

The new {{site.data.keyword.conversationshort}} is a clean slate in the same IBM Cloud instance as your classic experience. Assistants that you created in one experience don't appear in the other. However, you can switch back and forth between experiences without losing any work. For more information, see [Switching the experience](/docs/watson-assistant?topic=watson-assistant-welcome-new-assistant#welcome-new-assistant-switch-experience).

### What happens when I switch between the classic and new {{site.data.keyword.conversationshort}} experiences?
{: #faq-switching}
{: faq}

The assistants that you create in one experience don't transfer to the other. However, you can switch experiences, return to your work, and create or use assistants. You don't lose anything by switching. Changing experiences doesn't affect other users in the same instance. For more information, see [Switching the experience](/docs/watson-assistant?topic=watson-assistant-welcome-new-assistant#welcome-new-assistant-switch-experience).

### Is the classic {{site.data.keyword.conversationshort}} experience going away?
{: #faq-classic-lifecycle}
{: faq}

IBM has no plans to discontinue the classic {{site.data.keyword.conversationshort}} experience. However, we encourage you to explore the benefits and capabilities in the new {{site.data.keyword.conversationshort}}. For more information, see the [Getting Started guide](https://www.ibm.com/blogs/watson/2021/12/getting-started-with-the-new-watson-assistant-part-i-the-build-guide/){: external} or the [documentation](/docs/watson-assistant) for the new experience.

### Where are the search skill and channel integrations in the new {{site.data.keyword.conversationshort}} experience? 
{: #faq-integrations}
{: faq}

In the left navigation, click **Integrations** ![Integrations](images/integrations-icon.png). On the Integrations page, you can add search, channel, and extension integrations to your assistant. For more information, see [Adding integrations](/docs/watson-assistant?topic=watson-assistant-deploy-integration-add).

### Where is the Assistant ID found in the new product experience?
{: #faq-assistant-id}
{: faq}

The assistant ID can be found in **Assistant settings**.

In **Assistant settings**, the assistant ID is in the **Assistant IDs and API details** section.

## What do the draft and live tags mean?
{: #faqs-draft-live-tags}
{: faq}

A `Draft` tag indicates that the information is linked to your draft environment, which means that you can preview these updates but they are not visible to your users. A `Live` tag indicates that the information is linked to your live environment, which means that the content is available to your users to interact with.

For more information, see [Environments](/docs/watson-assistant?topic=watson-assistant-publish-overview#environments).

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

- The Lite plan that you were using expired. Lite plans expire if they are not used within a 30-day span. To begin again, log in to IBM Cloud and create a new service instance of {{site.data.keyword.conversationshort}}.
- An instance is locked when you exceed the plan limits for the month. To log in successfully, wait until the start of the next month when the plan limit totals are reset.

## Why don't I see the Analytics page?
{: #faqs-view-analytics}
{: faq}

To view the **Analytics** page, you must have a service role of Manager and a platform role of at least Viewer. For more information about access roles and how to request an access role change, see [Managing access to resources](/docs/watson-assistant?topic=watson-assistant-access-control).

## Why am I unable to view the API details, API key, or service credentials?
{: #faqs-view-api-details}
{: faq}

If you cannot view the API details or service credentials, it is likely that you do not have Manager access to the service instance in which the resource was created. Only people with Manager access to the instance can use the service credentials.

## Can I export the user conversations from the Analytics page?
{: #faqs-export-conversation}
{: faq}

You cannot directly export conversations from the conversation page. However, you can use the `/logs` API to list events from the transcripts of conversations that occurred between your users and your assistant. For more information, see the [V2 API reference](https://cloud.ibm.com/apidocs/assistant/assistant-v2#listlogs){: external}. Or, you can use a Python script to export logs. For more information, see [export_logs_py](https://github.com/watson-developer-cloud/community/blob/master/watson-assistant/export_logs_py.py).

## Can I change my plan to a Lite plan?
{: #faqs-downgrade-plan}
{: faq}

No, you cannot change from a Trial, Plus, or Standard plan to a Lite plan. And you cannot upgrade from a Trial to a Standard plan.

## How many Lite plan instances of {{site.data.keyword.conversationshort}} can I create?
{: #faqs-lite-plans}
{: faq}

You can have only one Lite plan instance of {{site.data.keyword.conversationshort}} per resource group.

## How do I create a webhook?
{: #faqs-webhook-how}
{: faq}

To define a webhook and add its details, go to the **Live environment** page and open the **Environment settings** page. From the **Environment settings** page, click **Webhooks > Pre-message webhook**. You can add details about your webhook. For more information, see [Making a call before processing a message](/docs/watson-assistant?topic=watson-assistant-webhook-pre).

## Can I have more than one entry in the URL field for a webhook?
{: #faqs-webhook-url}
{: faq}

No, you can define only one webhook URL for an action. For more information, see [Defining the webhook](/docs/watson-assistant?topic=watson-assistant-webhook-pre#webhook-pre-create).

## Is there a range of IP addresses that are being used by a webhook?
{: #faqs-webhook-ip}
{: faq}

Unfortunately, the IP address ranges from which {{site.data.keyword.conversationshort}} might call a webhook URL are subject to change, which in turn prevent using them in any static firewall configuration.  Use the https transport and specify an authorization header to control access to the webhook.

## What do I do if the training process seems stuck?
{: #faqs-stuck-training}
{: faq}

If the training process gets stuck, first check whether for an outage for the service by going to the [Cloud status page](https://cloud.ibm.com/status){: external}. You can start a new training process to stop the current process and start over.

## How do I see my monthly active users in {{site.data.keyword.conversationshort}}?
{: #faqs-see-mau}
{: faq}

To see your monthly active users (MAU):
1.  Sign in to https://cloud.ibm.com
1.  Click the **Manage** menu, then choose **Billing and usage**.
1.  Click **Usage**.
1.  For {{site.data.keyword.conversationshort}}, select **View Plans**.
1.  Under **Time Frame**, select the month that you need.
1.  Select your Plus plans or Plus Trial plans to see monthly active users and the API calls.

## Can I see what web browser users are using with {{site.data.keyword.conversationshort}}?
{: #faqs-user-browser}
{: faq}

With the V2 API and an Enterprise plan, you can use the Segment extension to see what browser was used to send the message. For more information, see [Sending events to Segment](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-segment-add).

## Is it possible to increase the number of intents per skill
{: #faqs-intents-number}
{: faq}

No, it is not possible to increase the number of intents per skill.
