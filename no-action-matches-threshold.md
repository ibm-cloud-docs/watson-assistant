---

copyright:
  years: 2023
lastupdated: "2023-04-06"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Setting a threshold to trigger the "No action matches" system action
{: #no-action-matches-threshold}

Unrecognized input by customers triggers the [No action matches](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-handle-errors#no-action-matches) action that can be configured to fetch answers from a [search integration](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-search-add#search-no-action-matches) or trigger the [Fallback](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-handle-errors#fallback-action) action. 

For more information, see [When the assistant can't understand your customer's request](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-handle-errors#no-action-matches).

By setting this threshold, you can affect how often your assistant routes customers to the “No action matches” action.

Your assistant uses various thresholds for each of these settings when finding a matching action:

- Rarely (This is the default)
- Sometimes
- More often

To set the threshold:

1. On the **Actions** page, click **Global settings** ![Gear icon](../../icons/settings.svg).

1. On the **Action response modes** tab, use the **Use "No action matches"** section to choose a setting.
