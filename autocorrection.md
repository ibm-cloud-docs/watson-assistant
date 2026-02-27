---

copyright:
  years: 2015, 2026
lastupdated: "2026-02-16"

keywords: autocorrection, spelling correction, spell check

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Autocorrecting user input
{: #autocorrection}

*Autocorrection* fixes misspellings that users make in their requests. Corrected words are used to match to an action or an intent.

Autocorrection corrects user input in the following way:

- Original input: `letme applt for a memberdhip`
- Corrected input: `let me apply for a membership`

- Original input: `I want to know the montth-to-month schedule for a facee-to-faace meting with the supervisor`
- Corrected input: `I want to know the month to month schedule for a face to face meeting with the supervisor`

When your assistant checks whether a word needs a spelling correction, it goes beyond a simple dictionary lookup. It uses natural language processing and probabilistic models to understand the context and decide whether the word is misspelled.

By default, autocorrection is enabled in all assistants that use English. However, it is disabled by default in all assistants that use French. You can enable or disable **Autocorrection** by going to **Global settings** > **Autocorrection**. 

Autocorrection is not available for search integration in your assistant and for assistant languages other than English and French. {: important}

## Disabling autocorrection
{: #autocorrection-disable}

If necessary, you can disable autocorrection for your assistant. 

If a domain‑specific term is incorrectly corrected, you can prevent this behavior by adding the term or phrase to your training data. For more information, see [Autocorrection rules](#autocorrection-rules).
{: note}

If you are using actions in your assistant, follow these steps to disable autocorrection:

1. On the **Actions** page, click **Global settings** ![Gear icon](images/gear-icon-black.png).

1. Click the **Autocorrection** tab.

1. Set the switch to **Off**, then click **Save**.

If you are using dialog in your assistant, follow these steps to disable autocorrection:

1.  In the **Options** section, click **Autocorrection**.

1. Set the switch to **Off**.

## Testing autocorrection in dialog
{: #autocorrection-test}

If you are using dialog, you can test autocorrection by using **Try it out**.

1.  In **Try it out**, enter a request that includes some misspelled words.

    If words in your input are misspelled, they are corrected automatically, and an ![Auto-correct](images/auto-correct.png) icon is displayed. The corrected utterance is underlined.

1.  Hover over the underlined utterance to see the original wording.

    If your assistant does not correct a misspelled term that you expected it to fix, review the correction rules. It might show that the term belongs to a category the assistant does not change.

## Autocorrection rules
{: #autocorrection-rules}

To avoid overcorrection, your assistant does not correct the spelling of the following types of input:

- Capitalized words.
- Words with an uppercase character.
- Emojis.
- Locations, such as states and street addresses.
- Numbers and units of measurement or time.
- Proper nouns, such as common given names or company names.
- Text within quotation marks.
- Words containing special characters, such as asterisks (*), ampersands (&), or at signs (@), including the ones used in email addresses or URLs.
- Words that *belong*, meaning words with implied significance because they occur in your action steps, dialog entity values, entity synonyms, or intent user examples.

### How is spelling autocorrection related to fuzzy matching?
{: #autocorrection-vs-fuzzy-matching}

In dialog, *fuzzy matching* helps your assistant recognize dictionary-based entity mentions in user input. It uses a dictionary lookup approach to match a word from the user input to an existing entity value or synonym in the skill's training data. For example, if the user enters `boook`, and your training data contains a `@reading_material` entity with a `book` value, then fuzzy matching recognizes that the two terms (`boook` and `book`) mean the same thing.

In dialog, when both autocorrection and fuzzy matching are enabled, fuzzy matching runs first. If it matches a term to a dictionary entity value or synonym, it marks the term as belonging to the skill. It then skips autocorrection for that term.

For example, if a user enters a sentence like `I wnt to buy a boook`, fuzzy matching identifies that `boook` matches your entity value `book` and adds it to the protected words list. Your assistant then corrects the input to `I want to buy a boook`. Notice that it fixes `wnt` but does not change `boook`. If you see this behavior when you test your dialog, it might seem like the assistant is making a mistake. However, it is behaving correctly. 

Fuzzy matching identifies `boook` as a `@reading_material` entity mention, and autocorrection updates `wnt` to `want`, and enables the assistant to map the input to the `#buy_something` intent. Each feature contributes differently, but together they help your assistant to interpret the user’s meaning accurately.
