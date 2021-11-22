---

copyright:
  years: 2015, 2021
lastupdated: "2021-10-08"

keywords: global support, universal language, universal model, another language

subcollection: watson-assistant

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# Adding support for global audiences
{: #admin-language-support}

Your customers come from all around the globe. You need an assistant that can talk to them in their own language and in a familiar style. Choose the approach that best fits your business needs.

- **Quickest solution**: The simplest way to add language support is to author the assistant in a single language. You can translate each message that is sent to your assistant from the customer's local language to the assistant language. Later you can translate each response from the assistant language back to the customer's local language.

    This approach simplifies the process of authoring and maintaining the conversation. You can build one assistant and use it for all languages. However, the intention and meaning of the customer message can be lost in the translation.

    For more information about webhooks you can use for translation, see [Webhook overview](/docs/watson-assistant?topic=watson-assistant-webhook-overview).

- **Most precise solution**: If you have the time and resources, the best user experience can be achieved when you build multiple assistants, one for each language that you want to support. {{site.data.keyword.conversationshort}} has built-in support for all languages. Use one of 13 language-specific models or the universal model, which adapts to any other language you want to support.

    When you build an assistant that is dedicated to a language, a language-specific classifier model is used by the assistant. The precision of the model means that your assistant can better understand and recognize the goals of even the most colloquial message from a customer.

    Use the universal language model to create an assistant that is fluent even in languages that {{site.data.keyword.conversationshort}} doesn't support with built-in models.

    To deploy, use the web chat integration with your French-speaking assistant to deploy to a French-language page on your website. Deploy your German-speaking assistant to the German page of your website. Maybe you have a support phone number for French customers. You can configure your French-speaking assistant to answer those calls, and configure another phone number that German customers can use.

## Understanding the universal language model 
{: #admin-language-support-universal}

An assistant that uses the universal language model applies a set of shared linguistic characteristics and rules from multiple languages as a starting point. It then learns from the training data that you add to it.

The universal language classifier can adapt to a single language per assistant. It cannot be used to support multiple languages within a single assistant. However, you can use the universal language model in one assistant to support one language, such as Russian, and in another assistant to support another language, such as Hindi. The key is to add enough training examples or intent user examples in your target language to teach the model about the unique syntactic and grammatical rules of the language.

Use the universal language model when you want to create a conversation in a language for which no dedicated language model is available, and which is unique enough that an existing model is insufficient.

For more information about feature support in the universal language model, see [Supported languages](#admin-language-support-codes).

## Integration considerations
{: #admin-language-support-integrations}

Keep these tips in mind for integrations:

- **Phone integration**: If you want to deploy an assistant that uses the universal language model with the phone integration, you must connect to custom Speech service language models that can understand the language you're using. For more information about supported language models, see the [Speech to Text](/docs/speech-to-text?topic=speech-to-text-models#modelsList){: external} and [Text to Speech](/docs/text-to-speech?topic=text-to-speech-voices#languageVoices){: external} documentation.
- **Search integration**: If you build an assistant that specializes in a single language, be sure to connect it to data collections that are written in that language. For more information about the languages that are supported by {{site.data.keyword.discoveryshort}}, see [Language support](/docs/discovery-data?topic=discovery-data-language-support){: external}.
- **Web chat**: Web chat has some hardcoded strings that you can customize to reflect your target language. For more information, see [Global audience support](/docs/watson-assistant?topic=watson-assistant-web-chat-basics#web-chat-basics-global).

## Supported languages
{: #admin-language-support-codes}

{{site.data.keyword.conversationshort}} supports individual features to varying degrees per language.
{: shortdesc}

{{site.data.keyword.conversationshort}} has classifier models that are designed specifically to support conversations in the following languages:

| Language | Language code |
|----------|---------------|
| Arabic | ar |
| Chinese (Simplified) | zh-cn |
| Chinese (Traditional) | zh-tw |
| Czech | cs |
| Dutch | nl |
| English | en-us |
| French | fr |
| German | de |
| Italian | it |
| Japanese | ja |
| Korean | ko |
| Portuguese (Brazilian) | pt-br |
| Spanish | es |
| Universal | xx |
{: caption="Table 1. Supported languages" caption-side="top"}

## Feature support details
{: #admin-language-support-tables}

The following tables illustrate the level of language support available for product features.

In the following tables, the level of language and feature support is indicated by these codes:

- GA: The feature is generally available and supported for this language. Note that features might continue to be updated even after they are generally available.
- Beta: The feature is supported only as a Beta release, and is still undergoing testing before it is made generally available in this language.
- NA: Indicates that a feature is not available in this language.

### Content support details
{: #admin-language-support-content}

| Language | **Actions** | <!--**Dialog**--> | **Search** |
| --- |:---:|:---:|:---:|
| **English (en)**                   | GA | <!--GA--> | GA |
| **Arabic (ar)**                    | GA | <!--GA--> | GA |
| **Chinese (Simplified) (zh-cn)**   | GA | <!--GA--> | GA |
| **Chinese (Traditional) (zh-tw)**  | GA | <!--GA--> | GA |
| **Czech (cs)**                     | GA | <!--GA--> | GA |
| **Dutch (nl)**                     | GA | <!--GA--> | GA |
| **French (fr)**                    | GA | <!--GA--> | GA |
| **German (de)**                    | GA | <!--GA--> | GA |
| **Italian (it)**                   | GA | <!--GA--> | GA |
| **Japanese (ja)**                  | GA | <!--GA--> | GA |
| **Korean (ko)**                    | GA | <!--GA--> | GA |
| **Portuguese (Brazilian) (pt-br)** | GA | <!--GA--> | GA |
| **Spanish (es)**                   | GA | <!--GA--> | GA |
| **Universal (xx)**                 | GA | <!--GA--> | GA |
{: caption="Table 2. Content support details" caption-side="top"}

<!--### Intent feature support details
{: #admin-language-support-intents}

| Language | **[Content Catalog](/docs/assistant?topic=assistant-catalog){: external}** | **[Irrelevance detection](/docs/assistant?topic=assistant-irrelevance-detection){: external}** | **[Enhanced intent detection](/docs/assistant?topic=assistant-intent-detection){: external}** |
|:---:|:---:|:---:|:---:|
| **English (en)**                   | GA | GA | GA |
| **Arabic (ar)**                    | GA (except Covid-19) | NA | NA |
| **Chinese (Simplified) (zh-cn)**   | NA | NA | NA |
| **Chinese (Traditional) (zh-tw)**  | NA | NA | NA |
| **Czech (cs)**                     | NA | NA | NA |
| **Dutch (nl)**                     | NA | NA | NA |
| **French (fr)**                    | GA | NA | NA |
| **German (de)**                    | GA (except Covid-19) | NA | NA |
| **Italian (it)**                   | GA (except Covid-19) | NA | NA |
| **Japanese (ja)**                  | GA (except Covid-19) | NA | NA |
| **Korean (ko)**                    | NA | NA | NA |
| **Portuguese (Brazilian) (pt-br)** | GA | NA | NA |
| **Spanish (es)**                   | GA | NA | NA |
| **Universal (xx)**                 | NA | GA | GA |
{: caption="Table 3. Intent feature support details" caption-side="top"}

### Recommendations feature support details continued
{: #admin-language-support-recommendations}

| Language | **[User example recommendations](/docs/assistant?topic=assistant-intent-recommendations#intent-recommendations-get-example-recommendations-task){: external}** | **[Intent recommendations](/docs/assistant?topic=assistant-intent-recommendations#intent-recommendations-get-intent-recommendations-task){: external}** |
|:---:|:---:|:---:|
| **English (en)**                   | GA | GA |
| **Arabic (ar)**                    | NA | NA |
| **Chinese (Simplified) (zh-cn)**   | NA | NA |
| **Chinese (Traditional) (zh-tw)**  | NA | NA |
| **Czech (cs)**                     | NA | NA |
| **Dutch (nl)**                     | NA | NA |
| **French (fr)**                    | NA | GA |
| **German (de)**                    | NA | GA |
| **Italian (it)**                   | NA | GA |
| **Japanese (ja)**                  | GA | NA |
| **Korean (ko)**                    | NA | NA |
| **Portuguese (Brazilian) (pt-br)** | NA | GA |
| **Spanish (es)**                   | NA | GA |
| **Universal (xx)**                 | NA | NA |
{: caption="Table 4. Recommendations feature support details continued" caption-side="top"}-->

<!--### User input processing support details
{: #admin-language-support-input}

| Language | **[Dictionary-based entity support](/docs/assistant?topic=assistant-entities#entities-create-dictionary-based){: external}** | **[Fuzzy matching (*Misspelling*)](/docs/assistant?topic=assistant-entities#entities-fuzzy-matching){: external}** | **[Fuzzy matching (*Stemming*, *Partial match*)](/docs/assistant?topic=assistant-entities#entities-fuzzy-matching){: external}** | **[Autocorrection](/docs/assistant?topic=assistant-dialog-runtime-spell-check){: external}** |
|:---:|:---:|:---:|:---:|:---:|
| **English (en)**                   | GA | GA | GA | GA |
| **Arabic (ar)**                    | GA | GA | NA | NA |
| **Chinese (Simplified) (zh-cn)**   | GA | NA | NA | NA |
| **Chinese (Traditional) (zh-tw)**  | GA | NA | NA | NA |
| **Czech (cs)**                     | GA | GA | GA | NA |
| **Dutch (nl)**                     | GA | GA | NA | NA |
| **French (fr)**                    | GA | GA | GA | Beta |
| **German (de)**                    | GA | GA | GA | NA |
| **Italian (it)**                   | GA | GA | NA | NA |
| **Japanese (ja)**                  | GA | GA | NA | NA |
| **Korean (ko)**                    | GA | GA | NA | NA |
| **Portuguese (Brazilian) (pt-br)** | GA | GA | NA | NA |
| **Spanish (es)**                   | GA | GA | NA | NA |
| **Universal (xx)**                 | GA | GA | NA | NA |
{: caption="Table 5. User input processing support details" caption-side="top"}-->

<!--### Entity feature support details
{: #admin-language-support-entities}

| Language | **[Contextual entities](/docs/assistant?topic=assistant-entities#entities-create-annotation-based){: external}** | **[Synonym recommendations](/docs/assistant?topic=assistant-entities#entities-create-dictionary-based){: external}** |
|:---:|:---:|:---:|
| **English (en)**                   | GA | GA |
| **Arabic (ar)**                    | NA | NA |
| **Chinese (Simplified) (zh-cn)**   | NA | NA |
| **Chinese (Traditional) (zh-tw)**  | NA | NA |
| **Czech (cs)**                     | NA | NA |
| **Dutch (nl)**                     | NA | NA |
| **French (fr)**                    | Beta | GA |
| **German (de)**                    | NA | NA |
| **Italian (it)**                   | NA | NA |
| **Japanese (ja)**                  | NA | GA |
| **Korean (ko)**                    | NA | NA |
| **Portuguese (Brazilian) (pt-br)** | NA | NA |
| **Spanish (es)**                   | NA | GA |
| **Universal (xx)**                 | NA | NA |
{: caption="Table 6. Entity feature support details" caption-side="top"}-->

<!--### System entity feature support details
{: #admin-language-support-system-entities}

| Language | **[System entities](/docs/assistant?topic=assistant-system-entities){: external}** | **[Legacy system entities](/docs/assistant?topic=assistant-legacy-system-entities){: external}** |
|:---|:---:|:---:|
| **English (en)**                   | GA | Deprecated |
| **Arabic (ar)**                    | GA | Deprecated |
| **Chinese (Simplified) (zh-cn)**   | GA | Deprecated |
| **Chinese (Traditional) (zh-tw)**  | GA | Deprecated |
| **Czech (cs)**                     | GA | Deprecated |
| **Dutch (nl)**                     | GA | Deprecated |
| **French (fr)**                    | GA | Deprecated |
| **German (de)**                    | GA | Deprecated |
| **Italian (it)**                   | GA | Deprecated |
| **Japanese (ja)**                  | GA | Deprecated |
| **Korean (ko)**                    | GA | Deprecated |
| **Portuguese (Brazilian) (pt-br)** | GA | Deprecated |
| **Spanish (es)**                   | GA | Deprecated |
| **Universal (xx)**                 | GA | NA |
{: caption="Table 7. System entity feature support details" caption-side="top"}-->

The {{site.data.keyword.conversationshort}} service supports multiple languages as noted, but the tool interface itself (descriptions, labels, etc.) is in English. All supported languages can be input and trained through the English interface.
{: note}

GB18030 compliance: GB18030 is a Chinese standard that specifies an extended code page for use in the Chinese market. This code page standard is important for the software industry because the China National Information Technology Standardization Technical Committee has mandated that any software application that is released for the Chinese market after September 1, 2001, be enabled for GB18030. The {{site.data.keyword.conversationshort}} service supports this encoding, and is certified GB18030-compliant

## Changing an assistant language
{: #admin-language-support-change-language}

Once an assistant has been created, its language cannot be modified.

<!--## Configuring bidirectional languages
{: #admin-language-support-configure-bidirectional}

For bidirectional languages, such as Arabic, you can change your skill preferences.

1.  From your skill tile, click the *Actions* drop-down menu, and then select **Language Preferences**.

    This option is only available for skills that are configured to use a bidirectional language.
    {: note}

1.  Select from the following options for your skill:

    - **GUI Direction**: Specifies the layout direction of elements, such as buttons or menus, in the graphical user interface. Choose `LTR` (left-to-right) or `RTL` (right-to-left). If not specified, the tool follows the web browser GUI direction setting.
    - **Text Direction**: Specifies the direction of typed text. Choose `LTR` (left-to-right) or `RTL` (right-to-left), or select `Auto` which will automatically choose the text direction based on your system settings. The `None` option will display left-to-right text.
    - **Numeric Shaping**: Specifies which form of numerals to use when presenting regular digits. Choose from `Nominal`, `Arabic-Indic`, or `Arabic-European`. The `None` option will display Western numerals.
    - **Calendar Type**: Specifies how you choose filtering dates in the skill UI. Choose `Islamic-Civil`, `Islamic-Tabular`, `Islamic-Umm al-Qura`, or `Gregorian`.

    This setting is not reflected in the "Try it out" panel.
    {: note}

    ![Bidi options](images/bidi-options.png)

1.  Click the **X** to close the page. Your changes are saved automatically.-->

## Working with accented characters
{: #admin-language-support-accents}

In a conversational setting, users might or might not use accents while interacting with the {{site.data.keyword.conversationshort}} service. As such, both accented and non-accented versions of words might be treated the same for intent detection and entity recognition.

However for some languages, like Spanish, some accents can alter the meaning of the entity. Thus, for entity detection, although the original entity might implicitly have an accent, your assistant can also match the non-accented version of the same entity, but with a slightly lower confidence score.

For example, for the word "barrió", which has an accent and corresponds to the past tense of the verb "barrer" (to sweep), your assistant can also match the word "barrio" (neighborhood), but with a slightly lower confidence.

The system will provide the highest confidence scores in entities with exact matches. For example, `barrio` will not be detected if `barrió` is in the training set; and `barrió` will not be detected if `barrio` is in the training set.

You are expected to train the system with the proper characters and accents. For example, if you are expecting `barrió` as a response, then you should put `barrió` into the training set.

Although not an accent mark, the same applies to words using, for example, the Spanish letter `ñ` vs. the letter `n`, such as "uña" vs. "una". In this case the letter `ñ` is not simply an `n` with an accent; it is a unique, Spanish-specific letter.

<!--You can enable fuzzy matching if you think your customers will not use the appropriate accents, or misspell words (including, for example, putting a `n` instead of a `ñ`), or you can explicitly include them in the training examples.-->
