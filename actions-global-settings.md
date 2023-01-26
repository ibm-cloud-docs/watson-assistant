---

copyright:
  years: 2022, 2023
lastupdated: "2023-01-27"
keywords: settings
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

# Global settings for actions
{: #actions-global-settings}

Use **Global settings** to configure features across all actions.
{: shortdesc}

On the **Actions** page, click **Global settings** ![Gear icon](images/gear-icon-black.png).

This page provides options, configurations, and tasks for the following:

- [Ask clarifying question](#actions-global-settings-ask-clarifying-question)
- [Change conversation topic](#actions-global-settings-change-conversation-topic)
- [Autocorrection](#actions-global-settings-autocorrection)
- [Display formats](#actions-global-settings-display-formats)
- [Algorithm version](#actions-global-settings-algorithms-versions)
- [Auto-save](#actions-global-settings-auto-save)
- [Upload/Download](#actions-global-settings-upload-download)

## Ask clarifying question
{: #actions-global-settings-ask-clarifying-question}

When your assistant finds that more than one action might fulfill a customer's request, it can automatically ask for clarification. Instead of guessing which action to take, your assistant shows a list of the possible actions to the customer, and asks the customer to pick the right one. For more information, see [Asking clarifying questions](/docs/watson-assistant?topic=watson-assistant-understand-questions#understand-questions-ask-clarifying-question).

On the **Ask clarifying question** tab, you can make the following changes:

- In the **Assistant says** field, edit the text that is displayed before the list of clarification choices.

    The default text is *Did you mean:*. You can change it to something else, such as *What do you want to do?* or *Pick what to do next*.

- In the **Label for a fallback choice** field, edit the label that is displayed for the choice that customers can click when none of the other choices are quite right. When a user picks this choice, the *No action matches* system action is taken next.

    The label *None of the above* is used if you don't change it.  

    This fallback choice gives customers a way to get out of the clarification process if it's not helping them. If you don't want to give customers a fallback choice, remove the text from the field.

If necessary, you can disable clarifying questions for all actions. To disable clarification for all actions:

1. On the **Ask clarifying question** tab, set the switch to **Off**.

1. Click **Save**, and then click **Close**.

## Change conversation topic
{: #actions-global-settings-change-conversation-topic}

The **Change conversation topic** feature enables your assistant to handle digressions, dynamically responding to the user by changing the conversation topic as needed. For more information, see [Allowing your customers to change the topic of the conversation](/docs/watson-assistant?topic=watson-assistant-change-topic).

If necessary, you can disable changing the topic for all actions:

1. On the **Change conversation topic** tab, set the switch to **Off**.

1. Click **Save**, and then click **Close**.

## Autocorrection
{: #actions-global-settings-autocorrection}

*Autocorrection* fixes misspellings that users make in their requests. The corrected words are used to match to an action. 

Autocorrection is enabled automatically for all English-language assistants. It is also available in French-language assistants, but is disabled by default. The autocorrection setting isn't available for any other languages.

For more information, see [Autocorrecting user input](/docs/watson-assistant?topic=watson-assistant-autocorrection).

## Display formats
{: #actions-global-settings-display-formats}

**Display formats** lets you specify the display formats for variables that use date, time, numbers, currency, or percentages. You can also choose a default locale to use if one isn't provided by the client application. This lets you make sure that the format of a variable that's displayed in the web chat is what you want for your assistant. For example, you can choose to have the output of a time variable appear in HH:MM format instead of HH:MM:SS.

Variables are formatted using a system default unless you specify otherwise.

| <nobr>Display format setting</nobr> | Description | <nobr>English - United States (en-US) examples</nobr> |
| ---- | ---- | ---- |
| Locale | Choose a default locale for the assistant if one can't be determined. The locale you choose uses formats specific to that country and language. If you choose a locale, the date, time, number, currency, and percentage format fields change to show choices specific to that locale. The system default is `English - United States (en-US)`. | |
| Date | For calendar dates, choose short, medium, long, full, YY/MM/DD, or YYYY/MM/DD | <ul><li>Short: `1/31/23`</li><li>Medium: `Jan 31, 2023`<li>Long: `January 31, 2023`</li><li>Full: `Tuesday, January 31, 2023`</li></ul> |
| Time | For times, choose short or medium | <ul><li>Short: `1:53 PM`</li><li>Medium: `1:53:30 PM`</li></ul> |
| Number fraction digits | Use the system default (up to 14 digits) or two digits | `10.12` |
| Number delimiter | Use the system default, none, comma, or period | <ul><li>None: `2000.12`</li><li>Comma: `2,000.12`<li>Period: `2.000,12`</li></ul> |
| Currency fraction digits | Use the system default (up to 14 digits) or two digits | `10.99` |
| Currency symbol | Use the system default or choose a global symbol | `$10.99` |
| <nobr>Percentage fraction digits</nobr> | Use the system default (up to 14 digits) or two digits | `10.75%` |


## Algorithm version
{: #actions-global-settings-algorithms-versions}

**Algorithm version** allows you to choose which {{site.data.keyword.conversationshort}} algorithm to apply to your future trainings. For more information, see [Algorithm version](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

## Auto-save
{: #actions-global-settings-auto-save}

When working on actions, your assistant automatically saves changes when you do one of the following:

- Click on a new step
- Open Preview
- Reset Preview

For more information, see [Saving your actions](/docs/watson-assistant?topic=watson-assistant-save-actions)

If you want to disable auto-save, you can toggle it off:

1. On the **Auto-save** tab, set the switch to **Off**.

1. Click **Save**, and then click **Close**.

The auto-save setting is a user preference that applies to all assistants in your instance. Changing the setting applies only to you and doesn't affect other users. {: note}

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

On the **Upload/Download** tab, drag and drop a JSON file onto the tab or click to select a file from your local system, then click **Upload**.

The imported JSON file must use UTF-8 encoding, without byte order mark (BOM) encoding. The JSON file cannot contain tabs, newlines, or carriage returns.
{: important}
