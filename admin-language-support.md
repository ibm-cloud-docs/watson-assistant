---

copyright:
  years: 2015, 2023
lastupdated: "2023-07-25"

keywords: global support, universal language, universal model, another language

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

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

    You can enable the download of language data files, in CSV format, so you can translate training examples and assistant responses from English into other languages and use in other assistants. For more information, see [Using multilingual downloads for translation](#admin-language-support-multilingual).

## Understanding the universal language model 
{: #admin-language-support-universal}

An assistant that uses the universal language model applies a set of shared linguistic characteristics and rules from multiple languages as a starting point. It then learns from the training data that you add to it.

The universal language classifier can adapt to a single language per assistant. It cannot be used to support multiple languages within a single assistant. However, you can use the universal language model in one assistant to support one language, such as Russian, and in another assistant to support another language, such as Hindi. The key is to add enough training examples or intent user examples in your target language to teach the model about the unique syntactic and grammatical rules of the language.

Use the universal language model when you want to create a conversation in a language where no model is available, and which is unique enough that an existing model is insufficient.

For more information about feature support in the universal language model, see [Supported languages](#admin-language-support-codes).

## Integration considerations
{: #admin-language-support-integrations}

Keep these tips in mind for integrations:

- **Phone integration**: If you want to deploy an assistant that uses the universal language model, you must connect to custom Speech service language models that can understand the language you're using. For more information about supported language models, see the [Speech to Text](/docs/speech-to-text?topic=speech-to-text-models#modelsList){: external} and [Text to Speech](/docs/text-to-speech?topic=text-to-speech-voices#languageVoices){: external} documentation.
- **Search integration**: If you build an assistant that specializes in a single language, be sure to connect it to data collections that are written in that language. For more information about the languages that are supported by {{site.data.keyword.discoveryshort}}, see [Language support](/docs/discovery-data?topic=discovery-data-language-support){: external}.
- **Web chat**: Web chat has some hardcoded strings that you can customize to reflect your target language. For more information, see [Supporting global audiences](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-global).

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
| Universal* | xx |
*If you want to support conversations in a language for which Watson Assistant does not have a dedicated model, such as Russian, use Universal. 
{: caption="Supported languages" caption-side="top"}

## Feature support details
{: #admin-language-support-tables}

The level of language and feature support is indicated by codes:

- GA: The feature is generally available and supported for this language. Features might continue to be updated even after they are generally available.
- Beta: The feature is supported only as a Beta release and is still undergoing testing before it is made generally available in this language.
- NA: A feature is not available in this language.

### Content support details
{: #admin-language-support-content}

| Language | **Actions** | **Dialog** | **Search** |
| --- |:---:|:---:|:---:|
| **English (en)**                   | GA |  GA | GA |
| **Arabic (ar)**                    | GA | GA | GA |
| **Chinese (Simplified) (zh-cn)**   | GA | GA | GA |
| **Chinese (Traditional) (zh-tw)**  | GA | GA | GA |
| **Czech (cs)**                     | GA | GA | GA |
| **Dutch (nl)**                     | GA | GA | GA |
| **French (fr)**                    | GA | GA | GA |
| **German (de)**                    | GA | GA | GA |
| **Italian (it)**                   | GA | GA | GA |
| **Japanese (ja)**                  | GA | GA | GA |
| **Korean (ko)**                    | GA | GA | GA |
| **Portuguese (Brazilian) (pt-br)** | GA | GA | GA |
| **Spanish (es)**                   | GA | GA | GA |
| **Universal (xx)**                 | GA | GA | GA |
{: caption="Content support details" caption-side="top"}

The {{site.data.keyword.conversationshort}} service supports multiple languages as noted, but the user interface itself (such as descriptions and labels) is in English. All supported languages can be input and trained through the English interface.
{: note}

GB18030 compliance: GB18030 is a Chinese standard that specifies an extended code page for use in the Chinese market. This code page standard is important for the software industry because the China National Information Technology Standardization Technical Committee mandates that any software application that is released for the Chinese market after September 1, 2001, be enabled for GB18030. The {{site.data.keyword.conversationshort}} service supports this encoding, and is certified GB18030-compliant

## Changing an assistant language
{: #admin-language-support-change-language}

After an assistant is created, its language cannot be modified.

## Working with accented characters
{: #admin-language-support-accents}

In a conversational setting, users might or might not use accents with the {{site.data.keyword.conversationshort}} service. As such, both accented and nonaccented versions of words might be treated the same for intent detection and entity recognition.

However, for some languages like Spanish, some accents can alter the meaning of the entity. Thus, for entity detection, although the original entity might implicitly have an accent, your assistant can also match the nonaccented version of the same entity, but with a slightly lower confidence score.

For example, for the word "barrió", which has an accent and corresponds to the past tense of the verb "barrer" (to sweep), your assistant can also match the word "barrio" (neighborhood), but with a slightly lower confidence.

The system provides the highest confidence scores in entities with exact matches. For example, `barrio` isn't detected if `barrió` is in the training set; and `barrió` isn't detected if `barrio` is in the training set.

You are expected to train the system with the proper characters and accents. For example, if you are expecting `barrió` as a response, put `barrió` into the training set.

Although not an accent mark, the same applies to words that use the Spanish letter `ñ` versus the letter `n`, such as "uña" versus "una". In this case, the letter `ñ` is not simply an `n` with an accent; it is a unique, Spanish-specific letter.

## Using multilingual downloads for translation
{: #admin-language-support-multilingual}

[IBM Cloud]{: tag-ibm-cloud}

You can enable the download of language data files, in CSV format, so you can translate training examples and assistant responses into other languages and use in other assistants.

Each CSV file includes `translatable_string` data that you can use with a machine or human translation service. 

Each CSV file also includes `id`, `resource_type`, and `locator` data that {{site.data.keyword.conversationshort}} can use in another assistant to re-create your source assistant. You don't need to edit this information.

The overview of the multilingual process is:
- [Enable multilingual download](#admin-language-support-multilingual-enable): In your source assistant, enable multilingual download
- [Translate content](#admin-language-support-multilingual-translate): Use the CSV files with a translation service
- [Upload to language-specific assistants](#admin-language-support-multilingual-upload): In a destination assistant for another language, use the CSV files to upload translated training and responses

### Enabling multilingual download
{: #admin-language-support-multilingual-enable}

To enable multilingual download:

1. Open **Assistant settings**.

1. In the **Download/Upload** section, click **Enable multilingual download**. 

   Enabling multilingual might take a few minutes to process, but you can work elsewhere in the assistant. The Download/Upload button is disabled until this process finishes. After the multilingual download is enabled in an assistant, it can't be disabled.
   {: note}

1. Click **Download/Upload files**. 

1. On the **Download** tab, choose **Multilingual file package**.

1. Select a published version, then click **Download**. You need at least one version for the download to be available.

   Downloading your first file might take a few minutes to process, but you can work elsewhere in the assistant. The Download/Upload button is disabled until this process finishes.
   {: note}

1. When the download finishes, your .zip file contains:

   - `action-responses.csv`
   - `action-training.csv`
   - `Data (Do not edit)` folder, which contains `assistant.bin`

   If you are using dialog, the .zip file also contains:
   - `dialog-responses.csv`
   - `dialog-training.csv`

### Translating content
{: #admin-language-support-multilingual-translate}

To translate content:

1. Translate the content in the CSV files, for example, from English to French. Save files with translations as CSV UTF-8 (Comma Delimited) to account for any language-specific characters.

1. When you are finished with the translation process, create a new .zip file that includes:

   - `action-responses.csv` with your translations. Don't change the name of the file.
   - `action-training.csv` with your translations. Don't change the name of the file.
   - The original, untouched `Data (Do not edit)` folder, which contains `assistant.bin`

   If you translated dialog content, also include `dialog-responses.csv` and `dialog-training.csv` in the .zip file.

### Uploading to language-specific assistants
{: #admin-language-support-multilingual-upload}

To upload to a language-specific assistant:

1. Create or switch to a destination assistant that uses the language for your translations. 

1. In the destination assistant, open **Assistant settings**.

1. If you translated dialog training and responses, ensure that dialog is active in the destination assistant.

1. In the **Download/Upload** section, click **Download/Upload files**.

   You don't need to enable multilingual download in the destination assistant.
   {: note}

1. On the **Upload** tab, choose **Multilingual file package**.

1. Attach your multilingual .zip file package, then click **Upload**. The translated content is added to your draft environment, so you can work on publishing the translated assistant.
