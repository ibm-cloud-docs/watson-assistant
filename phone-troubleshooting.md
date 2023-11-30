---

copyright:
  years: 2022, 2023
lastupdated: "2023-11-30"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}


# Troubleshooting and Logs
{: #phone-troubleshooting}



## Troubleshooting
{: #phone-troubleshooting-tips}

Find solutions to problems that you might encounter when using the phone integration.

- A *Forbidden* message: The phone number that you specified when you configured the phone integration cannot be verified. Ensure that the number fully matches the SIP trunk phone number.

- A lot of latency between caller questions and Watson answers: Most likely coming from latency that is caused by one of the Watson services, you can [view logs in IBM Log Analysis](#phone-troubleshooting-logs). At the end of each call, you see a `CWSGW0160I: Call was ended.` event. Expand on this entry to see a summary of the `max_response_milliseconds` and details of the `assistant_interaction_summaries`, which helps you identify the service the latency is coming from.

  If your plan allows, you can also look at the Call Detail Record (CDR) to determine which service is misbehaving. For more information, see [Call Detail Records (CDRs)](#phone-troubleshooting-cdrs).

## Viewing logs
{: #phone-troubleshooting-logs}

The log events that occur in the components that are used by the phone integration are written to IBM Log Analysis. To check the logs, create an instance and configure the platform logs to observe the region where your service instance is hosted.

For more information about setting up an instance, see [Provisioning an instance](/docs/log-analysis?topic=log-analysis-provision){: external}.

Currently, the Phone and SMS integrations are the only components of your assistant that write logs to the IBM Log Analysis dashboard.
{: note}

After you create the instance, get log information by completing the following steps.

1.  Go to the [IBM Cloud Logging](/observe/logging){: external} page.
1.  Click **Options**, then choose **Edit platform**.
1.  Select the region and instance, and then click **Select**.
1.  To open the IBM Log Analysis console, click **Open Dashboard**.
1.  The source name of the log events is *Watson*.

    You can apply filters or search the logs by values such as a phone number or instance ID.

## Call Detail Records (CDRs)
{: #phone-troubleshooting-cdrs}

The phone integration can generate call detail record (CDR) events, which contain summary information about a single call. Call detail records are configured through a webhook. For more information, see [Logging activity with a webhook](/docs/watson-assistant?topic=watson-assistant-webhook-log#webhook-log).

For more information about the structure of the CDR event payload, see [CDR log event reference](/docs/watson-assistant?topic=watson-assistant-cdr-log-reference).

You can also inject custom data into the CDR event. For more information, see [Injecting custom values into CDR log events](/docs/watson-assistant?topic=watson-assistant-phone-actions#phone-actions-cdr-custom-data).

