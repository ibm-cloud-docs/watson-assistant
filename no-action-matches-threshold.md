---

copyright:
  years: 2023
lastupdated: "2023-03-30"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Setting a threshold to trigger the "No action matches" system action
{: #no-action-matches-threshold}

Unrecognized input by customers triggers the *No action matches* action that can be configured to fetch answers from a search integration or trigger the *Fallback* action. 

For more information, see [When the assistant can't understand your customer's request](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-handle-errors#no-action-matches).

By setting this threshold, you can affect how often your assistant routes customers to the “No action matches” action.

There are three settings:

| Setting | Description |
| --- | --- |
| Rarely | This is the default. Triggers only when confidence scores for matching actions are low. |
| Sometimes | Triggers when confidence scores are higher but not a strong match. |
| More often | Triggers even when confidence scores are closer to a match. |
{: caption="Settings" caption-side="top"}

To set the threshold:

1. From the **Actions** page of the assistant, click **Global settings** ![Gear icon](../../icons/settings.svg).

1. On the **Action response modes** tab, use the **Use "No action matches"** section to choose a setting.

