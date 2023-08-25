---

copyright:
  years: 2022, 2023
lastupdated: "2023-08-25"

keywords: settings
subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Global settings for actions
{: #actions-global-settings}

Use **Global settings** to configure features across all actions.
{: shortdesc}

On the **Actions** page, click **Global settings** ![Gear icon](../../icons/settings.svg).

Global settings provide options, configurations, and tasks for:

- [Clarifying questions](#actions-global-settings-response-modes)
- [Change conversation topic](#actions-global-settings-change-conversation-topic)
- [Autocorrection](#actions-global-settings-autocorrection)
- [Display formats](#actions-global-settings-display-formats)
- [Algorithm version](#actions-global-settings-algorithms-versions)
- [Autolearning](#actions-global-settings-autolearning)
- [Upload/Download](#actions-global-settings-upload-download)

## Clarifying questions
{: #actions-global-settings-response-modes}

On the **Clarifying questions** tab, you can customize how an action asks clarifying questions.

In the **Ask clarifying questions** section, you can:
- Enable or disable if your assistant disambiguates (asks a clarifying question).
- Modify the text that your assistant uses to introduce the clarification list or when no action matches.
- Enable or disable response modes, and modify the text that your assistant uses with a response mode. If you enable response modes, you can use the **Customize modes** section to choose a response mode for each action to set how it behaves.

In the **No action matches** section, you can affect how often your assistant routes customers to the *No action matches* action when input is unrecognized.

For more information, see:
- [Customizing clarifying questions](/docs/watson-assistant?topic=watson-assistant-understand-questions#understand-questions-disambiguation-config)
- [Response modes](/docs/watson-assistant?topic=watson-assistant-action-response-modes)
- [When the assistant can't understand your customer's request](/docs/watson-assistant?topic=watson-assistant-handle-errors#no-action-matches)

## Change conversation topic
{: #actions-global-settings-change-conversation-topic}

The **Change conversation topic** feature enables your assistant to handle digressions, dynamically responding to the user by changing the conversation topic as needed. For more information, see [Allowing your customers to change the topic of the conversation](/docs/watson-assistant?topic=watson-assistant-change-topic).

If necessary, you can disable changing the topic for all actions:

1. On the **Change conversation topic** tab, set the switch to **Off**.

1. Click **Save**, and then click **Close**.

### Allow change of topic between actions and dialog
{: #actions-global-settings-change-topic-action-to-dialog}

If you are using actions and dialog, you can ensure that customers can change topics between an action and a dialog node.

This setting is available if you activate dialog in Assistant settings. For more information, see [Activating dialog and migrating skills](/docs/watson-assistant?topic=watson-assistant-activate-dialog).
{: note}

1. Set the toggle **Change topics from actions to dialog** to **On**.

1. Click **Save**, and then click **Close**.

## Confirmation to return to previous topic
{: #actions-global-settings-change-topic-confirmation}

By default, new assistants are set to ask a "yes or no" question to confirm that the customers want to return to the previous action. You can modify these settings in the Confirmation section. For more information, see [Confirmation to return to previous topic](/docs/watson-assistant?topic=watson-assistant-change-topic#change-topic-confirmation).

## Autocorrection
{: #actions-global-settings-autocorrection}

*Autocorrection* fixes misspellings that users make in their requests. The corrected words are used to match to an action. 

Autocorrection is enabled automatically for all English-language assistants. It is also available in French-language assistants, but is disabled by default. The autocorrection setting isn't available for any other languages.

For more information, see [Autocorrecting user input](/docs/watson-assistant?topic=watson-assistant-autocorrection).

## Display formats
{: #actions-global-settings-display-formats}

Use display formats for variables that use date, time, numbers, currency, or percentages. You can also choose a default locale to use if one isn't provided by the client application. You can ensure that the format of a variable in the web chat is what you want for your assistant. For example, you can choose to have the output of a time variable appear in HH:MM format instead of HH:MM:SS.

Variables are formatted by using a system default unless you specify otherwise.

| <nobr>Display format setting</nobr> | Description | <nobr>English - United States (en-US) examples</nobr> |
| ---- | ---- | ---- |
| Locale | Choose a default locale for the assistant if one can't be determined. The locale that you choose uses formats specific to that country and language. If you choose a locale, the date, time, number, currency, and percentage format fields change to show choices specific to that locale. The system default is `English - United States (en-US)`. | |
| Date | For calendar dates, choose short, medium, long, full, YY/MM/DD, or YYYY/MM/DD | <ul><li>Short: `1/31/23`</li><li>Medium: `Jan 31, 2023`<li>Long: `January 31, 2023`</li><li>Full: `Tuesday, January 31, 2023`</li></ul> |
| Time | For times, choose short or medium | <ul><li>Short: `1:53 PM`</li><li>Medium: `1:53:30 PM`</li></ul> |
| Number fraction digits | Use the system default (up to 14 digits) or two digits | `10.12` |
| Number delimiter | Use the system default, none, comma, or period | <ul><li>None: `2000.12`</li><li>Comma: `2,000.12`<li>Period: `2.000,12`</li></ul> |
| Currency fraction digits | Use the system default (up to 14 digits) or two digits | `10.99` |
| Currency symbol | Use the system default or choose a global symbol | `$10.99` |
| <nobr>Percentage fraction digits</nobr> | Use the system default (up to 14 digits) or two digits | `10.75%` |

## Autolearning
{: #actions-global-settings-autolearning}

**Autolearning** enables your assistant to learn from interactions with your customers and improve responses. For more information, see [Using autolearning to improve assistant responses](/docs/watson-assistant?topic=watson-assistant-autolearn).

## Algorithm version
{: #actions-global-settings-algorithms-versions}

Choose which {{site.data.keyword.conversationshort}} algorithm to apply to your future trainings. For more information, see [Algorithm version](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

## Upload/Download
{: #actions-global-settings-upload-download}

You can upload or download actions.

### Downloading
{: #actions-global-settings-download}

To back up actions, download a JSON file and store it. On the **Upload/Download** tab, click the **Download** button.

### Uploading
{: #actions-global-settings-upload}

To reinstate a backup copy of actions that you exported from another service instance or environment, import the JSON file of the actions you exported.

If the {{site.data.keyword.conversationshort}} service changes between the time you export the actions and import it, due to functional updates that are regularly applied to instances in cloud-hosted continuous delivery environments, your imported actions might function differently than before.
{: important}

On the **Upload/Download** tab, drag a JSON file onto the tab or click to select a file from your local system, then click **Upload**.

The imported JSON file must use UTF-8 encoding, without byte order mark (BOM) encoding. The JSON file cannot contain tabs, newlines, or carriage returns.
{: important}
