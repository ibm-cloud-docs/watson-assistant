---

copyright:
  years: 2022
lastupdated: "2022-09-20"

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

{{site.data.content.classiclink}}

# Troubleshooting and Viewing Logs
{: #phone-troubleshooting}

## Troubleshooting
{: #phone-troubleshooting-tips}

Find solutions to problems that you might encounter while using the integration.

- If you get a *Forbidden* message, it means the phone number that you specified when you configured the integration cannot be verified. Make sure the number fully matches the SIP trunk phone number.

## Viewing logs
{: #phone-troubleshooting-logs}

The log events that occur in the components that are used by the phone integration are written to IBM Log Analysis. To check the logs, create an instance and configure the platform logs to observe the region where your service instance is hosted.

For more information about setting up an instance, see [Provisioning an instance](/docs/log-analysis?topic=log-analysis-provision){: external}.

Currently, the Phone and SMS integrations are the only components of your assistant that write logs to the IBM Log Analysis dashboard.
{: note}

After you create the instance, get log information by completing the following steps:

1.  Go to the [IBM Cloud Logging](https://cloud.ibm.com/observe/logging){: external} page.
1.  Click **Options**, then choose **Edit platform**.
1.  Select the region and instance, and then click **Select**.
1.  To open the IBM Log Analysis console, click **Open Dashboard**.
1.  The source name of the log events is *Watson*.

    You can apply filters or search the logs by values such as a phone number or instance ID.
