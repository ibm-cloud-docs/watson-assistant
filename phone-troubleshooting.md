---

copyright:
  years: 2022, 2025
lastupdated: "2025-05-26"

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

Log events from the components used by the phone integration are written to IBM Cloud Logs. To view these logs, create an instance and configure platform logs to monitor the region where your service instance is hosted.

For instructions on setting up an instance, see [Provisioning an instance](https://cloud.ibm.com/docs/cloud-logs?topic=cloud-logs-instance-provision&interface=ui).

Currently, only the Phone and SMS integrations write logs to the IBM Cloud Logs dashboard.{: note}

Once the instance is created, follow these steps to access log information:

1. Go to the [IBM Cloud Logging](https://cloud.ibm.com/observe/logging) page.

1. Select the Logging instance to use.

1. From the panel, choose **Getting Started**.

1. Click **Add Data Sources** > **Configure Platform Logs**.

1. Set the target region for log viewing, select the IBM Cloud Logs instance, and click **Save**.

1. To open the IBM Cloud Logs console, return to the [IBM Cloud Logging](https://cloud.ibm.com/observe/logging) page, and click **Dashboard**.

1. From the menu, select **Explore Logs**.

You can apply filters or search the logs by values such as phone number or instance ID.

## Call Detail Records (CDRs)
{: #phone-troubleshooting-cdrs}

The phone integration can generate call detail record (CDR) events, which contain summary information about a single call. Call detail records are configured through a webhook. For more information, see [Logging activity with a webhook](/docs/watson-assistant?topic=watson-assistant-webhook-log#webhook-log).

For more information about the structure of the CDR event payload, see [CDR log event reference](/docs/watson-assistant?topic=watson-assistant-cdr-log-reference).

You can also inject custom data into the CDR event. For more information, see [Injecting custom values into CDR log events](/docs/watson-assistant?topic=watson-assistant-phone-actions#phone-actions-cdr-custom-data).
