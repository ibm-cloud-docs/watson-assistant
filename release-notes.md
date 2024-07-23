---

copyright:
  years: 2015, 2024
lastupdated: "2024-07-23"

subcollection: watson-assistant

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.conversationshort}}
{: #watson-assistant-release-notes}

Release notes describe the new features, changes, and bug fixes in each release of the product. For more information about changes in the web chat integration, see the [Web chat release notes](/docs/watson-assistant?topic=watson-assistant-release-notes-chat).




## 23 July 2024
{: #watson-assistant-jul232024}
{: release-note}

New “End the action” step behavior
: Using "End to action" in the last step no longer ends the action immediately. For more information see, [Choosing what to do at the end of a step](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-step-what-next)

New Hate, Abuse and Profanity Filter for {{site.data.keyword.conversationshort}}
: The new Hate, Abuse and Profanity (HAP) filter in {{site.data.keyword.conversationshort}} enhances user safety by identifying and addressing hate speech, abuse and profanity. This feature helps maintain a positive and inclusive online environment for your customers. For more information, see [HAP filter](/docs/watson-assistant?topic=watson-assistant-hap-filter).

## 18 July 2024
{: #watson-assistant-jul182024}
{: release-note}

Server-Sent Events for custom extensions
: watsonxAssistant now supports defining a JSON Path to stream text from Server-Sent Events (SSE) in custom extensions. This feature ensures that text is streamed and stored correctly, with built-in checks to handle potential errors. For more information, see [Streaming from an extension](/docs/watson-assistant?topic=watson-assistant-stream-from-extension).



## 03 July 2024
{: #watson-assistant-jul032024}
{: release-note}

Referencing user-defined variables with `user_defined_` prefix
: You can now reference the user-defined action or session variables through expressions in actions by using a reserved keyword prefix `user_defined_`. For more information, see [Variables](/docs/watson-assistant?topic=watson-assistant-expressions#expression-syntax-variables).

## 01 July 2024
{: #watson-assistant-jul012024}
{: release-note}

All-new homepage for {{site.data.keyword.conversationshort}}
: The all-new homepage of {{site.data.keyword.conversationshort}} has well-organized sections and easy-to-access tabs to enhance your user-interface experience. For more information, see [Getting started](/docs/watson-assistant?topic=watson-assistant-getting-started).

## 7 June 2024
{: #watson-assistant-jun072024}
{: release-note}

Improved accuracy in information gathering
: The information gathering feature is enhanced to reduce errors while filling the free-text step variables from the customer response. This allows for more accurate and efficient data entry. For more information, see [Information gathering](/docs/watson-assistant?topic=watson-assistant-information-gathering).

## 4 June 2024
{: #watson-assistant-jun042024}
{: release-note}
Phone-based conversational search support

: You can now use the streaming feature in the conversational search for the phone integration in your assistant. For more information see, [Conversational search](/docs/watson-assistant?topic=watson-assistant-conversational-search) and [Integrating with phone](/docs/watson-assistant?topic=watson-assistant-deploy-phone).

## 14 May 2024
{: #watson-assistant-may142024}
{: release-note}

Autocorrection is disabled for search integration
: The [autocorrection](/docs/watson-assistant?topic=watson-assistant-actions-global-settings#actions-global-settings-autocorrection) feature is now disabled for search integration in your assistant. For more information, see [Autocorrecting user input](/docs/watson-assistant?topic=watson-assistant-autocorrection).


## 03 May 2024
{: #watson-assistant-may032024}
{: release-note}

Conversational search is now generally available
: The Conversational search feature with the Retrieval-Augmented Generation (RAG) solution, powered by watsonx.ai, is now generally available. For more information about conversational search, see [Conversational search](/docs/watson-assistant?topic=watson-assistant-conversational-search). 

Elasticsearch search integration is now generally available
: Elasticsearch search integration is now generally available. For more information about Elasticsearch search integration, see [Elasticsearch search integration setup](/docs/watson-assistant?topic=watson-assistant-search-elasticsearch-add).


## 18 April 2024
{: #watson-assistant-apr192024}
{: release-note}

Tuning your assistant's tendency to say "I don't know"
:  You can now tune the tendency of your assistant to say "I don't know" in conversational search by using the **Tendency to say “I don’t know”** option in the conversational search settings. This option can help to reduce Large Language Model (LLM) hallucinations and provide higher fidelity answers for conversational search by tuning your assistant's tendency to fall back to the “I don’t know” answer. For more information, see [Tuning conversational search’s tendency to say “I don’t know"](/docs/watson-assistant?topic=watson-assistant-conversational-search#behavioral-tuning-conversational-search).

## 15 April 2024
{: #watson-assistant-apr152024}
{: release-note}



Overwrite all or skip all when you copy actions to another assistant
:  You can now choose to overwrite all references or skip all references when you copy actions from one assistant into another. For more information, see [Copying an action to another assistant](/docs/watson-assistant?topic=watson-assistant-copy-action).

## 11 April 2024
{: #watson-assistant-apr052024}
{: release-note}

Add examples for variables in the action editor
: You can now add examples of variables in a user input by using the Add examples button in the action editor. This helps your assistant to retrieve accurate information and respond to the user quickly. For more information, see [Adding examples for clarity](/docs/watson-assistant?topic=watson-assistant-information-gathering#add-examples-for-clarity).

Add a custom result filter for the search integration
: You can now filter your search result in the {{site.data.keyword.discoveryshort}} search integration by adding custom text strings in the **Custom result filter** field in **Search integration**. For more information, see [Configure the search for {{site.data.keyword.discoveryshort}}](/docs/watson-assistant?topic=watson-assistant-search-add#search-add-configure).

Configure search routing
: You can now configure the search routing for your assistant when no matches are available for the customer response. For more information, see [Configuring the search routing when no action matches](/docs/watson-assistant?topic=watson-assistant-handle-errors#config-search-routing).

## 26 March 2024
{: #watson-assistant-mar262024}
{: release-note}

Support integration with Genesys Audio Connector
: You can now integrate Genesys Audio Connector with your assistant to stream the conversation audio between the assistant and Genesys Cloud. For more information, see [Integrating with Genesys Audio Connector](/docs/watson-assistant?topic=watson-assistant-deploy-genesys-audioconnector).

## 16 February 2024
{: #watson-assistant-feb162024}
{: release-note}

Support for Llama2 chat format
:	You can now transform the session history of your assistant to a Llama2 compatible format for the generative AI use cases. For more information, see [`Array.transform()`](/docs/watson-assistant?topic=watson-assistant-expression-methods-actions#expression-methods-actions-arrays-transform) and [Session history](/docs/watson-assistant?topic=watson-assistant-publish-overview#publish-overview-environment-settings-session-history).

## 12 January 2024
{: #watson-assistant-jan122024}
{: release-note}

Segment extension
:   The segment extension is now available for Plus plan, Enterprise plan and Enterprise with data isolation plan. For more information, see [Sending events to Segment](/docs/watson-assistant?topic=watson-assistant-segment-add).

View number of actions within collections
:   You can now view the total number of actions that are within each collection on the **Action** page.

Search and analyze the conversational search requests
:   You can now search and analyze the conversational search requests from the customer in the **Analyze** page. For more information, see [Filtering conversations](/docs/watson-assistant?topic=watson-assistant-analytics-conversations#analytics-conversations-filtering).

## 15 December 2023
{: #watson-assistant-dec152023}
{: release-note}

OpenAPI document file size limit for integrating custom extension 
:   When you integrate a custom extension by using REST API, the maximum file size of the OpenAPI document that you can import is limited to `4 MB` if you have a *Plus* or *Enterprise* plan of {{site.data.keyword.conversationshort}}. However, if you have an Enterprise plan with data isolation, the maximum file size of the document is limited to `8 MB`. For more information, see [Preparing the API definition](/docs/watson-assistant?topic=watson-assistant-build-custom-extension#build-custom-extension-openapi-file).

Edit variable values directly in debug mode
:   You can now edit the variable value directly in the debug mode by clicking on the values. For more information, [Editing the variable values](/docs/watson-assistant?topic=watson-assistant-review#edit-variable-values).

Expand the debug mode panel for better visibility
:   You can now expand the debug mode panel by clicking the **Expand** icon for better visibility of the long variable values. For more information, see [Variable values in Preview](/docs/watson-assistant?topic=watson-assistant-review#review-variable-values).

## 12 December 2023
{: #watson-assistant-dec122023}
{: release-note}

Invalid date entry not accepted
:   Starting from this release, the assistant does not recognize the invalid date entry such as `Feb 31`, `31/11/2022`, and `Feb 29 2023`. In addition, the assistant does not automatically parse the invalid dates to the first day of the month. For more information, see [@sys-date](/docs/assistant?topic=assistant-system-entities#system-entities-sys-date).

## 8 December 2023
{: #watson-assistant-dec082023}
{: release-note}

Algorithm version Latest(15-Apr-2023) uses improved intent detection and matching 
:   The **Latest(15-Apr-2023)** algorithm version uses a new foundation model to improve the intent detection and action matching in assistants with languages such as English, French, German, Portuguese (Brazilian), Spanish, Arabic, Chinese (Simplified), Chinese (Traditional), Czech, Dutch, Italian, Japanese, and Korean. The new foundation model is trained by using the transformer architecture. For more information, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

Change in Pause response time configuration
:   You can now pause a response for any duration from `0` to `60 seconds`, which was limited from `1` to `10 seconds` in the previous releases. In addition, you can now pause the response in `milliseconds` by entering decimals of a `second` in the **Duration** field. For more information, see [Pause response](/docs/watson-assistant?topic=watson-assistant-respond#respond-pause-response).

## 28 November 2023
{: #watson-assistant-nov282023}
{: release-note}

New Genesys Bot Connector integration
:   You can create a Bot Connector that integrates Genesys Cloud with your assistant to faciliate messaging and conversation flows. For more information, see [Integrating with Genesys Bot Connector](/docs/watson-assistant?topic=watson-assistant-deploy-genesys-botconnector).

Intelligently recognize information in free text responses
:   You can now enable your assistants to intelligently recognize information provided by the customer in a session when using the free text response in an **Action** step. When you enable this feature, your assistant uses a large language model (LLM) in [watsonx.ai](https://www.ibm.com/products/watsonx-ai) to intelligently recognize multiple pieces of information in customer responses and fill corresponding steps to avoid multiple prompts in a session. This is a beta feature and available only in assistants that use the English language. For more information, see [Information Gathering](/docs/watson-assistant?topic=watson-assistant-using-watsonxai-for-generative-ai-capabilities) and [Global settings for actions](/docs/watson-assistant?topic=watson-assistant-actions-global-settings).

Conversational search by integrating Elasticsearch
:   You can now configure Elasticsearch as the content source for your search integration. For more information, see [Adding search](/docs/watson-assistant?topic=watson-assistant-search-overview#elasticsearch-integration-overview).

## 20 November 2023
{: #watson-assistant-nov202023}
{: release-note}

Message logs for a dialog without action
:   You can now use the **Message logs** tab in the **Analyze** page to see a log of all messages that are sent between the user and the assistant by turns. This feature is available for all messages including the messages that are sent when dialog is activated. For more information, see [Review customer conversations](/docs/watson-assistant?topic=watson-assistant-analytics-conversations).

Masking confidential customer information in assistants with `stateless` endpoint
:   You can now mask the confidential information in user input and assistant responses for assistants with the `stateless` endpoint. In the `stateless` message API, the private data is encrypted before returning them to the client app. For more information, see [Using variables to manage conversation information](/docs/watson-assistant?topic=watson-assistant-manage-info) and [Protecting the privacy of the customer information](/docs/watson-assistant?topic=watson-assistant-collect-info#protect-privacy-customer-information).

## 10 November 2023
{: #watson-assistant-nov102023}
{: release-note}

Masking confidential customer information
:  You can now mask the confidential customer information in an action by marking the variables as private. The feature for masking the confidential customer information is available only for actions in assistants with the `stateful` endpoint. For more information, see [Using variables to manage conversation information](/docs/watson-assistant?topic=watson-assistant-manage-info) and [Protecting the privacy of the customer information](/docs/watson-assistant?topic=watson-assistant-collect-info#protect-privacy-customer-information).

Editing and Visualization
:  After you create an action, you now have the choice to switch from the step edit view to a new visualization that displays a canvas with a flow chart of the action. Within the canvas you can pan and zoom. This visualization of an action is currently in beta. See [Visualizing the flow of the action](/docs/watson-assistant?topic=watson-assistant-build-actions-overview) for more information. 

## 18 October 2023
{: #watson-assistant-oct182023}
{: release-note}

Unrecognized requests analysis for new languages
:  The unrecognized requests analysis is now available for two more languages, Spanish and Brazilian Portuguese. You can access this only for assistants on IBM Cloud if you are in the Plus or higher plan. For more information, see [Use unrecognized requests to get action recommendations](/docs/watson-assistant?topic=watson-assistant-analytics-recognition).

Improvements to dialog search
:   When you search intents, entities, and dialog nodes, accuracy is improved and sensitivity is adjusted. Now, the language matches the language of the created resources for highest accuracy. For example, searching for Japanese keywords should be done in a v1 workspace or v2 dialog with Japanese as the language set. A potential workaround is to allow partial matches. Also, searches are for exact matches, so the search engine is sensitive to underscores (_) and extra spaces in the keyword.

## 8 October 2023
{: #watson-assistant-oct082023}
{: release-note}

Introducing {{site.data.keyword.conversationshort}}
:   {{site.data.keyword.assistant_classic_full}} is renamed. It is now called {{site.data.keyword.conversationfull}}.

## 25 August 2023
{: #watson-assistant-aug252023}
{: release-note}

Setting for when to use **No matches**
:   You can use a new global setting for actions to change how often your assistant routes customers to the **No matches** action. By setting this threshold, you can affect when the assistant fetches answers from a search integration, triggers the *Fallback* action, or switches topics. For more information, see [When the assistant can't understand your customer's request](/docs/watson-assistant?topic=watson-assistant-handle-errors#no-action-matches).

## 24 August 2023
{: #watson-assistant-aug242023}
{: release-note}

See who last edited a collection or action
:   Starting with this release, you can see who last edited a collection or action. On the Actions page, you can hover on the values in the Last edited column to see the email address of the person who last modified the collection or action. This information is available for edits as of August 24, 2023.

Change to response mode default settings
:    As of this release, the default settings for *Step validation attempts before offering support* have changed. In *Clarifying* mode, the default is now 2 instead of 1. In *Confident* mode, the default is now 4 instead of 3. For Enterprise plans, the customization choices are now 2 times, 3 times, and 4 times instead of 1 time, 2 times, and 3 times. For more information, see [Response modes](/docs/watson-assistant?topic=watson-assistant-action-response-modes).

Change to id values in multilingual downloads for translation
:   As of this release, there is a change to the `id` values in the multilingual downloads for translation. If you have used the multilingual download before, you need to download a new CSV file to match the IDs in your assistant. For more information, see [Using multilingual downloads for translation](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-multilingual).

## 10 August 2023
{: #watson-assistant-aug102023}
{: release-note}
Algorithm version **Beta** provides improved intent detection and action matching for more languages
:   The algorithm version **Beta** now provides improved intent detection and action matching for Arabic, Chinese (Simplified), Chinese (Traditional), Czech, Dutch, Italian, Japanese, and Korean. It includes a new foundation model that is trained using a transformer architecture to improve intent detection and action matching.

   Improvements include:
   - Improved robustness to variations in user inputs such as typos and different inflection forms
   - Less training data required to reach the same level of performance compared to previous algorithms

   For more information, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version)

Session history variable
:   You can record a summary of the recent messages from a conversation for each customer, for use with the `session_history` variable. Session history might be used to provide a summary of the conversation to a live agent during a transfer or call a generative AI extension to generate an answer based on a summary. For more information, see [Session history](/docs/watson-assistant?topic=watson-assistant-publish-overview#publish-overview-environment-settings-session-history).

## 3 August 2023
{: #watson-assistant-aug032023}
{: release-note}

Synonym recommendations discontinued
:   Synonym recommendations for entities, in the classic experience for dialog skills, are discontinued as of this release.

## 27 July 2023
{: watson-assistant-jul272023}
{: release-note}

Trigger word detected action is now generally available
:   Use the **Trigger word detected** action to add words or phrases to two separate groups. The first group connects customers with an agent, when it’s important for a customer to speak with a live agent rather than activate any further actions. The second group shows customers a customizable warning message, used to discourage customers from interacting with your assistant in unacceptable ways, such as using profanity. This action is included with all new assistants created as of February 2, 2023. This was a beta feature that is now generally available. For more information, see [Detecting trigger words](/docs/watson-assistant?topic=watson-assistant-trigger-phrases).

Action conditions are now generally available
:   An action condition is a Boolean test, based on some runtime value; the action runs only if the test evaluates as true. This test can be applied to any variable. By defining action conditions, you can do things such as control user access to actions or create date-specific actions. This was a beta feature that is now generally available. For more information, see [Adding conditions to an action](/docs/watson-assistant?topic=watson-assistant-action-conditions).

New expression method to sort arrays
:   The new [`Array.sort()`](/docs/watson-assistant?topic=watson-assistant-expression-methods-actions&locale=en#expression-methods-actions-arrays-sort) method does an in-place sorting and returns the sorted array.

## 24 July 2023
{: #watson-assistant-jul242023}
{: release-note}

OAuth 2.0 custom flow support for extensions
:   Any grant type that starts with `x-` is supported for OAuth 2.0 authentication. For more information, see [Preparing the API definition](/docs/watson-assistant?topic=watson-assistant-build-custom-extension#build-custom-extension-openapi-file) and [OAuth 2.0 Authentication](/docs/watson-assistant?topic=watson-assistant-add-custom-extension#add-custom-extension-oauth).

## 20 July 2023
{: #watson-assistant-jul202023}
{: release-note}

Action and collection names must now be unique
:   With this release, each action name must be different from other actions, and each collection name must be different from other collections. If your existing actions or collections have duplicate names, a warning icon appears in the Status column. For more information, see [Overview: Editing actions](/docs/watson-assistant?topic=watson-assistant-build-actions-overview) and [Organizing actions in collections](/docs/watson-assistant?topic=watson-assistant-collections).

## 14 July 2023
{: #watson-assistant-jul142023}
{: release-note}

Multiple responses when customizing validation
:    When you edit validation for a customer response, you can now include several validation responses. For more information, see [Customizing validation for a response](/docs/watson-assistant?topic=watson-assistant-handle-errors#customize-validation).

Fallback choice for dynamic options
:   The *dynamic options* response type now includes a fallback static choice, such as `None of the above`, if the options aren't what the customer wants. You can then add a step that is conditioned on this static option to provide further assistance. For more information, see [Dynamic options](/docs/watson-assistant?topic=watson-assistant-dynamic-options).

Allow change of topic between actions and dialog
:   If you are using actions and dialog, there is a new setting you can use to ensure that customers can change topics between an action and a dialog node. For more information, see [Allow change of topic between actions and dialog](/docs/watson-assistant?topic=watson-assistant-change-topic#change-topic-action-to-dialog).

Use multilingual downloads for translation
:   You can enable the download of language data files, in CSV format, so you can translate training examples and assistant responses into other languages and use in other assistants. For more information, see [Using multilingual downloads for translation](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-multilingual).

## 12 July 2023
{: #watson-assistant-jul122023}
{: release-note}
Algorithm version **Beta** provides improved intent detection and action matching for more languages
:   The algorithm version **Beta** now provides improved intent detection and action matching for French, German, Portuguese (Brazilian), and Spanish. It includes a new foundation model that is trained using a transformer architecture to improve intent detection and action matching.

   Improvements include:
   - Improved robustness to variations in user inputs such as typos and different inflection forms
   - Less training data required to reach the same level of performance compared to previous algorithms

   For more information, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version)

## 10 July 2023
{: #watson-assistant-jul102023}
{: release-note}

Change to message API
:   When debug is enabled on the runtime (`/message`) API call, if a dialog processing error happens, more output is presented within the `output.debug.log_messages` attribute.

## 7 July 2023
{: #watson-assistant-jul072023}
{: release-note}

SpEL expression of type `intents[i].confidence` is deprecated in actions
:   On or after July 10, 2023, this expression will evaluate to -1 with a warning log message. On or after July 17, 2023, usage of this expression will be removed and will result in an error.

## 21 June 2023
{: #watson-assistant-jun212023}
{: release-note}

Autolearning now available for all languages
:   Autolearning is now generally available for all languages and enabled by default in all new assistants. Your assistant can learn from interactions with your customers and improve responses. For more information, see [Using autolearning to improve assistant responses](/docs/watson-assistant?topic=watson-assistant-autolearn).

See which actions use a specific variable
:   The Variables page now includes a new *Actions count* column. You can click on the number in the column to see which actions use a variable. For more information, see [Creating a session variable](/docs/watson-assistant?topic=watson-assistant-manage-info#create-session-variable).

Expression editor character limit increased
:   The character limit in the expression editor has increased from 1,024 to 4,000. For more information, see [Writing expressions](/docs/watson-assistant?topic=watson-assistant-expressions).

## 15 June 2023
{: #watson-assistant-jun152023}
{: release-note}

New API version 
:   The current API version is now 2023-06-15. This version introduces the following changes:
   - Invalid expressions in callouts to client actions are now replaced with empty strings
   - The default value of `async_callout` changes from `true` to `false`

Custom extensions now support OAuth 2.0 authentication
:   You can now use OAuth 2.0 authentication when you build and add custom extensions. For more information, see [Building a custom extension](/docs/watson-assistant?topic=watson-assistant-build-custom-extension) and [Adding an extension to your assistant](/docs/watson-assistant?topic=watson-assistant-add-custom-extension).

## 8 June 2023
{: #watson-assistant-jun082023}
{: release-note}

Edit step titles
:  You can now add and edit titles for each step, which can help you more easily identify what a step does in an action. For more information, see [Editing actions](/docs/watson-assistant?topic=watson-assistant-build-actions-overview).

New message when deleting a subaction
:   If you delete an action that is a subaction, there is a new message that lists all the actions that call the subaction and asks you to confirm the deletion. The message helps you preserve dependencies between actions and subactions.

## 5 June 2023
{: #watson-assistant-jun052023}
{: release-note}

Filtering the list of actions
:   You can locate specific actions by filtering the list by subactions, by custom extension, or by variable. For more information, see [Filtering actions](/docs/watson-assistant?topic=watson-assistant-filter-actions).

## 29 May 2023
{: #watson-assistant-may292023}
{: release-note}

New expression choice for setting a session variable
:   Previously, to use an expression to set or modify a variable value, you needed to pick an existing variable or create a new one and select the expression option. Now you can use a new **Expression** choice to write an expression directly without first picking a variable. For more information, see [Storing a value in a session variable](/docs/watson-assistant?topic=watson-assistant-manage-info#store-session-variable).

Changes to validation of OpenAPI specifications 
:   When you build a custom extension, you work with OpenAPI specification files. This release includes changes to the validation of OpenAPI files, which might affect the connection between your actions and extensions 

   You can import an action with references to a custom extension and {{site.data.keyword.conversationshort}} can automatically connect the action and extension. With the validation change, modifications to the OpenAPI specification for your custom extension might affect this automatic connection. For more information, see [Building a custom extension](/docs/watson-assistant?topic=watson-assistant-build-custom-extension).

## 22 May 2023
{: #watson-assistant-may222023}
{: release-note}

Changes to the date and number formats in assistant responses
:   Beginning 22 May 2023, customers might see changes to the date and number formats in assistant responses.

   Examples of date changes include removed or added periods, such as:
   -  In Spanish, `18 abr. 2021` changes to `18 abr 2021`
   -  In Portuguese, `18 de abr` changes to `18 de abr.`

   The delimiter character changes for numbers in some languages. For example, in French, nonbreaking space (NBSP) changes to narrow no-break space (NNBSP).

   These changes are the result of migrating the {{site.data.keyword.conversationshort}} platform to Java 17, where locale values are updated by using specifications in [CLDR 39](https://cldr.unicode.org/index/downloads/cldr-39). 
   
   To avoid or minimize the impact of similar changes in the future, you can use [Display formats](/docs/watson-assistant?topic=watson-assistant-actions-global-settings#actions-global-settings-display-formats).

## 18 May 2023
{: #watson-assistant-may182023}
{: release-note}

Differences in contextual entity detection for dialog skills with few annotations
:   If you have 10 to 20 examples of contextual entities in your dialog skill, you might see differences in the entities detected due to updates made to address critical vulnerabilities. The impact of these differences is limited to only newly-trained models. Existing models are unaffected. You can mitigate these differences by annotating more examples. For more information, see [Annotation-based method](/docs/watson-assistant?topic=watson-assistant-entities#entities-annotations-overview).

## 17 May 2023
{: #watson-assistant-may172023}
{: release-note}

Display iframe inline
:   In the web chat, there are now two ways an iframe response can be included:
   - As a preview card that describes the embedded content. Customers can click this card to display the frame and interact with the content.
   - Inline, meaning within the conversation. This new option is good for smaller pieces of iframe content.

   For more information, see [Adding an iframe response](/docs/watson-assistant?topic=watson-assistant-respond#respond-add-iframe).

## 15 May 2023
{: #watson-assistant-may152023}
{: release-note}

Change to dialog skill context variables named `request`
:   If your dialog skill used a context variable that is named `request`, it was removed from the response payload of any `/message` calls in the V1 or V2 API, or through the {{site.data.keyword.conversationshort}} user interface. After 15 May 2023, this behavior changes. Your assistant doesn't remove context variables that are named `request` from the response payload anymore.

## 5 May 2023
{: #watson-assistant-may052023}
{: release-note}

New validation choices for date, time, and numeric customer responses
:   For *Number*, *Date*, *Time*, *Currency*, and *Percentage* customer responses, you can now customize the validation to check for a specific answer, such as a range of dates or a limited currency amount. For more information, see [Customizing validation for a response](/docs/watson-assistant?topic=watson-assistant-handle-errors#customize-validation).

## 3 May 2023
{: #watson-assistant-may032023}
{: release-note}

Algorithm version **Beta** provides improved intent detection and action matching
:   The algorithm version **Beta** now provides improved intent detection and action matching. It includes a new foundation model that is trained using a transformer architecture to improve intent detection and action matching for English.

   Improvements include:
   - Improved robustness to variations in user inputs such as typos and different inflection forms
   - Less training data required to reach the same level of performance compared to previous algorithms

   For more information, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

## 24 April 2023
{: #watson-assistant-apr242023}
{: release-note}

Response modes randomization behavior 
:   The response modes beta now uses the same randomization behavior during clarification that your actions have without response modes enabled. Previous to this change, when response modes were enabled, the clarification feature no longer periodically modified the options for clarification. Randomizing the clarification helps prevent bias that can be introduced by a percentage of people who always pick the first option without carefully reviewing all of their choices beforehand. For more information, see [Response modes](/docs/watson-assistant?topic=watson-assistant-action-response-modes) or [Asking clarifying questions](/docs/watson-assistant?topic=watson-assistant-understand-questions#understand-questions-ask-clarifying-question).

## 21 April 2023
{: #watson-assistant-apr212023}
{: release-note}

Collections
:   You can use a *collection* to organize your actions. You can put actions into folder-style groups based on whatever categorization you need at your organization, such as by use case, internal team, or status. For more information, see [Organizing actions in collections](/docs/watson-assistant?topic=watson-assistant-collections).

## 18 April 2023
{: #watson-assistant-apr182023}
{: release-note}

Activity log
:   The **Activity log** is a beta feature that is available for evaluation and testing. Use the activity log to track changes. It gives you visibility into the modifications that are made to your assistant. It is available for Plus plans and higher. For more information, see [Activity log](/docs/watson-assistant?topic=watson-assistant-activity-log).

## 16 April 2023
{: #watson-assistant-apr162023}
{: release-note}

Allow changing topics in free text and regex responses
:   By default, customers can't change topics when the assistant is asking for a free text response or when an utterance matches the pattern in a regex response. Now free text and regex customer response types have a setting to allow a user to digress and change topics. For more information, see [Enabling changing the topic for free text and regex customer responses](/docs/watson-assistant?topic=watson-assistant-change-topic#change-topic-free-text-regex).

Autolearning beta for dialog removed
:   As of this release, the *autolearning* beta has been removed from the **Analytics** section in dialog. You can use actions to test a new and improved autolearning beta. For more information, see [Using autolearning to improve assistant responses](/docs/watson-assistant?topic=watson-assistant-autolearn).

## 7 April 2023
{: #watson-assistant-apr072023}
{: release-note}

Never return choice when customer changes topics
:   If a customer changes a topic during a conversation, there might be some situations when you might not want them to return to the previous action. If you need to do this, a new **Never return** choice is available in **Action settings**. For more information, see [Disabling returning to the original topic](/docs/watson-assistant?topic=watson-assistant-change-topic#change-topic-never-return).

## 22 March 2023
{: #watson-assistant-mar222023}
{: release-note}

Autolearning
:   **Autolearning** is a beta feature that is available for evaluation and testing purposes in English-language assistants only. Use autolearning to enable your assistant to learn from interactions with your customers and improve responses. For more information, see [Using autolearning to improve assistant responses](/docs/watson-assistant?topic=watson-assistant-autolearn).

## 21 March 2023
{: #watson-assistant-mar212023}
{: release-note}

Response modes
:   **Response modes** is a beta feature that is available for evaluation and testing purposes. Choose a default *response mode*, which modifies the assistant's behavior when asking clarifying questions. For more information, see [Response modes](/docs/watson-assistant?topic=watson-assistant-action-response-modes).

## 20 March 2023
{: #watson-assistant-mar202023}
{: release-note}

Auto-save setting removed from Global Settings
:  The **Auto-save** setting was removed from Global Settings. It was a user preference that allowed you to disable automatic saving of actions and applied to all assistants in your instance. Changing the setting applied only to you and didn't affect other users. Actions continue to be automatically saved as you work. For more information, see [Saving your actions](/docs/watson-assistant?topic=watson-assistant-save-actions).

## 16 March 2023
{: #watson-assistant-mar162023}
{: release-note}

New algorithm version **Latest (20 Dec 2022)** provides improved irrelevance detection 
:   A new algorithm version is available. The **Latest (20 Dec 2022)** version includes a new irrelevance detection implementation to improve off-topic detection accuracy.

   Improvements include:
   - Relevant user inputs are expected to get higher confidence, so they are less likely to be considered irrelevant or require clarification
   - Irrelevance detection is improved in the presence of direct entity references
   - Irrelevance detection is more stable across small changes to input
   - Intent detection is more stable regarding occurrence of numerics, such as postal codes
   - For German-language assistants, intent detection is more robust in the presence of umlauts 

   This algorithm was first introduced as the **Beta** version in June 2022. Since then, support for more languages has been added. This algorithm version was stabilized in December 2022 with minor enhancements since that time.

   With this new release, the June 1, 2022 version is now labeled as **Previous (01 Jun 2022)**. The oldest release labeled as **01 Jan 2022** is no longer available for training. As of now, the new **Beta** version has the same behavior as the **Latest (20 Dec 2022)** version. Updates to the **Beta** version will be released soon.

   For more information, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

## 10 March 2023
{: #watson-assistant-mar102023}
{: release-note}

Dialog session variables now available in Preview
:   If you are using dialog in {{site.data.keyword.conversationshort}}, you can now see session variables for dialog when debugging in Preview. For more information, see [Variable values in Preview](/docs/watson-assistant?topic=watson-assistant-review#review-variable-values).

## 6 March 2023
{: #watson-assistant-mar062023}
{: release-note}

Improvements to algorithm version beta
:   Improvements to the current *Beta* algorithm version include:
   - Relevant examples are expected to get higher confidence
   - For Spanish-language assistants, intent detection is improved in the presence of direct entity references
   - Intent detection is more stable regarding occurrence of numerics, such as postal codes
   - Intent detection now accounts for fuzzy closed entity mentions
   - For German-language assistants, intent detection is more robust in the presence of umlauts 

   For more information, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

## 3 March 2023
{: #watson-assistant-mar032023}
{: release-note}

Adding and using multiple environments
:   Each assistant has a draft and live environment. For Enterprise plans, you can now add up to three environments as a staging area to test your assistant before deployment. You can build content in the draft environment and test versions of your content in the extra environments. For more information, see [Adding and using multiple environments](/docs/watson-assistant?topic=watson-assistant-multiple-environments).

Confirmation to return to previous action
:   If a customer digresses and changes to a new topic, assistants now ask a "yes or no" confirmation question that the customers want to return to the previous action. Previously, the assistant returned to the previous action without asking. New assistants are set to use this confirmation by default. For more information, see [Confirmation to return to previous topic](https://test.cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-change-topic#change-topic-confirmation).

## 1 March 2023
{: #watson-assistant-mar012023}
{: release-note}

Unrecognized requests group names
:   This change improves the group names for unrecognized requests. For groups with examples phrased in the form of question, the group name can be more indicative of a question rather than a request. For more information, see [Use unrecognized requests to get action recommendations](/docs/watson-assistant?topic=watson-assistant-analytics-recognition).

## 23 February 2023
{: #watson-assistant-feb232023}
{: release-note}

Private variables excluded from logs
:   Private context variables are no longer saved in logs or sent to external services using log webhooks. Private variables are any values stored inside the following objects:

    - `context.integrations.*.private` (accessible from actions as `system_integrations.*.private`)
    - `context.integrations.*.$private`
    - `context.skills.*.user_defined.private`
    - `context.skills.*.user_defined.$private`
    - `context.private`
    - `context.$private`

## 16 February 2023
{: #watson-assistant-feb162023}
{: release-note}

Improvements to setting variable values
:   When you use **Set variable values** on an action step:

   - The available choices now match by type. For example, if you want to set a date variable, the choices are limited to other date variables. Previously, all variables of all types were listed as choices. 
   
   - You can set a scalar value for each variable type. For example, you can set a specific date for a date variable or set a specific number for a number variable.

   For more information, see [Storing a value in a session variable](/docs/watson-assistant?topic=watson-assistant-manage-info#store-session-variable).

Confirmation and free text response types setting default 
:   The *Confirmation* and *Free text* response types are now set to **Always ask for this information** by default. For more information, see [Skipping steps, always asking steps, or never asking steps](/docs/watson-assistant?topic=watson-assistant-collect-info#collect-info-skip-step).

## 13 February 2023
{: #watson-assistant-feb132023}
{: release-note}

Response variations
:   In actions, you can add *response variations* so that your assistant can respond to the same request in different ways. You can choose to rotate through the response variations sequentially or in random order. For more information, see [Adding variations](/docs/watson-assistant?topic=watson-assistant-respond#respond-variations).

Microsoft Teams integration
:   A [Microsoft Teams integration](/docs/watson-assistant?topic=watson-assistant-deploy-microsoft-teams) is now available to connect your assistant with the people, content, and tools that your business or community needs to chat, call, and collaborate. 

## 3 February 2023
{: #watson-assistant-feb032023}
{: release-note}

Action conditions (beta)
:   An action condition is a boolean test, based on some runtime value; the action executes only if the test evaluates as true. This test can be applied to any variable. By defining action conditions, you can do things such as control user access to actions or create date-specific actions. This is a beta feature that is available for evaluation and testing purposes. For more information, see [Adding conditions to an action](/docs/watson-assistant?topic=watson-assistant-action-conditions).

## 2 February 2023
{: #watson-assistant-feb022023}
{: release-note}

Detect trigger words (beta)
:   Use the **Trigger word detected** action to add words or phrases to two separate groups. The first group connects customers with an agent, when it’s important for a customer to speak with a live agent rather than activate any further actions. The second group shows customers a customizable warning message, used to discourage customers from interacting with your assistant in unacceptable ways, such as using profanity. This action is included with all new assistants created as of this date. This is a beta feature that is available for evaluation and testing purposes. For more information, see [Detecting trigger words](/docs/watson-assistant?topic=watson-assistant-trigger-phrases).

Changes to unrecognized requests algorithm
:   In **Analyze**, the **Recognition** page lets you view groups of similar unrecognized requests. You can use the requests as example phrases in new or existing actions to address questions and issues that aren't being answered by your assistant. With this release, the criteria for grouping the requests is relaxed for customers with lesser amounts of data. Also, the group names have been improved with better grammar and to be more representative of the requests. For more information, see [Use unrecognized requests to get action recommendations](/docs/watson-assistant?topic=watson-assistant-analytics-recognition).

## 1 February 2023
{: #watson-assistant-feb012023}
{: release-note}

Actions templates updated with new design and new choices
:   The actions template catalog has a new design that lets you select multiple templates at the same time. It also has new and updated templates, including starter kits you can use with external services such as Google and HubSpot. For more information, see [Building actions from a template](/docs/watson-assistant?topic=watson-assistant-actions-templates).

## 26 January 2023
{: #watson-assistant-jan262023}
{: release-note}

Display formats for variables
:   In **Global settings** for actions, **Display formats** lets you specify the display formats for variables that use date, time, numbers, currency, or percentages. You can also choose a default locale to use if one isn't provided by the client application. This lets you make sure that the format of a variable that's displayed in the web chat is what you want for your assistant. For example, you can choose to have the output of a time variable appear in HH:MM format instead of HH:MM:SS. For more information, see [Display formats](/docs/watson-assistant?topic=watson-assistant-actions-global-settings#actions-global-settings-display-formats).

Intent recommendations and intent user example recommendations discontinued
:   As of this release, intent recommendations and intent user example recommendations are discontinued in dialog skills in the classic experience. **Intent recommendations** has been removed from the **Intents** page and **Recommended examples** has been removed from intents. You can [use unrecognized requests to get action recommendations](/docs/watson-assistant?topic=watson-assistant-analytics-recognition).

## 18 January 2023
{: #watson-assistant-jan182023}
{: release-note}

Algorithm version stability improvement
:   As of this date, the **Latest (01 Jun 2022)** and **Beta** algorithm versions now have more stable behavior across retrained models, in the presence of overlapping entities (the same entity value belonging to more than one entity type). Previously, when there were overlapping entities definitions, confidences could differ across different retraining. With this improvement, you can expect to see similar confidences. For more information, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

## 12 January 2023
{: #watson-assistant-jan122023}
{: release-note}

Autocorrection setting for actions
:   The **Global settings** for actions now include an **Autocorrection** setting. *Autocorrection* fixes misspellings that users make in their requests. The corrected words are used to match to an action. 

   While the setting is new, the autocorrection feature was already used automatically by all English-language assistants. Autocorrection is also available in French-language assistants, but is disabled by default. The autocorrection setting isn't available for any other languages. The new setting lets you disable or enable autocorrection if necessary.

   For more information, see [Autocorrecting user input](/docs/watson-assistant?topic=watson-assistant-autocorrection).

Improved experience when setting a variable value
:   The dropdown list for setting a variable value within an action step has a new organization. The new list is intended to provide an improved experience.

## 11 January 2023
{: #watson-assistant-jan112023}
{: release-note}

Algorithm version 01-Jun-2022 uses enhanced intent detection by default
:   As of this date, the algorithm version **Latest (01-Jun-2022)** now uses enhanced intent detection by default. Before this change, some skills that did not include a specific algorithm version selection inadvertently used **Previous (01-Jan-2022)**. You can notice small changes in intent detection behavior when changes are made to an assistant that previously didn't have enhanced intent detection enabled. For more information, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

## 6 December 2022
{: #watson-assistant-dec062022}
{: release-note}

Updated expression methods
:   The following new and updated methods are available in expressions:
   - The [`Array.joinToArray()`](/docs/watson-assistant?topic=watson-assistant-expression-methods-actions#expression-methods-actions-arrays-join-to-array) method now supports a new boolean parameter you can use to specify that the data type of values from the input array should be preserved in the returned array.
   - The new [`String.toJson()`](/docs/watson-assistant?topic=watson-assistant-expression-methods-actions#expression-methods-actions-strings-toJson) method parses a string containing JSON data and returns a JSON object or array. This method is supported in both actions and dialog.

## 5 December 2022
{: #watson-assistant-dec052022}
{: release-note}

Unsupported HTML removed from text responses in channel integrations
:   HTML tags (except for links) are now automatically removed from text responses that are sent to the Facebook, WhatsApp, and Slack integrations, because those channels do not support HTML formatting. HTML tags are still handled appropriately in channels that support them (such as the web chat) and stored in the session history.

## 2 December 2022
{: #watson-assistant-dec022022}
{: release-note}

Pause response type
:   Use a *Pause* response to have your assistant wait for a specified interval before displaying the next response. This pause might be to allow time for a request to complete, or simply to mimic the appearance of a live agent who might pause between responses. The pause can be of any duration from 1 to 10 seconds. For more information, see [Pause response](/docs/watson-assistant?topic=watson-assistant-respond#respond-pause-response).

## 17 November 2022
{: #watson-assistant-nov172022}
{: release-note}

Use unrecognized requests to get action recommendations
:   In **Analyze**, the new **Recognition** page lets you view groups of similar unrecognized requests. You can use the requests as example phrases in new or existing actions to address questions and issues that aren't being answered by your assistant. For more information, see [Use unrecognized requests to get action recommendations](/docs/watson-assistant?topic=watson-assistant-analytics-recognition).

## 15 November 2022
{: #watson-assistant-nov152022}
{: release-note}

Journeys
:   Beginning with web chat version 6.9.0, you can now create _journeys_ to guide your customers through tasks they can already complete on your website. A journey is an interactive, multipart response that can combine text, video, and images, presented in sequence in a small window superimposed over your website.

    Journeys are available as a beta feature. For more information, see [Guiding customers with journeys](/docs/watson-assistant?topic=watson-assistant-journeys).

## 10 November 2022
{: #watson-assistant-nov102022}
{: release-note}

Dynamic options
:   Within the options customer response, you can use the **dynamic** setting to generate the list when you need to ask questions that are potentially different each time and for each customer. You need to set up a list variable as the source of the options. For more information, see [Dynamic options](/docs/watson-assistant?topic=watson-assistant-dynamic-options).

Extension inspector
:   You can use the new extension inspector in the action editor **Preview** pane to debug problems with custom extensions. The extension inspector shows detailed information about what data is being sent to and returned from an external API. For more information, see [Debugging failures](/docs/watson-assistant?topic=watson-assistant-call-extension#extension-debug).

## 3 November 2022
{: #watson-assistant-nov032022}
{: release-note}

Never ask a step
:   There may be some situations where you need a step to never ask a question because you anticipate there might be redundant questions in the conversation. A new setting, **Never ask**, is now available for any step that expects a customer response. For more information, see [Skipping steps, always asking steps, or never asking steps](/docs/watson-assistant?topic=watson-assistant-collect-info#collect-info-skip-step).

Action notes
:   You can now add free-form notes to each action. Within each action, you can use **Action notes** to add a description, documentation, comments, or any other annotations to help you keep track of your work as you build an action. For more information, see [Using the action editor](/docs/watson-assistant?topic=watson-assistant-build-actions-overview#build-actions-overview-use).

Variable values in Preview
:  Viewing action variables in Preview has been improved. Now you can see the history of all action variables, rather than one action at a time. For more information, see [Variable values](/docs/watson-assistant?topic=watson-assistant-review#review-variable-values).

## 21 October 2022
{: #watson-assistant-oct212022}
{: release-note}

Algorithm version updates
:   The algorithm version setting for both actions and dialog now includes three choices: beta, latest, and previous. For more information, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

## 12 October 2022
{: #watson-assistant-oct122022}
{: release-note}

`now(String timezone)` method output includes time zone offset
:   The string returned from the `now(String timezone)` method now includes the time zone offset (such as `-05:00`). The new format is `yyyy-MM-dd HH:mm:ss 'GMT'XXX` (where `XXX` represents the time zone offset). This change enables accurate time zone computations when used with other date and time methods such as `before`, `after`, and `reformatDateTime`.

    If you have an existing action or dialog that depends on the previous format, you can adapt it by reformatting the output using `now(timezone).reformatDateTime('yyyy-MM-dd HH:mm:ss')`.
    
    For more information, see [Expression language methods for actions](/docs/watson-assistant?topic=watson-assistant-expression-methods-actions#expression-methods-actions-now).

## 23 September 2022
{: #watson-assistant-sep232022}
{: release-note}

Upload an image as a preview background
:   On the **Preview** page, you can now upload an image of your organization's website as a background. For more information, see [Previewing and sharing your assistant](/docs/watson-assistant?topic=watson-assistant-preview-share).

## 16 September 2022
{: #watson-assistant-sep162022}
{: release-note}

Session ID information on Analyze page
:   Session ID information for conversations is now displayed on the Conversations tab of the Analyze page. You can also filter customer conversation data by the session ID. From the Conversations tab of the Analyze page, use the Keyword filter to search by session ID. For more information, see [Filtering conversations](/docs/watson-assistant?topic=watson-assistant-analytics-conversations#analytics-conversations-filtering).

   The ability to filter on session ID has limited support for conversations that occurred before this feature release. For all conversations that occurred before 16 September 2022, you can filter only by a single session ID at a time.

## 12 September 2022
{: #watson-assistant-sep122022}
{: release-note}

Fix for fuzzy matching in German
:   In some cases, German closed entities were incorrectly matching shorter values over longer values. For example, suppose that you defined two entity values, `Pflege` and `Pflegegeld` in one entity. If a customer accidentally input `Pflegegelb`, the assistant would incorrectly match with `Pflege` rather than `Pflegegeld`.

   With this fix, the `Pflegegelb` input value would correctly match `Pflegegeld`, not `Pflege`. For more information, see [How fuzzy matching works](/docs/watson-assistant?topic=watson-assistant-entities#entities-fuzzy-matching).

## 9 September 2022
{: #watson-assistant-sep092022}
{: release-note}

New operators available for building conditions
:   Several new operators are available for building conditions in your actions. The options response type now has the `is any of` and `is none of` operators available. For more information, see [Operators](/docs/watson-assistant?topic=watson-assistant-step-conditions#step-conditions-operators).

Copy actions to other assistants
:   You can copy an action from one assistant to another. When you copy an action, references to other actions, variables, and saved responses are also copied. For more information, see [Copying an action to another assistant](/docs/watson-assistant?topic=watson-assistant-copy-action).

Filter variables and saved responses by name
:   You can now find variables and saved responses more easily. On the Actions page, you can filter variables you created or saved responses you added. Click the search icon, then enter a search string. Your list of variable or saved responses filters to match what you enter.

## 1 September 2022
{: #watson-assistant-sep012022}
{: release-note}

Conditioning on days of the week
:   You can now condition a step on days of the week. This feature is available with the _date_ response type and the _Current date_ built-in variable.

    For example, you might [define a customer response](/docs/watson-assistant?topic=watson-assistant-collect-info#choose-type) in step 1 with the date response type. When the customer responds to that step, they choose a date. You can then condition a later step on whether the date that the customer chose is Wednesday.

New operators available for building conditions
:   Several new operators are available for building conditions in your actions. The free text response type now has the `contains`, `does not contain`, `matches`, and `does not match` operators available. For more information, see [Operators](/docs/watson-assistant?topic=watson-assistant-step-conditions#step-conditions-operators).

Extensions support for arrays
:   Custom extensions now support passing arrays as parameters and accessing arrays in response variables. For more information, see [Calling a custom extension](/docs/watson-assistant?topic=watson-assistant-call-extension).

## 26 August 2022
{: #watson-assistant-aug262022}
{: release-note}

New filter on the Analyze page
:   You can now filter customer conversation data by the _Greet customer_ system action. From the Conversations tab of the Analyze page, open the Actions filter and select **Greet customer**. For more information, see [Filtering conversations](/docs/watson-assistant?topic=watson-assistant-analytics-conversations#analytics-conversations-filtering).

Filter actions by name
:   You can now find actions more easily. On the Actions page, you can filter actions by name. Click the search icon, then enter a search string. Your list of actions filters to match what you enter.

## 12 August 2022
{: #watson-assistant-aug122022}
{: release-note}

Actions templates
:   When creating actions, you can choose a template that relates to the problem you’re trying to solve. Templates help tailor your actions to include items specific to your business need. The examples in each template can also help you to learn how actions work. Actions templates include features such as intents, entities, condition-based responses, synonyms, response validations, and agent fallback. For more information, see [Building actions from a template](/docs/watson-assistant?topic=watson-assistant-actions-templates).

Channel name variable
:   The `Channel name` integration variable lets you add step conditions using these channels: web chat, phone, SMS, WhatsApp, Slack, or Facebook Messenger. For more information, see [Adding conditions to a step](/docs/watson-assistant?topic=watson-assistant-step-conditions).

## 11 August 2022
{: #watson-assistant-aug112022}
{: release-note}

Algorithm version options available in more languages
:   Algorithm version options are now available in Arabic, Czech, and Dutch. This allows you to choose which {{site.data.keyword.conversationshort}} algorithm to apply to your future trainings. For more information, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

## 9 August 2022
{: #watson-assistant-aug092022}
{: release-note}

New API methods
:   The v2 API now supports new **Environments** and **Releases** methods:

    - **Environments**: Retrieve information about the environments associated with an assistant.

    - **Releases**: Retrieve information about the releases (versions) that have been published for an assistant, and assign an available release to an environment.

For more information, see the v2 [API Reference](https://{DomainName}/assistant/assistant-v2){: external}.

## 5 August 2022
{: #watson-assistant-aug052022}
{: release-note}

Initial value of session variables
:   You can now set the initial value of a session variable to an expression. For more information, see [Creating a session variable](/docs/watson-assistant?topic=watson-assistant-manage-info#create-session-variable).

Uploading intents
:   If you created intents in the classic experience, you can migrate your intents to actions in {{site.data.keyword.conversationshort}}. This can provide a helpful starting point when you are ready to start building actions. For more information, see [Uploading intents as actions](/docs/watson-assistant?topic=watson-assistant-upload-download-actions#upload-download-actions-upload-intents).

## 19 July 2022
{: #watson-assistant-jul192022}
{: release-note}

Changes to publishing and environments
:   You can now publish versions of your content without assigning to the live environment, allowing you to make continuous updates before customers see it in production. Also, the formerly separate pages for your draft and live environments now appear as tabs on a single *Environments* page, from which you can set up unique configurations for building and testing in the draft environment, and for your customers in the live environment. For more information, see the [Publishing overview](/docs/watson-assistant?topic=watson-assistant-publish-overview).

Logs reader role
:   Identity and Access Management now includes a new service role, **Logs Reader**, which lets you grant access to Analytics without assigning the Manager role. Use Logs Reader in combination with the Reader or Writer role to provide access to the Analytics page. For more information, see [Managing access](/docs/watson-assistant?topic=watson-assistant-access-control).

## 15 July 2022
{: #watson-assistant-jul152022}
{: release-note}

Segment extension
:   The Segment extension is now available for Enterprise plans. With this extension, you can use [Segment](https://segment.com/){: external} to capture and centralize data about your customers' behavior, including their interactions with your assistant. For more information, see [Sending events to Segment](/docs/watson-assistant?topic=watson-assistant-segment-add).

New expression property
:   You can now use the `.literal` property to return the exact response that a customer specifies. This property is helpful if a customer uses a synonym of an option, and you want your assistant to respond with the exact phrase they specified. To set this property, click **Set variable values** and assign a session variable to the step variable. Add the `.literal` property to the step variable. Use the session variable in the assistant's response to display the customer's input.

    For example, suppose you have an option called `plant` that has `fern` as a synonym. A customer might say `buy a fern`. In this case, you can use the `.literal` property so the assistant's response uses the customer's input. Your assistant might respond, `Great! I see you want to buy a fern.`

## 11 July 2022
{: #watson-assistant-jul112022}
{: release-note}

Ability to duplicate an action
:   You can duplicate an action to reuse information in a new action. When you duplicate an action, the new action includes everything except example phrases. Click the overflow menu on the action you want and select **Duplicate**.

New demo site
:   Explore our [interactive demo site](https://www.ibm.com/products/watson-assistant/demos/lendyr/demo.html){: external} to learn how {{site.data.keyword.conversationshort}} can be used to build powerful, scalable experiences for your users.

## 24 June 2022
{: #watson-assistant-jun242022}
{: release-note}

Algorithm version options available in more languages
:   Algorithm version options are now available in Chinese (Traditional), Japanese, and Korean. This allows you to choose which {{site.data.keyword.conversationshort}} algorithm to apply to your future trainings. For more information, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

## 16 June 2022
{: #watson-assistant-jun162022}
{: release-note}

Algorithm version
:   Algorithm version allows you to choose which {{site.data.keyword.conversationshort}} algorithm to apply to your future trainings. For more information, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

Algorithm beta version (2022-06-10)
:   Algorithm beta version (2022-06-10) includes a new irrelevance detection algorithm to improve off-topic detection accuracy. Utterances with similar meanings are expected to have more similar confidences in comparison to previous irrelevance detection algorithms. For example, the training utterance `please suggest route from times square` has 100% confidence at runtime. Currently in IBM Cloud, the utterance `please suggest route from central park` gets a low confidence and could be flagged as irrelevant. With beta version (2022-06-10), the same utterance is expected to be predicted correctly with a ~46% confidence.

## 3 June 2022
{: #watson-assistant-jun032022}
{: release-note}

Extensions support for importing API document with unsupported methods
:   When building a custom extension, you can now import an API document even if it contains operations with required array parameters, which are not supported. The unsupported operations are automatically disabled, but this does not affect other operations. (Previously, the entire API document was rejected if it contained unsupported operations.) For more information, see [Building a custom extension](/docs/watson-assistant?topic=watson-assistant-build-custom-extension).

## 27 May 2022
{: #watson-assistant-may272022}
{: release-note}

Support for custom extensions and dialog in Actions preview panel
:   You can now view your entire assistant from the **Actions preview** panel, including custom extensions and dialog. This allows you to have a complete view of how an action is working. For more information about previewing actions, see [Reviewing and debugging your actions](/docs/watson-assistant?topic=watson-assistant-review).

## 19 May 2022
{: #watson-assistant-may192022}
{: release-note}

Sign out due to inactivity setting
:   {{site.data.keyword.conversationfull}} now uses the **Sign out due to inactivity setting** from Identity & Access Management (IAM). {{site.data.keyword.cloud_notm}} account owners can select the time it takes before an inactive user is signed out and their credentials are required again. The default is 2 hours.

   An inactive user will see two messages. The first message alerts them about an upcoming session expiration and provides a choice to renew. If they remain inactive, a second session expiration message appears and they will need to log in again.

   For more information, see [Setting the sign out due to inactivity duration](/docs/account?topic=account-iam-work-sessions&interface=ui#sessions-inactivity){: external}.

## 12 May 2022
{: #watson-assistant-may122022}
{: release-note}

Ability to upload and download example phrases and upload saved customer responses
:   You can now upload and download example phrases from **Customer starts with** at the start of an action. This can be useful if you have a large number of example phrases and don't want to define them one by one. For more information, see [Adding more examples](/docs/watson-assistant?topic=watson-assistant-understand-questions#understand-questions-adding-more-examples).

   You can also now upload saved customer responses from the **Saved responses** page. For more information, see [Uploading saved customer responses](/docs/watson-assistant?topic=watson-assistant-collect-info#uploading-saved-customer-response).

   The ability to upload example phrases and saved customer responses is also helpful if you're using the classic experience and want to migrate your intents and entities to {{site.data.keyword.conversationshort}}. For more information, see [Migrating intents and entities](/docs/watson-assistant?topic=watson-assistant-migrate-intents-entities).

## 5 May 2022
{: #watson-assistant-may052022}
{: release-note}

Success/failure variable for extensions
:   Each call to a custom extension now returns a `Ran successfully` response variable, which you can use to check the success or failure of the call. For more information, see [Checking success or failure](/docs/watson-assistant?topic=watson-assistant-call-extension#extension-check-success).

## 28 April 2022
{: #watson-assistant-apr282022}
{: release-note}

Definitive calculation for abandoned actions
:   Abandonment is now definitively calculated for your actions. On the **Analytics** page, actions are no longer considered `Ongoing` in the action completion analysis. An action is considered abandoned if it was not completed after 1 hour of inactivity and doesn't meet the criteria for any other incompletion reason (escalated to agent, started a new action, or stuck on a step). This change applies only to actions data after April 26, 2022. For more information about action incompletion, see [Reasons for incompletion](/docs/watson-assistant?topic=watson-assistant-analytics-action-completion#incomplete-reasons).

Managing operations in extensions
:   When you add a custom extension to an assistant, you can now choose which operations and response properties will be available to actions. For more information, see [Adding an extension to your assistant](/docs/watson-assistant?topic=watson-assistant-add-custom-extension).

## 21 April 2022
{: #watson-assistant-apr212022}
{: release-note}

Ability to duplicate a step
:   You can now duplicate a step so you don't have to re-create variable settings and customizations. Duplicating a step is helpful when you need to add a step similar to a previous step, but with minor modifications. For more information about how to duplicate a step, see [Duplicating a step](/docs/watson-assistant?topic=watson-assistant-build-actions-overview#build-actions-overview-duplicate-step).

Markdown supported in action editor
:   The action editor now supports basic Markdown syntax. As you type, the action editor renders the Markdown so you can see the content as your customers will when they interact with the assistant.

## 5 April 2022
{: #watson-assistant-apr052022}
{: release-note}

Dialog feature available
:   The dialog feature is available. If you have a dialog-based assistant that was built using the classic experience, you can now migrate your dialog skill to {{site.data.keyword.conversationshort}}. For more information, see [Migrating to {{site.data.keyword.conversationshort}}](/docs/watson-assistant?topic=watson-assistant-migrate-overview).

## 28 March 2022
{: #watson-assistant-mar282022}
{: release-note}

New service desk support reference implementation
:   You can use the reference implementation details to integrate the web chat with the Kustomer service desk.

## 18 March 2022
{: #watson-assistant-mar182022}
{: release-note}

Custom extensions
:   If you need to integrate your assistant with an external service that has a REST API, you can now build a custom extension by importing an OpenAPI document. Your assistant can then send requests to the external service and receive response data it can use in the conversation. For example, you might use an extension to interact with a ticketing or customer relationship management (CRM) system, or to retrieve real-time data such as mortgage rates or weather conditions.

   For more information about custom extensions, see [Building a custom extension](/docs/watson-assistant?topic=watson-assistant-build-custom-extension) and [Calling a custom extension](/docs/watson-assistant?topic=watson-assistant-call-extension).

Confirmation customer response type
:   The confirmation customer response type is now available. Use this response type when a customer's response must be either Yes or No. For more information, see [Confirmation](/docs/watson-assistant?topic=watson-assistant-collect-info#customer-response-type-confirmation).

Search integration highlights text in browser
:   Search results in {{site.data.keyword.conversationshort}} include a link. Now, when a customer clicks the link, search results are highlighted in their browser so it’s easier for them to see the relevant content. This feature is supported on Chromium browsers, including Google Chrome and Microsoft Edge.

## 24 February 2022
{: #watson-assistant-feb242022}
{: release-note}

Regex customer response type
:   The regex customer response type is now available. Use this response type to capture a value that must conform to a particular pattern or format, such as an email address or telephone number. For more information, see [Regex](/docs/watson-assistant?topic=watson-assistant-collect-info#customer-response-type-regex).

## 17 February 2022
{: #watson-assistant-feb172022}
{: release-note}

Adding users from the Manage menu
:   If you want to collaborate with others on your assistants, you can now quickly add users with Administrator and Manager access from the **Manage** menu in your assistant. For more information, see [Adding users from the Manage menu](/docs/watson-assistant?topic=watson-assistant-access-control#access-control-add-users).

Preview page share link
:   When you use the **Copy link to share** button to share your assistant, the shared assistant now mirrors the Preview page. If you share the assistant with a colleague, they are able to see the assistant with any customizations that you made on the Preview page.

## 10 February 2022
{: #watson-assistant-feb102022}
{: release-note}

Links in assistant responses can be configured to open in a new tab
:   When you build an action, your assistant responses can include links. If you're using web chat, you can now control whether the link opens in a new tab. To enable a link to open in a new tab, select **Open link in new tab** from the **Insert link** configuration window. For more information, see [Adding assistant responses](/docs/watson-assistant?topic=watson-assistant-respond).

## 9 February 2022
{: #watson-assistant-feb092022}
{: release-note}

All instances now default to new experience
:    All new instances of {{site.data.keyword.conversationshort}} now direct users to the new product experience by default.

    {{site.data.keyword.conversationfull}} has been completely overhauled to simplify the end-to-end process of building and deploying a virtual assistant, reducing time to launch and enabling nontechnical authors to create virtual assistants without involving developers. For more information about {{site.data.keyword.conversationshort}}, and instructions for switching between experiences, see [Welcome to {{site.data.keyword.conversationshort}}](/docs/watson-assistant?topic=watson-assistant-welcome-new-assistant).

    If you would like to send us feedback on {{site.data.keyword.conversationshort}}, please use [this form](https://form.asana.com/?k=vvRdQAmGMFAeEGRryhTA2w&d=8612789739828){: external}.

## 3 February 2022
{: #watson-assistant-feb032022}
{: release-note}

Customize the Preview page background
:   You can now change the background of the **Preview** page to one of your organization's web pages so you can preview and test your assistant from a customer's perspective. For more information, see [Previewing and sharing your assistant](/docs/watson-assistant?topic=watson-assistant-preview-share).

Add a type to session variables
:   When you create a session variable, you can now assign a type to the variable. For more information, see [Creating a session variable](/docs/watson-assistant?topic=watson-assistant-manage-info#create-session-variable). After a type is assigned to a variable, you can set more explicit conditions on that variable. Previously, you were able to check only whether session variables were `defined` or `not defined`. With variable types, you can create conditions based on the type of the variable (for example, `account balance < 100` or `departure date is after today`). For more information, see [Operators](/docs/watson-assistant?topic=watson-assistant-step-conditions#step-conditions-operators).

Create saved customer responses
:   You can now create saved customer responses. There might be some questions that your assistant needs to ask in different steps and actions. For example, a banking assistant might have different actions that ask for a customer's account number. Instead of building the same response over and over, you can create a saved customer response and reuse it across steps in multiple actions. For more information, see [Saving and reusing customer responses](/docs/watson-assistant?topic=watson-assistant-collect-info#saved-customer-responses).

## 13 January 2022
{: #watson-assistant-jan132022}
{: release-note}

New setting for options customer response type
:    In actions, a new **List options** setting allows you to enable or disable the options customer response from appearing in a list. This can be useful to prevent a phone integration from reading a long list of options to the customer. As part of this change, all customer response types now have a **Settings** icon. **Allow skipping** has moved from **Edit Response** and is now found in the new settings. For more information, see [Collecting information from your customers](/docs/watson-assistant?topic=watson-assistant-collect-info).

## 24 December 2021
{: #watson-assistant-dec242021}
{: release-note}

Apache Log4j security vulnerability updates
:   {{site.data.keyword.conversationfull}} upgraded to using Log4j version 2.17.0, which addresses all of the Critical severity and High severity Log4j CVEs, specifically CVE-2021-45105, CVE-2021-45046, and CVE-2021-44228.

## 3 December 2021
{: #watson-assistant-dec032021}
{: release-note}

Configure webhook timeout
:   From the **Pre-message webhook** and **Post-message webhook** configuration pages, you can configure the webhook timeout length from a minimum of 1 second to a maximum of 30 seconds. For more information, see [Extending your assistant with webhooks](/docs/watson-assistant?topic=watson-assistant-webhook-overview).

User-based switching between {{site.data.keyword.conversationshort}} experiences
:   Previously, switching between {{site.data.keyword.conversationshort}} and the classic experience was instance-based. For example, if a user switched from the classic experience to {{site.data.keyword.conversationshort}}, all users of that instance were switched to {{site.data.keyword.conversationshort}}. Now, switching between the experiences is user-based. So, any user of an instance can switch between the new and classic experiences, and other users of that instance are not affected.

## 27 November 2021
{: #watson-assistant-nov272021}
{: release-note}

New API version
:   The current API version is now `2021-11-27`. This version introduces the following changes:

    - The `output.text` object is no longer returned in `message` responses. All responses, including text responses, are returned only in the `output.generic` array.

## 12 November 2021
{: #watson-assistant-nov122021}
{: release-note}

Completion analytic information
:   On the **Analyze** page, the **How often** chart can now also show the percentage of complete actions. Use the icon in the upper right of the chart to toggle between a line chart that shows the percentage of complete actions and a bar chart that shows the number of complete and incomplete actions. For more information, see [Improving completion](/docs/watson-assistant?topic=watson-assistant-analytics-action-completion#analytics-improving-completion).

Preview page update
:   The **Test integrations** panel no longer exists on the **Preview** page. You can manage your draft web chat channel from the **Preview** page. However, all other draft environment integrations are managed from the **Draft environment** page. For more information, see [Previewing and sharing your assistant](/docs/watson-assistant?topic=watson-assistant-preview-share).

## 4 November 2021
{: #watson-assistant-nov042021}
{: release-note}

Draft and Live Environment pages
:   Two pages, **Draft environment** and **Live environment**, help you to see how your channels and resolution methods are connected, both for testing/preview and for live deployment. The Draft environment page is new as of this release. The Live environment page was previously named Connect. For more information, see [Overview: Publishing and deploying your assistant](/docs/watson-assistant?topic=watson-assistant-publish-overview).

## 1 November 2021
{: #watson-assistant-nov012021}
{: release-note}

New API version
:   The current API version is now `2021-11-01`. This version includes the following changes:

   - Currency and percentage values are stored as `system_type` objects in actions. Previously, they were stored as atomic numbers.
   - The `$skip_user_input` flag is now in `contex.global.system.skip_user_input`. Previously, it was in `context.skills.["skill-reference"].user_defined.skip_user_input`.
   - When an expression is evaluated, the result is no longer subject to a SpEL evaluation. As a result, actions no longer support inline SpEL expressions such as `<? code ?>` or variable references such as `<? ${variable_name} ?>`. These are all superseded by the rich text editor's validated JSON serialization. Previously, you could write dynamic SpEL expressions such as `<? 1+1 ?>` to a scalar value and expect the result to be `2`. Now the corresponding expression construct must be used, for example, `"expression": "1+1"`.

Add variables to links
:   When including a link in an assistant response, you can now access and use variables. In the URL field for a link, type a dollar sign (`$`) character to see a list of variables to choose from.

## 25 October 2021
{: #watson-assistant-oct252021}
{: release-note}

Facebook and Slack integrations now available
:   {{site.data.keyword.conversationfull}} now includes integrations for [Facebook Messenger](/docs/watson-assistant?topic=watson-assistant-deploy-facebook) and [Slack](/docs/watson-assistant?topic=watson-assistant-deploy-slack).

Analytics for draft and live environments
:   The **Analyze** page now lets you see analytics data for either the draft or live environments. For more information, see [Use analytics to review your entire assistant at a glance](/docs/watson-assistant?topic=watson-assistant-analytics-overview).

## 7 October 2021
{: #watson-assistant-oct072021}
{: release-note}

Introducing {{site.data.keyword.conversationshort}}
:   This new experience, focused on using **actions** to build customer conversations, is designed to make it simple enough for *anyone* to build a virtual assistant. Building, testing, publishing, and analyzing your assistant can all now be done in one simple and intuitive interface.

    - New **navigation** provides a workflow for building, previewing, publishing, and analyzing your assistant.
    - Each assistant has a **home page** with a task list to help you get started.
    - Build conversations with **actions**, which represent the tasks you want your assistant to help your customers with. Each action contains a series of steps that represent individual exchanges with a customer.
    - A new way to **publish** lets you review and debug your work in a draft environment before going live to your customers.
    - Use a new suite of **analytics** to improve your assistant. Review which actions are being completed to see what your customers want help with, determine if your assistant understands and addresses customer needs, and decide how can you make your assistant better.
    - New **[documentation](/docs/watson-assistant)** focuses on the workflow of building, deploying, and improving your assistant.

## 21 September 2021
{: #watson-assistant-sep212021}
{: release-note}

Analytics Overview change
:   To improve reliability, the Values column has been removed from **Top entities** on the **Analytics Overview** page. Top Entities continues to provide counts of entity types. For more information, see [Top intents and top entities](/docs/watson-assistant?topic=watson-assistant-logs-overview#logs-overview-tops).

## 16 September 2021
{: #watson-assistant-sep162021}
{: release-note}

Enhanced intent detection for French, Italian, and Spanish dialog skills
:   The new intent detection model improves your assistant's ability to understand what customers want. This model is now available in dialog skills using French, Italian, and Spanish.

Change to the irrelevance detection option
:   As of this release, new English dialog skills no longer include the option to choose between the **Enhanced** or **Existing** irrelevance detection. By default, intent detection and irrelevance detection are paired like this:

    - If you use the dialog skill options to choose enhanced intent detection, it is automatically paired with enhanced irrelevance detection.
    - If you use the dialog skill options to choose existing intent detection, it is automatically paired with existing irrelevance detection.

    For more information, see [Defining what's irrelevant](/docs/watson-assistant?topic=watson-assistant-irrelevance-detection).

    If necessary, you can use the [Update workspace API](https://{DomainName}/apidocs/assistant/assistant-v1?curl=#updateworkspace){: external} to set your English-language assistant to one of the four combinations of intent and irrelevance detection:

    - Enhanced intent recognition and enhanced irrelevance detection
    - Enhanced intent recognition and existing irrelevance detection
    - Existing intent recognition and enhanced irrelevance detection
    - Existing intent recognition and existing irrelevance detection

    For French, Italian, and Spanish, you can use the API to set your assistant to these combinations:
    - Enhanced intent recognition and enhanced irrelevance detection
    - Existing intent recognition and existing irrelevance detection

## 15 September 2021
{: #watson-assistant-sep152021}
{: release-note}

Dialog skill "Try it out" improvements
:   The **Try it out** pane now includes these changes:

    - It now includes runtime warnings in addition to runtime errors.

    - For dialog skills, the **Try it out** pane now uses the [React](https://reactjs.org/){: external} UI framework similar to the rest of the {{site.data.keyword.assistant_classic_short}} user interface. You shouldn't see any change in behavior or functionality. As a part of the update, dialog skill error handling has been improved within the "Try it out" pane. This update was enabled on these dates:

        - September 9, 2021 in the Tokyo and Seoul data centers
        - September 13, 2021 in the London, Sydney, and Washington, D.C. data centers
        - September 15, 2021 in the Dallas and Frankfurt data centers

## 13 September 2021
{: #watson-assistant-sep132021}
{: release-note}

Dialog skill "Try it out" improvements
:   For dialog skills, the **Try it out** pane now uses the [React](https://reactjs.org/){: external} UI framework similar to the rest of the {{site.data.keyword.assistant_classic_short}} user interface. You shouldn't see any change in behavior or functionality. As a part of the update, dialog skill error handling has been improved within the "Try it out" pane. This update was enabled on September 9, 2021 in the Tokyo and Seoul data centers. On September 13, 2021, the update was enabled in the London, Sydney, and Washington, D.C. data centers.

Disambiguation feature updates
:   The dialog skill disambiguation feature now includes improved features:

    - **Increased control**: The frequency and depth of disambiguation can now be controlled by using the **sensitivity** parameter in the [workspace API](https://{DomainName}/apidocs/assistant/assistant-v1#updateworkspace){: external}. There are 5 levels of sensitivity:
        - `high`
        - `medium_high`
        - `medium`
        - `medium_low`
        - `low`

        The default (`auto`) is `medium_high` if this option is not set.

    - **More predictable**: The new disambiguation feature is more stable and predictable. The choices shown may sometimes vary slightly to enable learning and analytics, but the order and depth of disambiguation is largely stable.

    These new features may affect various metrics, such as disambiguation rate and click rates, as well as influence conversation-level key performance indicators such as containment.

    If the new disambiguation algorithm works differently than expected for your assistant, you can adjust it using the sensitivity parameter in the update workspace API. For more information, see [Update workspace](https://{DomainName}/apidocs/assistant/assistant-v1#updateworkspace){: external}.

## 9 September 2021
{: #watson-assistant-sep092021}
{: release-note}

Actions skill improvements
:   Actions skills now include these new features:

    - **Change conversation topic**: In general, an action is designed to lead a customer through a particular process without any interruptions. In real life, however, conversations almost never follow such a simple flow. In the middle of a conversation, customers might get distracted, ask questions about related issues, misunderstand something, or just change their minds about what they want to do. The **Change conversation topic** feature enables your assistant to handle these digressions, dynamically responding to the user by changing the conversation topic as needed. For more information, see [Allowing your customers to change the topic of the conversation](/docs/watson-assistant?topic=watson-assistant-change-topic).

    - **Fallback action**: The built-in action, *Fallback*, provides a way to automatically connect customers to a human agent if they need more help. This action helps you to handle errors in the conversation, and is triggered by these conditions:
        - Step validation failed: The customer repeatedly gave answers that were not valid for the expected customer response type.
        - Agent requested: The customer directly asked to be connected to a human agent.
        - No action matches: The customer repeatedly made requests or asked questions that the assistant did not understand.

        For more information, see [Editing the fallback action](/docs/watson-assistant?topic=watson-assistant-handle-errors#fallback-action).


Dialog skill "Try it out" improvements
:   For dialog skills, the **Try it out** pane now uses the [React](https://reactjs.org/){: external} UI framework similar to the rest of the {{site.data.keyword.assistant_classic_short}} user interface. You shouldn't see any change in behavior or functionality. As a part of the update, dialog skill error handling has been improved within the "Try it out" pane. This update will be implemented incrementally, starting with service instances in the Tokyo and Seoul data centers.

## 2 September 2021
{: #watson-assistant-sep022021}
{: release-note}

Deploy your assistant on the phone in minutes
:   We have partnered with [IntelePeer](https://intelepeer.ai/){: external} to enable you to generate a phone number for free within the phone integration. Simply choose to generate a free number when following the prompts to create a phone integration, finish the setup, and a number is assigned to your assistant. These numbers are robust and ready for production.

Connect to your existing service desks
:   We have added step-by-step documentation for connecting to [Genesys](/docs/watson-assistant?topic=watson-assistant-deploy-phone-genesys) and [Twilio Flex](/docs/watson-assistant?topic=watson-assistant-deploy-phone-flex) over the phone. Easily hand off to your live agents when your customers require telephony support from your service team. {{site.data.keyword.assistant_classic_short}} deploys on the phone via SIP, so most phone based service desks can easily be integrated via SIP trunking standards.

## 23 August 2021
{: #watson-assistant-aug232021}
{: release-note}

Intent detection updates
:   Intent detection for the English language has been updated with the addition of new word-piece algorithms. These algorithms improve tolerance for out-of-vocabulary words and misspelling. This change affects only English-language assistants, and only if the enhanced intent recognition model is enabled.

Automatic retraining of old skills and workspaces
:   As of August 23, 2021, {{site.data.keyword.assistant_classic_short}} enabled automatic retraining of existing skills in order to take advantage of updated algorithms. The {{site.data.keyword.assistant_classic_short}} service will continually monitor all ML models, and will automatically retrain those models that have not been retrained within the previous 6 months. For more information, see [Automatic retraining](/docs/watson-assistant?topic=watson-assistant-algorithm-version#algorithm-version-auto-retrain).

## 19 August 2021
{: #watson-assistant-aug192021}
{: release-note}

Actions preview now includes debug mode and variable values
:   When previewing your actions, you can use **debug mode** and **variable values** to ensure your assistant is working the way you expect.

    **Debug mode** allows you to go to the corresponding step by clicking on a step locator next to each message. It shows you the confidence score of top three possible action when the input triggers an action. You can also follow the step in the action editor along with the conversation flow.

    **Variable values** shows you a list of the variables and their values of current action and the session variables. You can check and edit variables during the conversation flow.

## 17 August 2021
{: #watson-assistant-aug172021}
{: release-note}

New service desk support reference implementation
:   You can use the reference implementation details to integrate the web chat with the Oracle B2C Service service desk.

## 29 July 2021
{: #watson-assistant-jul292021}
{: release-note}

Salesforce and Zendesk deployment changes
:   The Salesforce and Zendesk integrations have been updated to use the [new chat history widget](/docs/watson-assistant?topic=watson-assistant-release-notes-chat#4.5.0). The updated deployment process applies to all new deployments, including any redeployments of existing Salesforce and Zendesk connections. However, existing deployments are not affected and do not need to be modified or redeployed at this time.

Fallback value for session variables
:   In action skills, you can now set a fallback value for session variables. This feature lets you to define a value for a session variable if a user-defined value isn't found. To learn more, see [Creating a session variable](/docs/watson-assistant?topic=watson-assistant-manage-info#create-session-variable).

## 16 July 2021
{: #watson-assistant-jul162021}
{: release-note}

Logging API changes
:   The internal storage and processing of logs has changed. Some undocumented fields or filters might no longer be available. (Undocumented features are not officially supported and might change without notice.)

New API version
:   The current API version (v1 and v2) is now `2021-06-14`. The following changes were made with this version:

    - The `metadata` property of entities detected at run time is deprecated. For detailed information about detected system entities, see the `interpretation` property.
    - The data types of certain entity mentions are no longer automatically converted:
        - Numbers in scientific notation (such as `1E10`), which were previously converted to numbers
        - Boolean values (such as `false`), which were previously converted to booleans

    These values are now returned as strings.

## 17 June 2021
{: #watson-assistant-jun172021}
{: release-note}

Actions skill now generally available
:   As of this release, the beta program has ended, and actions skills are available for general use.

    An actions skill contains actions that represent the tasks you want your assistant to help your customers with. Each action contains a series of steps that represent individual exchanges with a customer. Building the conversation that your assistant has with your customers is fundamentally about deciding which steps, or which user interactions, are required to complete an action. After you identify the list of steps, you can then focus on writing engaging content to turn each interaction into a positive experience for your customer. For more information, see [Overview: Editing actions](/docs/watson-assistant?topic=watson-assistant-build-actions-overview).

Date and time response types
:   New to action skills, these response types allow you to collect date and time information from customers as they answer questions or make requests. For more information, see [Collecting information from your customers](/docs/watson-assistant?topic=watson-assistant-collect-info).

New built-in variables
:   Two kinds of built-in variables are now available for action skills.

    - **Set by assistant** variables include the common and essential variables `Now`, `Current time`, and `Current date`.
    - **Set by integration** variables are `Timezone` and `Locale` and are available to use when connected to a webhook or integration.

    For more information, see [Using variables to manage conversation information](/docs/watson-assistant?topic=watson-assistant-manage-info).

Universal language model now generally available
:   You now can build an assistant in any language you want to support. If a dedicated language model is not available for your target language, create a skill that uses the universal language model. The universal model applies a set of shared linguistic characteristics and rules from multiple languages as a starting point. It then learns from training data written in the target language that you add to it. For more information, see [Understanding the universal language model](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-universal).

## 3 June 2021
{: #watson-assistant-jun032021}
{: release-note}

Log webhook support for actions and search skills
:   The log webhook now supports messages exchanged with actions skills and search skills, in addition to dialog skills. For more information, see [Logging activity with a webhook](/docs/watson-assistant?topic=watson-assistant-webhook-log).

## 27 May 2021
{: #watson-assistant-may272021}
{: release-note}

Change to conversation skill choices
:   When adding skills to new or existing assistant, the conversation skill choices have been combined, so that you pick from either an actions skill or a dialog skill.

    With this change:
    - New assistants can use up to two skills, either actions and search or dialog and search. Previously, new assistants could use up to three skills: actions, dialog, and search.
    - Existing assistants that already use an actions skill and a dialog skill together can continue to use both.
    - The ability to use actions and dialog skills together in a new assistant is planned for 2H 2021.

## 20 May 2021
{: #watson-assistant-may202021}
{: release-note}

Actions skill improvement
:  Actions now include a new choice, **Go to a subaction**, for what to do next in a step. This feature lets you can call one action from another action, to switch the conversation flow to another action to perform a certain task. If you have a portion of an action that can be applied across multiple use cases you can build it once and call to it from each action. This new option is available in the **And then** section of each step. For more information, see [Go to a subaction](/docs/watson-assistant?topic=watson-assistant-step-what-next#go-to-another-action).

## 21 April 2021
{: #watson-assistant-apr212021}
{: release-note}

Preview button for testing your assistant
:   For testing your assistant, the new Preview button replaces the previous Preview tile in Integrations.

New checklist with steps to go live
:   Each assistant includes a checklist that you can use to ensure you're ready to go live.

Actions skill improvement
:   Actions now include currency and percentage response types.

Learn what's new
:   The *What's new* choice on the help menu opens a list of highlighting recent features.

## 14 April 2021
{: #watson-assistant-apr142021}
{: release-note}

Actions skill improvement
:   Actions now include a free text response type, allowing you to capture special instructions or requests that a customer wants to pass along.

## 8 April 2021
{: #watson-assistant-apr082021}
{: release-note}

Deploy your assistant to WhatsApp - now generally available
:   Make your assistant available through WhatsApp messaging so it can exchange messages with your customers where they are. This integration, which is now generally available, creates a connection between your assistant and WhatsApp by using Twilio as a provider. For more information, see [Integrating with WhatsApp](/docs/watson-assistant?topic=watson-assistant-deploy-whatsapp).

Web chat home screen now generally available
:   Ease your customers into the conversation by adding a home screen to your web chat window. The home screen greets your customers and shows conversation starter messages that customers can click to easily start chatting with the assistant. For more information about the home screen feature, see [Configuring the home screen](/docs/watson-assistant?topic=watson-assistant-web-chat-configure-home-screen). The home screen feature is now enabled by default for all new web chat deployments. Also, you can now access context variables from the home screen. Note that initial context must be set using a `conversation_start` node. For more information, see [Starting the conversation](/docs/watson-assistant?topic=watson-assistant-dialog-start#dialog-start-welcome).

Connect to human agent response type allows more text
:   In a dialog skill, the response type *Connect to human agent* now allows 320 characters in the *Response when agents are online* and *Response when no agents are online* fields. The previous limit was 100 characters.

Legacy system entities deprecated
:   In January 2020, a new version of the system entities was introduced. As of April 2021, only the new version of the system entities is supported for all languages. The option to switch to using the legacy version is no longer available.    

## 6 April 2021
{: #watson-assistant-apr062021}
{: release-note}

Service API endpoint change
:   As explained in [December 2019](#watson-assistant-dec122019), as part of work done to fully support IAM authentication, the endpoint you use to access your {{site.data.keyword.assistant_classic_short}} service programmatically is changing. The old endpoint URLs are deprecated and **will be retired on 26 May 2021**. Update your API calls to use the new URLs.

    The pattern for the endpoint URL changes from `gateway-{location}.watsonplatform.net/assistant/api/` to `api.{location}.assistant.watson.cloud.ibm.com/`. The domain, location, and offering identifier are different in the new endpoint. For more information, see [Updating endpoint URLs from watsonplatform.net](/docs/watson?topic=watson-endpoint-change){: external}.

    - If your service instance API credentials show the old endpoint, create a new credential and start using it today. After you update your custom applications to use the new credential, you can delete the old one.

    - For a web chat integration, you might need to take action depending on when and how you created your integration.

        - If you tied your deployment to a specific web chat version by using the `clientVersion` parameter and specified a version earlier than version 3.3.0, update the parameter value to use version 3.3.0 or later. Web chat integrations that use the latest or 3.3.0 and later versions will not be impacted by the endpoint deprecation.

        - If you created your web chat integration before May 2020, check the code snippet that you embedded in your web page to see if it refers to `watsonplatform.net`. If so, you must edit the code snippet to use the new URL syntax. For example, change the following URL:

            ```html
             <script src="https://assistant-web.watsonplatform.net/loadWatsonAssistantChat.js"></script>
            ```

            The correct syntax to use for the source service URL looks like this:

            ```code
            src="https://web-chat.global.assistant.watson.appdomain.cloud/loadWatsonAssistantChat.js"
            ```

    - If your web chat integration connects to a Salesforce service desk, then you must edit the API call that is included in the code snippet that you added to the Visualforce Page that you created in Salesforce. From Salesforce, search for *Visualforce Pages*, and find your page. In the `<iframe>` snippet that you pasted into the page, make the following change:

      Replace: `src=“https://assistant-integrations-{location}.watsonplatform.net/public/salesforceweb”` with a url with this syntax:

        ```code
        src="https://integrations.{location}.assistant.watson.appdomain.cloud/public/salesforceweb/{integration-id}/agent_application?version=2020-09-24"
        ```
        {: codeblock}

      From the Web chat integration Salesforce live agent setup page, find the *Visualforce page markup* field. Look for the `src` parameter in the `<iframe>` element. It contains the full URL to use, including the appropriate `{location}` and `{integration-id}` values for your instance.

    - For a Slack integration that is over 7 months old, make sure the Request URL is using the proper endpoint.

        - Go to the [Slack API](https://api.slack.com/){: external} web page. Click *Your Apps* to find your assistant app. Click *Event Subscriptions* from the navigation pane.
        - Edit the Request URL.

      For example, if the URL has the syntax: `https://assistant-slack-{location}.watsonplatform.net/public/message`, change it to have this syntax:

      ```code
      https://integrations.{location}.assistant.watson.appdomain.cloud/public/slack/{integration-id}/message?version=2020-09-24
      ```
      {: codeblock}

      Check the *Generated request URL* field in the Slack integration setup page for the full URL to use, which includes the appropriate `{location}` and `{integration-id}` values for your instance.

    - For a Facebook Messenger integration that is over 7 months old, make sure the Callback URL is using the proper endpoint.

        - Go to the [Facebook for Developers](https://developers.facebook.com/apps/){: external} web page.
        - Open your app, and then select *Messenger>Settings* from the navigation pane.
        - Scroll down to the *Webhooks* section and edit the *Callback URL* field.

          For example, if the URL has the syntax: `https://assistant-facebook-{location}.watsonplatform.net/public/message/`, change it to have this syntax:

          ```code
          https://integrations.{location}.assistant.watson.appdomain.cloud/public/facebook/{integration-id}/message?version=2020-09-24
          ```
          {: codeblock}

          Check the *Generated callback URL* field in the Facebook Messenger integration setup page for the full URL to use, which includes the appropriate `{location}` and `{integration-id}` values for your instance.

    - For a Phone integration, if you connect to existing speech service instances, make sure those speech services use credentials that were generated with the latest endpoint syntax (a URL that starts with `https://api.{location}.speech-to-text.watson.cloud.ibm.com/`).

    - For a search skill, if you connect to an existing {{site.data.keyword.discoveryshort}} service instance, make sure the {{site.data.keyword.discoveryshort}} service uses credentials that were generated with the supported syntax (a URL that starts with `https://api.{location}.discovery.watson.cloud.ibm.com/`).

    - No action is required for the following integration types:

        - Intercom
        - SMS with Twilio
        - WhatsApp with Twilio
        - Zendesk service desk connection from web chat

## 23 March 2021
{: #watson-assistant-mar232021}
{: release-note}

Actions skill improvement
:   Actions have a new toolbar making it easier to send feedback, access settings, save, and close.

## 17 March 2021
{: #watson-assistant-mar172021}
{: release-note}

Channel transfer response type
:   Dialog skills now include a channel transfer response type. If your assistant uses multiple integrations to support different channels for interaction with users, there might be some situations when a customer begins a conversation in one channel but then needs to transfer to a different channel. The most common such situation is transferring a conversation to the web chat integration, to take advantage of web chat features such as service desk integration. For more information, see [Adding a Channel transfer response type](/docs/watson-assistant?topic=watson-assistant-dialog-overview#dialog-overview-add-channel-transfer.

Intercom and WhatsApp integrations now available in Lite plan
:   The integrations for Intercom and WhatsApp are now available in the Lite plan for {{site.data.keyword.assistant_classic_short}}. For more information, see [Integrating with Intercom](/docs/watson-assistant?topic=watson-assistant-deploy-intercom) and [Integrating with WhatsApp](/docs/watson-assistant?topic=watson-assistant-deploy-whatsapp).

## 16 March 2021
{: #watson-assistant-mar162021}
{: release-note}

Session history now generally available
:   Session history allows your web chats to maintain conversation history and context when users refresh a page or change to a different page on the same website. It is enabled by default. For more information about this feature, see [Session history](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-session-history){: external}.

    Session history persists within only one browser tab, not across multiple tabs. The dialog provides an option for links to open in a new tab or the same tab. See [this example](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-session-history#Tutorial1){: external} for more information on how to format links to open in the same tab.

    Session history saves changes that are made to messages with the [pre:receive event](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#prereceive){: external} so that messages still look the same on rerender. This data is only saved for the length of the session. If you prefer to discard the data, set `event.updateHistory = false;` so the message is rerendered without the changes that were made in the pre:receive event.

    [instance.updateHistoryUserDefined()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateHistoryUserDefined){: external} provides a way to save state for any message response. With the state saved, a response can be rerendered with the same state. This saved state is available in the `history.user_defined` section of the message response on reload. The data is saved during the user session. When the session expires, the data is discarded.

    Two new history events, [history:begin](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#historybegin){: external} and [history:end](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#historyend){: external} announce the beginning and end of the history of a reloaded session. These events can be used to view the messages that are being reloaded. The history:begin event allows you to edit the messages before they are displayed.

    See this example for more information on saving the state of [customResponse](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#customresponse){: external} types in session history.

Channel switching
:   You can now create a dialog response type to functionally generate a connect-to-agent response within channels other than web chat. If a user is in a channel such as Slack or Facebook, they can trigger a channel transfer response type. The user receives a link that forwards them to your organization's website where a connection to an agent response can be started within web chat. For more information, see [Adding a Channel transfer response type](//docs/watson-assistant?topic=watson-assistant-dialog-overview#dialog-overview-add-channel-transfer).

## 11 March 2021
{: #watson-assistant-mar112021}
{: release-note}

Actions skill improvement
:   Updated the page where you configure a step with an *Options* reply constraint. Now it's clearer that you have a choice to make about whether to always ask for the option value or to skip asking. For more information, see [Skipping steps, always asking steps, or never asking steps](/docs/watson-assistant?topic=watson-assistant-collect-info#collect-info-skip-step).

## 4 March 2021
{: #watson-assistant-mar042021}
{: release-note}

Support for every language!
:   You now can build an assistant in any language you want to support. If a dedicated language model is not available for your target language, create a skill that uses the universal language model. The universal model applies a set of shared linguistic characteristics and rules from multiple languages as a starting point. It then learns from training data written in the target language that you add to it.

    The universal model is available as a beta feature. For more information, see [Understanding the universal language model](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-universal).

Actions skill improvement
:   Now you can indicate whether or not to ask for a number when you apply a number reply constraint to a step. Test how changes to this setting might help speed up a customer's interaction. Under the right circumstances, it can be useful to let a number mention be recognized and stored without having to explicitly ask the customer for it. For more information, see [Skipping steps, always asking steps, or never asking steps](/docs/watson-assistant?topic=watson-assistant-collect-info#collect-info-skip-step).

## 1 March 2021
{: #watson-assistant-mar012021}
{: release-note}

Introducing the *Enterprise* plan!
:   The Enterprise plan includes all of the market differentiating features of the Plus plan, but with higher capacity limits, additional security features, custom onboarding support to get you going, and a lower overall cost at higher volumes.

    To have a dedicated environment provisioned for your business, request the *Enterprise with Data Isolation* plan. To submit a request online, go to [http://ibm.biz/contact-wa-enterprise](http://ibm.biz/contact-wa-enterprise){: external}.

    The Enterprise plan is replacing the Premium plan. The Premium plan is being retired today. Existing Premium plan users are not impacted. They can continue to work in their Premium instances and create instances up to the 30-instance limit. New users do not see the Premium plan as an option when they create a service instance.

    For more information, see the [Pricing](https://www.ibm.com/products/watsonx-assistant/pricing){: external} page.

Other plan changes
:   Our pricing has been revised to reflect the features we've added that help you build an assistant that functions as a powerful omnichannel SaaS application.

    Starting on 1 March 2021, the Plus plan starts at $140 per month and includes your first 1,000 monthly users. You pay $14 for each additional 100 active users per month. Use of the voice capabilities that are provided by the *Phone* integration are available for an additional $9 per 100 users per month.

    The Plus Trial plan was renamed to Trial.

SOC 2 compliance
:   {{site.data.keyword.assistant_classic_short}} is SOC 2 Type 2 compliant, so you know your data is secure.

    The System and Organization Controls framework, developed by the American Institute of Certified Public Accountants (AICPA), is a standard for controls that protect information stored in the cloud. SOC 2 reports provide details about the nature of internal controls that are implemented to protect customer-owned data. For more information, see [IBM Cloud compliance programs](https://www.ibm.com/cloud/compliance/global){: external}.

## 25 February 2021
{: #watson-assistant-feb252021}
{: release-note}

Search skill can emphasize the answer
:   You can configure the search skill to highlight text in the search result passage that {{site.data.keyword.discoveryshort}} determines to be the exact answer to the customer's question.

Integration changes
:   The following changes were made to the integrations:

    - The name of *Preview link* integration changed to *Preview*.
    - The *Web chat* and *Preview* integrations are no longer added automatically to every new assistant.

        The integrations continue to be added to the *My first assistant* that is generated for you automatically when you first create a new service instance.

Message and log webhooks are generally available
:   The premessage, postmessage, and log webhooks are now generally available. For more information about them, see [Webhook overview](/docs/watson-assistant?topic=watson-assistant-webhook-overview).

## 11 February 2021
{: #watson-assistant-feb112021}
{: release-note}

The `user_id` value is easier to access
:   The `user_id` property is used for billing purposes. Previously, it was available from the context object as follows:

    - v2: `context.global.system.user_id`
    - v1: `context.metadata.user_id`

    The property is now specified at the root of the `/message` request in addition to the context object. The built-in integrations typically set this property for you. If you're using a custom application and don't specify a `user_id`, the `user_id` is set to the `session_id` (v2) or `conversation_id`(v1) value.

Digression bug fix
:   Fixed a bug where digression setting changes that were made to a node with slots were not being saved.

## 5 February 2021
{: #watson-assistant-feb052021}
{: release-note}

Documentation update
:   The phone and *SMS with Twilio* deployment documentation was updated to include instructions for migrating from {{site.data.keyword.iva_short}}. For more information, see [Migrating from {{site.data.keyword.iva_short}}](/docs/watson-assistant?topic=watson-assistant-deploy-phone-config#deploy-phone-config-migrate-from-va).

## 27 January 2021
{: #watson-assistant-jan272021}
{: release-note}

German language improvements
:   A word decomposition function was added to the intent and entity recognition models for German-language dialog skills.

    A characteristic of the German language is that some words are formed by concatenating separate words to form a single compound word. For example, "festnetznummer" (landline number) concatenates the words "festnetz" (landline) and "nummer" (number). When your customers chat with your assistant, they might write a compound word as a single word, as hyphenated words, or as separate words. Previously, the variants resulted in different intent confidence scores and different entity mention counts based on your training data. With the addition of the word decomposition function, the models now treat all compound word variants as equivalent. This update means you no longer need to add examples of every variant of the compound words to your training data.

## 19 January 2021
{: #watson-assistant-jan192021}
{: release-note}

The *Phone* and *SMS with Twilio* integrations are now generally available!
:   For more information, see:

    - [Integrating with phone](/docs/watson-assistant?topic=watson-assistant-deploy-phone)
    - [Integrating with *SMS with Twilio*](/docs/watson-assistant?topic=watson-assistant-deploy-sms)

*Preview link* change
:   When you create a preview link, you can now test your skill from a chat window that is embedded in the page. You can also copy the URL that is provided, and open it in a web browser to see an IBM-branded web page with the web chat embedded in it. You can share the URL to the public IBM web page with others to get help with testing or for demoing purposes.

Import and export UI changes
:   The label on buttons for importing skills changed from *Import* to *Upload*, and the label on buttons for exporting skills changed from *Export* to *Download*.

Coverage metric change
:   The coverage metric now looks for nodes that were processed with a node condition that includes the `anything_else` special condition instead of nodes that are named `Anything else`. For more information, see [Starting and ending the dialog](/docs/watson-assistant?topic=watson-assistant-dialog-start).

## 15 January 2021
{: #watson-assistant-jan152021}
{: release-note}

Use new webhooks to process messages!
:   A set of new webhooks is available as a beta feature. You can use the webhooks to perform preprocessing tasks on incoming messages and postprocessing tasks on the corresponding responses. You can use the new log webhook to log each message with an external service. For more information, see [Webhook overview](/docs/watson-assistant?topic=watson-assistant-webhook-overview).

New service desk support reference implementation
:   You can use the reference implementation details to integrate the web chat with the NICE inContact service desk. For more information, see [Integrating with phone and NICE CXone contact center](/docs/watson-assistant?topic=watson-assistant-deploy-phone-nicecxone).

Phone and *SMS with Twilio* integration updates
:   The phone integration now enables you to specify more than one phone number, and the numbers can be imported from a comma-separated values (CSV) file. The *SMS with Twilio* integration no longer requires you to add your SMS phone number to the setup page.

## 6 January 2021
{: #watson-assistant-jan062021}
{: release-note}

Import and export UI changes
:   The label on buttons for importing intents and entities changed from *Import* to *Upload*. The label on buttons for exporting intents and entities changed from *Export* to *Download*.

## 4 January 2021
{: #watson-assistant-jan042021}
{: release-note}

Dialog methods updates
:   Documentation and examples were added for the following supported dialog methods:

    - `JSONArray.addAll(JSONArray)`
    - `JSONArray.containsIgnoreCase(value)`
    - `String.equals(String)`
    - `String.equalsIgnoreCase(String)`

    For more information, see [Expression language methods for dialog](/docs/watson-assistant?topic=watson-assistant-dialog-methods).

## 17 December 2020
{: #watson-assistant-dec172020}
{: release-note}

Accessibility improvements
:   The product was updated to provide enhanced accessibility features.

## 14 December 2020
{: #watson-assistant-dec142020}
{: release-note}

Increased Phone and SMS with Twilio integrations availability
:   These beta SMS and voice capabilities are now available from service instances that are hosted in Seoul, Tokyo, London, and Sydney.

Improved JSON editor
:   The JSON editor in the dialog skill was updated. The editor now uses JSON syntax highlighting and allows you to expand and collapse objects.

Connect to agent from actions skill
:   The actions skill now supports transferring a customer to an agent from within an action step. For more information, see [Connecting to a live agent](/docs/watson-assistant?topic=watson-assistant-human-agent).

## 4 December 2020
{: #watson-assistant-dec042020}
{: release-note}

Introducing more service desk options for web chat
:   When you deploy your assistant by using the web chat integration, there are now reference implementations that you can use for the following service desks:

    - Twilio Flex
    - Genesys Cloud

    Alternatively, you can bring your own service desk by using the service desk extension starter kit.

Autolearning has been moved and improved
:   Go to the *Analytics>Autolearning* page to enable the feature and see visualizations that illustrate how autolearning impacts your assistant's performance over time. For more information, see [Using autolearning to improve assistant responses](/docs/watson-assistant?topic=watson-assistant-autolearn).

Search from actions skill
:   The actions skill now supports triggering a search that uses your associated search skill from within an action step. For more information, see [Search for the answer](/docs/watson-assistant?topic=watson-assistant-step-what-next#search-for-answer).

System entities language support change
:   The new system entities are now used by all skills except Korean-language dialog skills. If you have a Korean skill that uses the older version of the system entities, update it. The legacy version will stop being supported for Korean skills in March 2021.

Disambiguation selection enhancement
:   When a customer chooses an option from a disambiguation list, the corresponding intent is submitted. With this latest release, a confidence score of 1.0 is assigned to the intent. Previously, the original confidence score of the option was used.

Skill import improvements
:   Importing of large skills from JSON data is now processed in the background. When you import a JSON file to create a skill, the new skill tile appears immediately. However, depending on the size of the skill, it might not be available for several minutes while the import is being processed. During this time, the skill cannot be opened for editing or added to an assistant, and the skill tile shows the text **Processing**.

## 23 November 2020
{: #watson-assistant-nov232020}
{: release-note}

Deploy your assistant to WhatsApp!
:   Make your assistant available through WhatsApp messaging so it can exchange messages with your customers where they are. This beta integration creates a connection between your assistant and WhatsApp by using Twilio as a provider. For more information, see [Integrating with WhatsApp](/docs/watson-assistant?topic=watson-assistant-deploy-whatsapp).

## 13 November 2020
{: #watson-assistant-nov132020}
{: release-note}

New coverage metric and enhanced intent detection model
:   The following features are available in service instances hosted in all data center locations except Dallas.

Introducing the coverage metric!
:   Want a quick way to see how your dialog is doing at responding to customer queries? Enable the new coverage metric to find out. The coverage metric measures the rate at which your dialog is confident that it can address a customer's request per message. For conversations that are not covered, you can review the logs to learn more about what the customer wanted. For the metric to work, you must design your dialog to include an *Anything else* node that is processed when no other dialog node intents are matched. For more information, see [Graphs and statistics](/docs/watson-assistant?topic=watson-assistant-logs-overview#logs-overview-graphs).

Try out the enhanced intent detection model
:   The new model, which is being offered as a beta feature in English-language dialog and actions skills, is faster and more accurate. It combines traditional machine learning, transfer learning, and deep learning techniques in a cohesive model that is highly responsive at run time.

## 3 November 2020
{: #watson-assistant-nov032020}
{: release-note}

Suggestions are now generally available
:   The Suggestions feature that is available for the web chat integration is generally available and is enabled by default when you create a new web chat integration. For more information, see [Configuring suggestions](/docs/watson-assistant?topic=watson-assistant-web-chat-suggestions).

## 29 October 2020
{: #watson-assistant-oct292020}
{: release-note}

System entity support changes
:   For English, Brazilian Portuguese, Czech, Dutch, French, German, Italian, and Spanish dialog skills only the new system entities API version is supported. For backward compatibility, both the `interpretation` and `metadata` attributes are included with the recognized entity object. The new system entity version is enabled automatically for dialog skills in the Arabic, Chinese, Korean, and Japanese languages. You can choose to use the legacy version of the system entities API by switching to it from the **Options>System Entities** page. This settings page is not displayed in English, Brazilian Portuguese, Czech, Dutch, French, German, Italian, and Spanish dialog skills because use of the legacy version of the API is no longer supported for those languages. For more information about the new system entities, see [System entities](/docs/watson-assistant?topic=watson-assistant-system-entities).

## 28 October 2020
{: #watson-assistant-oct282020}
{: release-note}

Introducing the *actions skill*!
:   The actions skill is the latest step in the continuing evolution of {{site.data.keyword.assistant_classic_short}} as a software as a service application. The actions skill is designed to make it simple enough for *anyone* to build a virtual assistant. We've removed the need to navigate between intents, entities, and dialog to create conversational flows. Building can all now be done in one simple and intuitive interface.

    The actions skill is available as a beta feature.

Web chat integration is created automatically
:   When you create a new assistant, a web chat integration is created for you automatically (in addition to the preview link integration, which was created previously). These integrations are added also to the assistant that is auto-generated (named *My first assistant*) when you create a new service instance. For more information, see [Web chat overview](/docs/watson-assistant?topic=watson-assistant-web-chat-overview).

Text messaging integration was renamed
:   The *Twilio messaging* integration was renamed to *SMS with Twilio*.

## 9 October 2020
{: #watson-assistant-oct092020}
{: release-note}

Search skill update
:   Support was added for a new version of the {{site.data.keyword.discoveryshort}} API which adds the following capabilities:

    - The search skill can now connect to existing Premium {{site.data.keyword.discoveryshort}} service instances.

    - When you connect to a Box, Sharepoint, or Web crawl data collection, the result content fields are automatically populated for you. The **Title** now uses the `title` field from the source document instead of the `extracted_metadata.title` field, which provides better results.

## 1 October 2020
{: #watson-assistant-oct012020}
{: release-note}

Introducing the *Phone* integration!
:   Your customers are calling; now your assistant can answer. Add a phone integration to enable your assistant to answer customer support calls. The integration connects to your existing Session Initiation Protocol (SIP) trunk, which routes incoming calls to your assistant. For more information, see [Integrating with phone](/docs/watson-assistant?topic=watson-assistant-deploy-phone).

Introducing the *Twilio messaging* integration!
:   Enable your assistant to receive and respond to questions that customers submit by using SMS text messaging. When you enable both new integrations, your assistant can send text messages to a customer in the context of an ongoing phone conversation. For more information, see [Integrating with SMS](/docs/watson-assistant?topic=watson-assistant-deploy-sms).

    The *Phone* and *Twilio messaging* integrations are available as beta features in {{site.data.keyword.assistant_classic_short}} service instances that are hosted in Dallas, Frankfurt, and Washington, DC.

The web chat integration is added to new assistants automatically
:   Much like the *Preview link* integration, the *Web chat* integration now is added to the *My first assistant* assistant that is created for new users automatically.

## 24 September 2020
{: #watson-assistant-sep242020}
{: release-note}

Introducing the containment metric!
:   Want a quick way to see how often your assistant has to ask for help? Enable the new containment metric to find out. The containment metric measures the rate at which your assistant is able to address a customer's goal without human intervention. For conversations that are not contained, you can review the logs to understand what led customers to seek help outside of the assistant. For the metric to work, you must design your dialog to flag requests for additional support when they occur. For more information, see [Graphs and statistics](/docs/watson-assistant?topic=watson-assistant-logs-overview#logs-overview-graphs).

Chat transfer improvements
:   When you add the *Connect to human agent* response type to a dialog node, you can now define messages to show to your customers during the transfer, and can specify service desk agent routing preferences. For more information, see [Adding a *Connect to human agent* response type](/docs/watson-assistant?topic=watson-assistant-dialog-overview#dialog-overview-add-connect-to-human-agent).

## 22 September 2020
{: #watson-assistant-sep222020}
{: release-note}

New API version
:   The current v2 API version is now `2020-09-24`. In this version, the structure of the `search` response type has changed. The `results` property has been removed and replaced with two new properties:

    - `primary_results` property includes the search results that should be displayed in the initial response to a user query.
    - `additional_results` property includes search results that can be displayed if the user wants to see more.

    The search skill configuration determines how many search results are included in the `primary_results` and `additional_results` properties.

Search skill improvements
:   The following improvements were made to the search skill:

    - **Control the number of search results**: You can now customize the number of search results that are shown in a response from the search skill. For more information, see [Configure the search](/docs/watson-assistant?topic=watson-assistant-search-add#search-add-configure).

    - **FAQ extraction is available for web crawl data collections**: When you create a web crawl data collection type, you can now enable the FAQ extraction beta feature. FAQ extraction allows the {{site.data.keyword.discoveryshort}} service to identify question and answer pairs that it finds as it crawls the website.

## 16 September 2020
{: #watson-assistant-sep162020}
{: release-note}

Search skill refinement change
:   The search refinement beta feature that was added in [June](#watson-assistant-jun242020) now is disabled by default. Enable the feature to refine the search results that are returned from the {{site.data.keyword.discoveryshort}} service. For more information, see [Configure the search](/docs/watson-assistant?topic=watson-assistant-search-add#search-add-configure).

## 25 August 2020
{: #watson-assistant-aug252020}
{: release-note}

Give the web chat integration a try!
:   You can now use the web chat integration with a Lite plan. Previously, the web chat was available to Plus or higher plans only. For more information, see [Web chat overview](/docs/watson-assistant?topic=watson-assistant-web-chat-overview).

## 12 August 2020
{: #watson-assistant-aug122020}
{: release-note}

v2 Logs API is available
:   If you have a Premium plan, you can use the v2 API `logs` method to list log events for an assistant. For more information, see the [API reference](https://{DomainName}/assistant/assistant-v2#listlogs){: external} documentation.

## 5 August 2020
{: #watson-assistant-aug052020}
{: release-note}

Enable your skill to improve itself
:   Try the new **autolearning** beta feature to empower your skill to improve itself automatically over time. Your skill observes customer choices to understand which choices are most often the best. As its confidence grows, your skill presents better options to get the right answers to your customers with fewer clicks. For more information, see [Using autolearning to improve assistant responses](/docs/watson-assistant?topic=watson-assistant-autolearn).

Show more of search results
:   When search results are returned from the search skill, the customer can now click a twistie to expand the search result card to see more of the returned text.

## 29 July 2020
{: #watson-assistant-jul292020}
{: release-note}

The @sys-location and @sys-person system entities were removed
:   The `@sys-location` and `@sys-person` system entities are no longer listed on the *System entities* page. If your dialog uses one of these entities, a red `Entity not created` notification is displayed to inform you that the entity is not recognized.

Skill menu actions moved
:   The menu that was displayed in the header of the skill while you were working with a skill was removed. The actions that were available from the menu, such as import and export, are still available. Go to the Skills page, and click the menu on the skill tile.

    The import skill process was updated to support overwriting an existing skill on import.

Dialog issues were addressed
:   These dialog issues were addressed:
    - Fixed an issue with adding a jump-to from a conditional response in one node to a conditional response in another node.
    - The page now responds better when you scroll horizontally to see multiple levels of child nodes.

## 15 July 2020
{: #watson-assistant-jul152020}
{: release-note}

Support ended for @sys-location and @sys-person
:   The person and location system entities, which were available as a beta feature in English dialog skills only, are no longer supported. You cannot enable them. If your dialog uses them, they are ignored by the service.

    Use contextual entities to teach your skill to recognize the context in which such names are used. For more information about contextual entities, see [Annotation-based method](/docs/watson-assistant?topic=watson-assistant-entities#entities-annotations-overview).

    For more information about how to use contextual entities to identify names of people, see the [Detecting Names And Locations With {{site.data.keyword.assistant_classic_short}}](https://medium.com/ibm-watson/detecting-names-and-locations-with-watson-assistant-e3e1fa2a8427){: external} blog post on Medium.

How legacy numeric system entities are processed has changed
:   All new dialog skills use the new system entities automatically.

    For existing skills that use legacy numeric system entities, how the entities are processed now differs based on the skill language.

    - Arabic, Chinese, Korean, and Japanese dialog skills that use legacy numeric system entities function the same as before.
    - If you choose to continue to use the legacy system entities in European-language dialog skills, a new legacy API format is used. The new legacy API format simulates the legacy system entities behavior. In particular, it returns a `metadata` object and does not stop the service from identifying multiple system entities for the same input string. In addition, it returns an `interpretation` object, which was introduced with the new version of system entities. Review the `interpretation` object to see the useful information that is returned by the new version.

    Update your skills to use the new system entities from the **Options>System Entities** page.

Web chat security is generally available
:   Enable the security feature of web chat so that you can verify that messages sent to your assistant come from only your customers and can pass sensitive information to your assistant.

    When configuring the JWT, you no longer need to specify the Authentication Context Class Reference (acr) claim.

## 1 July 2020
{: #watson-assistant-jul012020}
{: release-note}

Salesforce support is generally available
:   Integrate your web chat with Salesforce so your assistant can transfer customers who asks to speak to a person to a Salesforce agent who can answer their questions. For more information, see [Integrating with Salesforce](/docs/watson-assistant?topic=watson-assistant-deploy-salesforce).

## 24 June 2020
{: #watson-assistant-jun242020}
{: release-note}

Get better answers from search skill
:   The search skill now has a beta feature that limits the search results that are returned to include only those for which {{site.data.keyword.discoveryshort}} has calculated a 20% or higher confidence score. You can toggle the feature on or off from the *Refine results to return more selective answers* switch on the configuration page. You cannot change the confidence score threshold from 0.2. This beta feature is enabled by default. For more information, see [{{site.data.keyword.discoveryfull}} search integration setup](/docs/watson-assistant?topic=watson-assistant-search-add).

## 3 June 2020
{: #watson-assistant-jun032020}
{: release-note}

Zendesk support is generally available
:   Integrate your web chat with Zendesk so your assistant can transfer customers who asks to speak to a person to a Zendesk agent who can answer their questions. And now you can secure the connection to Zendesk. For more information, see [Integrating with Zendesk](/docs/watson-assistant?topic=watson-assistant-deploy-zendesk).

Pricing plan changes
:   We continue to revamp the overall service plan structure for {{site.data.keyword.assistant_classic_short}}. In April, we announced [a new low cost entry point](#watson-assistant-apr012020) for the Plus plan. Today, the Standard plan is being retired. Existing Standard plan users are not impacted; they can continue to work in their Standard instances. New users do not see the Standard plan as an option when they create a service instance. For more information, see the [Pricing](https://www.ibm.com/products/watsonx-assistant/pricing){: external} page.

## 27 May 2020
{: #watson-assistant-may272020}
{: release-note}

Full language support for new system entities
:   The new version of the system entities is generally available in dialog skills of all languages, including Arabic, Chinese (Simplified), Chinese (Traditional), Korean, and Japanese. For more information, see [Supported languages](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-codes).

New system entities are enabled automatically
:   All new dialog skills use the new version of the system entities automatically.

## 22 May 2020
{: #watson-assistant-may222020}
{: release-note}

Spelling correction in v2 API
:   The v2 `message` API now supports spelling correction options. For more information see the [API Reference](https://{DomainName}/apidocs/assistant/assistant-v2#message){: external}.

## 21 May 2020
{: #watson-assistant-may212020}
{: release-note}

Preview link URL change
:   The URL for the preview link was changed. If you previously shared the link with teammates, provide them with the new URL.

## 15 May 2020
{: #watson-assistant-may152020}
{: release-note}

Private endpoints support is available in Plus plan
:   You can use private endpoints to route services over the {{site.data.keyword.cloud_notm}} private network instead of the public network. For more information, see [Private network endpoints](/docs/watson-assistant?topic=watson-assistant-admin-securing#security-private-endpoints). This feature was previously available to users of Premium plans only.

## 14 May 2020
{: #watson-assistant-may142020}
{: release-note}

Get skill owner information
:   The email address of the person who owns the service instance that you are using is displayed from the User account menu. This information is especially helpful if you want to contact the instance owner to request access changes.

System entity deprecation
:   As stated in the [March deprecation notice](#watson-assistant-mar012020), the `@sys-location` and `@sys-person` system entities that were available as a beta feature are deprecated. If you are using one of these system entities in your dialog, a toggle is displayed for the entity on the *System entities* page. You can [search your dialog](/docs/watson-assistant?topic=watson-assistant-dialog-tasks#dialog-tasks-search) to find out where you are currently using the entity, and remove it. Consider using a contextual entity to identify references to locations and people instead. After removing the entity from your dialog, disable the entity from the *System entities* page.

## 13 May 2020
{: #watson-assistant-may132020}
{: release-note}

Stateless v2 message API
:   The v2 runtime API now supports a new stateless `message` method. If you have a client application that manages its own state, you can use this new method to take advantage of [many of the benefits](https://medium.com/ibm-watson/the-new-watson-assistant-v2-stateless-api-unlock-enterprise-features-today-2c02a4bbdef5){: external} of the v2 API without the overhead of creating sessions. For more information, see the [API Reference](https://{DomainName}/assistant/assistant-v2#message-stateless){: external}.

## 30 April 2020
{: #watson-assistant-apr302020}
{: release-note}

Web chat is generally available!
:   Add your assistant to your company website as a web chat widget that can help your customers with common questions and tasks. Service desk transfer support continues to be a beta feature. For more information, see [Web chat overview](/docs/watson-assistant?topic=watson-assistant-web-chat-overview).

Secure your web chat
:   Enable the beta security feature of web chat so that you can verify that messages sent to your assistant come from only your customers and can pass sensitive information to your assistant.

## 27 April 2020
{: #watson-assistant-apr272020}
{: release-note}

Add personality to your assistant in web chat
:   You can add an assistant image to the web chat header to brand the window. You can add an avatar image that represents your assistant or a brand logo, for example. For more information, see [Configuring style and appearance](/docs/watson-assistant?topic=watson-assistant-web-chat-style).

Know your plan
:   Now your service plan is displayed in the page header. And if you have a Plus Trial plan, you can see how many days are left in the trial.

## 21 April 2020
{: #watson-assistant-apr212020}
{: release-note}

Fuzzy matching support was expanded
:   Added support for stemming and misspelling in French, German, and Czech dialog skills. This enhancement means that the assistant can recognize an entity value that is defined in its singular form but mentioned in its plural form in user input. It also can recognize conjugated forms of a verb that is specified as an entity value.

    For example, if your French-language dialog skill has an entity value of `animal`, it recognizes the plural form of the word (`animaux`) when it is mentioned in user input. If your German-language dialog skill has the root verb `haben` as an entity value, it recognizes conjugated forms of the verb (`hast`) in user input as mentions of the entity.

## 2 April 2020
{: #watson-assistant-apr022020}
{: release-note}

New and improved access control
:   Now, when you give other people access to your {{site.data.keyword.assistant_classic_short}} resources, you have more control over the level of access they have to individual skills and assistants. You can give one person read-only access to a production skill and manager-level access to a development skill, for example. For more information, see [Managing access](/docs/watson-assistant?topic=watson-assistant-access-control).

    If you can't access the API Details for a skill or assistant anymore, you might not have the access role that is required to use the instance-level API credentials. You can use a personal API key instead.

## 1 April 2020
{: #watson-assistant-apr012020}
{: release-note}

Plus plan changes
:   The Plus plan is now available starting at $120/month for 1,000 users on pay-as-you-go or subscription IBM Cloud accounts. And you can subscribe without contacting Sales.

French language beta support added for contextual entities
:   You can add contextual entities to French-language dialog skills. For more information about contextual entities, see [Creating entities](/docs/watson-assistant?topic=watson-assistant-entities#entities-annotations-overview).

New API version
:   The current API version is now `2020-04-01`. The following change was made with this version:

    - An `integrations` property was added to the V2 `/message` context. The service now expects the `context.integrations` property to conform to a specific schema in which the allowed values are as follows:

        - `chat`
        - `facebook`
        - `intercom`
        - `liveengage`
        - `salesforce`
        - `slack`
        - `service_desk`
        - `text_messaging`
        - `voice_telephony`
        - `zendesk`

    If your app uses a `context.integrations` property that does not conform to the schema, a 400 error code will be returned.

## 31 March 2020
{: #watson-assistant-mar312020}
{: release-note}

The web chat integration was updated
:   The update adds an `isTrackingEnabled` parameter. You can add this parameter and set it to `false` to add the `X-Watson-Learning-Opt-Out` header to each `/message` request that originates from the web chat. For more information about the header, see [Data collection](https://{DomainName}/assistant/assistant-v2#data-collection){: external}. For more information about the parameter, see [Configuration](https://integrations.us-south.assistant.watson.cloud.ibm.com/web/developer-documentation/api-configuration){: external}.

## 26 March 2020
{: #watson-assistant-mar262020}
{: release-note}

The Covid-19 content catalog is available in Brazilian Portuguese, French, and Spanish
:   The content catalog defines a group of intents that recognize the common types of questions people ask about the novel coronavirus. You can use the catalog to jump-start development of chatbots that can answer questions about the virus and help to minimize the anxiety and misinformation associated with it. For more information about how to add a content catalog to your skill, see [Using content catalogs](/docs/watson-assistant?topic=watson-assistant-catalog).

## 19 March 2020
{: #watson-assistant-mar192020}
{: release-note}

A Covid-19 content catalog is available
:   The English-only content catalog defines a group of intents that recognize the common types of questions people ask about the novel coronavirus. The World Health Organization characterized COVID-19 as a pandemic on 11 March 2020. You can use the catalog to jump-start development of chatbots that can answer questions about the virus and help to minimize the anxiety and misinformation associated with it. For more information about how to add a content catalog to your skill, see [Using content catalogs](/docs/watson-assistant?topic=watson-assistant-catalog).

Fixed a problem with missing User Conversation data
:   A recent change resulted in no logs being shown in the User Conversations page unless you had a skill as the chosen data source. And the chosen skill had to be the same skill (with same skill ID) that was connected to the assistant when the user messages were submitted.

## 18 March 2020
{: #watson-assistant-mar182020}
{: release-note}

Technology preview is discontinued
:   The technology preview user interface was replaced with the {{site.data.keyword.assistant_classic_short}} standard user interface. If you used an Actions page to create actions and steps for your skill previously, you cannot access the Actions page anymore. Instead, use the Intents and Dialog pages to work with your skill.

## 16 March 2020
{: #watson-assistant-mar162020}
{: release-note}

Instructions updated for Slack integrations
:   The steps required to set up a Slack integration have changed to reflect permission assignment changes that were made by Slack. For more information, see [Integrating with Slack](/docs/watson-assistant?topic=watson-assistant-deploy-slack).

Order of response types is preserved
:   Previously, if you included a response type of **Search skill** in a list of response types for a dialog node, the search results were displayed last despite its placement in the list. This behavior was changed to show the search results in the appropriate order, namely in the sequence in which the search skill response type is listed for the dialog node.

## 10 March 2020
{: #watson-assistant-mar102020}
{: release-note}

Contextual entity support is generally available
:   You can add contextual entities to English-language dialog skills. For more information about contextual entities, see [Creating entities](/docs/watson-assistant?topic=watson-assistant-entities#entities-annotations-overview).

French language support added for autocorrection
:   Autocorrection helps your assistant understand what your customers want. It corrects misspellings in the input that customers submit before the input is evaluated. With more precise input, your assistant can more easily recognize entity mentions and understand the customer's intent. For more information, see [Autocorrecting user input](/docs/watson-assistant?topic=watson-assistant-autocorrection).

The new system entities are used by new skills
:   For new English, Brazilian Portuguese, Czech, Dutch, French, German, Italian, and Spanish dialog skills, the new system entities are enabled automatically. If you decide to turn on a system entity and add it to your dialog, it's the new and improved version of the system entity that is used. For more information, see [System entities](/docs/watson-assistant?topic=watson-assistant-system-entities).

## 6 March 2020
{: #watson-assistant-mar062020}
{: release-note}

Transfer a web chat conversation to a human agent
:   Delight your customers with 360-degree support by integrating your web chat with a third-party service desk solution. When a customer asks to speak to a person, you can connect them to an agent through a service desk solution, such as Zendesk or Salesforce. Service desk support is a beta feature. For more information, see [Adding contact center support](/docs/watson-assistant?topic=watson-assistant-deploy-web-chat-haa).

## 2 March 2020
{: #watson-assistant-mar022020}
{: release-note}

Known issue accessing logs
:   If you cannot access user logs from the Analytics page, ask the owner of the service instance for the skill to change your service level access to make you a Manager of the instance. For more information about access control, see [Managing access](/docs/watson-assistant?topic=watson-assistant-access-control).

## 1 March 2020 deprecation notice
{: #watson-assistant-mar012020}
{: release-note}

March 2020 deprecation notice
:   To help us continue to improve and expand the capabilities of the assistants you build with {{site.data.keyword.assistant_classic_short}}, we are deprecating some of the older technologies. Support for the older technologies will end in June 2020. Take action now to test and adopt the new technologies, so your skills and assistants will be ready when the old technologies stop being supported.

    The following technologies are being deprecated:

    - **Legacy version of numeric system entities**

        We released a whole new infrastructure for our numeric system entities across all languages except Chinese, Korean, Japanese and Arabic. The updated `@sys-number`, `@sys-date`, `@sys-time`, `@sys-currency`, and `@sys-percentage` entities provide superior number recognition with higher precision. For more information about the new system entities, see [System entities](/docs/watson-assistant?topic=watson-assistant-system-entities).

        The old version of the numeric system entities will stop being supported in June 2020 for English, Brazilian Portuguese, Czech, Dutch, French, German, Italian, and Spanish dialog skills.

        ***Action***: In each dialog skill where you use numeric system entities, go to the **Options>System entities** page and turn on the new system entities. Take some time to test the new version of system entities with your own dialogs to make sure they continue to work as expected. As you adopt the new system entities, share your feedback about your experience with the new technology.

    - **Person and location system entities**

        The `@sys-person` and `@sys-location` system entities, which were available in English as a beta only, are being deprecated. Consider using contextual entities as a way to capture these types of proper nouns. Instead of trying to add a dictionary-based entity that covers every permutation of the names for people or cities, for example, you can teach your skill to recognize the context in which such names are used. For more information about contextual entities, see [Annotation-based method](/docs/watson-assistant?topic=watson-assistant-entities#entities-annotations-overview).

        ***Action***: Remove references to `@sys-person` and `@sys-location` from your dialogs. Turn off the `@sys-person` and `@sys-location` system entities to prevent yourself or others from adding them to a dialog inadvertently.

    - **Irrelevance detection**

        We revised the irrelevance detection classification algorithm to make it even smarter out of the box. Now, even before you begin to teach the system about irrelevant requests, it is able to recognize user input that your skill is not designed to address. For more information, see [Irrelevance detection](/docs/watson-assistant?topic=watson-assistant-irrelevance-detection).

        ***Action***: In each dialog skill, go to the **Options>Irrelevance detection** page and turn on the new classification model. Make sure everything works as well, if not better, than it did before. Share your feedback.

    - **Old API version dates**

        v1 API versions that are dated on or before `2017-02-03` are being deprecated. When you send calls to the service with earlier API version dates, they will receive properly formatted and valid responses for a time, so you can gracefully transition to using the later API versions. However, the confidence scores and other results that are sent in the response will reflect those generated by a more recent version of the API.

        ***Action***: Do some testing of calls with the latest version to verify that things work as expected. Some functionality has changed over the last few years. After testing, change the version date on any API calls that you make from your applications.

## 28 February 2020
{: #watson-assistant-feb282020}
{: release-note}

{{site.data.keyword.assistant_classic_full}} is available in {{site.data.keyword.icp4dfull_notm}}
:   The service can be installed on-premises in environments where {{site.data.keyword.icp4dfull_notm}} 2.5 is installed on OpenShift or standalone. Version 2.5 has been deprecated, and documentation is no longer online; we recommend [upgrading to the latest version](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.7.x?topic=upgrading). 

## 26 February 2020
{: #watson-assistant-feb262020}
{: release-note}

Slot `Save it as` field retains your edits
:   When you edit what gets saved for a slot by using the JSON editor to edit the value of the context variable to be something other than what is specified in the **Check for** field, your changes are kept even if someone subsequently clicks the **Save it as** field.

## 20 February 2020
{: #watson-assistant-feb202020}
{: release-note}

Access control changes are coming
:   Notifications are displayed in the user interface for anyone with Reader and Writer level access to a service instance. The notification explains that access control is going to change soon, and that what they can do in the instance will change unless they are given Manager service access beforehand.

## 14 February 2020
{: #watson-assistant-feb142020}
{: release-note}

More web chat color settings
:   You can now specify the color of more elements of the web chat integration. For example, you can define one color for the web chat window header. You can define a different color for the user message bubble. And another color for interactive components, such as the launcher button for the chat.

## 13 February 2020
{: #watson-assistant-feb132020}
{: release-note}

Track API events
:   Premium plan users can now use the Activity Tracker service to track how users and applications interact with {{site.data.keyword.assistant_classic_full}} in {{site.data.keyword.cloud}}. See [Using {{site.data.keyword.at_full_notm}} to audit user activity](/docs/watson-assistant?topic=watson-assistant-admin-auditing).

## 5 February 2020
{: #watson-assistant-feb052020}
{: release-note}

New API version
:   The current API version is now `2020-02-05`. The following changes were made with this version:

    - When a dialog node's response type is `connect-to-agent`, the node's `title` is used as the `topic` value. Previously, `user_label` was used.

    - The `alternate_intents` property is stored as a Boolean value instead of a String.

## 4 February 2020
{: #watson-assistant-feb042020}
{: release-note}

Product user interface makeover
:   The UI has been updated to be more intuitive, responsive, and consistent across its pages. While the look and feel of the UI elements has changed, their function has not.

Requesting early access
:   The button you click to request participation in the early access program has moved from the Skills page to the user account menu.

## 24 January 2020
{: #watson-assistant-jan242020}
{: release-note}

New system entities are now generally available in multiple languages
:   The new and improved numeric system entities are now generally available in all supported languages, except Arabic, Chinese, Japanese, and Korean, where they are available as a beta feature. They are not used by your dialog skill unless you enable them from the **Options>System entities** page. For more information, see [System entities](/docs/watson-assistant?topic=watson-assistant-system-entities).

## 14 January 2020
{: #watson-assistant-jan142020}
{: release-note}

Fixed an error message that was displayed when opening an instance
:   An error that was displayed when you launched {{site.data.keyword.assistant_classic_short}} from the {{site.data.keyword.cloud}} dashboard has been fixed. Previously, an error message that said, `Module 'ui-router' is not available! You either misspelled the module name or forgot to load it` would sometimes be displayed.

## 12 December 2019
{: #watson-assistant-dec122019}
{: release-note}

Support for private network endpoints
:   Users of Premium plans can create private network endpoints to connect to {{site.data.keyword.assistant_classic_short}} over a private network. Connections to private network endpoints do not require public internet access. For more information, see [Private network endpoints](/docs/watson-assistant?topic=watson-assistant-admin-securing#security-private-endpoints).

Full support for IBM Cloud IAM
:   {{site.data.keyword.assistant_classic_short}} now supports the full implementation of {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). API keys for Watson services are no longer limited to a single service instance. You can create access policies and API keys that apply to more than one service, and you can grant access between services.

    - To support this change, the API service endpoints use a different domain and include the service instance ID. The pattern is `api.{location}.{offering}.watson.cloud.ibm.com/instances/{instance_id}`.

        Example URL for an instance hosted in the Dallas location: `api.us-south.assistant.watson.cloud.ibm.com/instances/6bbda3b3-d572-45e1-8c54-22d6ed9e52c2`

        The previous public endpoint domain was `watsonplatform.net`.

        For more information, see the [API reference](https://{DomainName}/assistant/assistant-v2#service-endpoint){: external}.

        These URLs do not introduce a breaking change. The new URLs work both for your existing service instances and for new instances. The original URLs continue to work on your existing service instances for at least one year (until December 2020).

    - For more information, see [Authenticating to Watson services](/docs/watson?topic=watson-iam){: external}.

## 26 November 2019
{: #watson-assistant-nov262019}
{: release-note}

Disambiguation is available to everyone
:   Disambiguation is now available to users of every plan type.

    The following changes were made to how it functions:

    - The text that you add to the dialog **node name** field now matters.

    - The text in the node name field might be shown to customers. The disambiguation feature shows it to customers if the assistant needs to ask them to clarify their meaning. The text you add as the node name must identify the purpose of the node clearly and succinctly, such as *Place an order* or *Get plan information*.

        If the *External node name* field exists and contains a summary of the node's purpose, then its summary is shown in the disambiguation list instead. Otherwise, the dialog node name content is shown.

      - Disambiguation is enabled automatically for all nodes. You can disable it for the entire dialog or for individual dialog nodes.

      - When testing, you might notice that the order of the options in the disambiguation list changes from one test run to the next. Don't worry; this new behavior is intended. As part of work being done to help the assistant learn automatically from user choices, the order of the options in the disambiguation list is being randomized on purpose. Changing the order helps to avoid bias that can be introduced by a percentage of people who always pick the first option without first reviewing their choices.

## 12 November 2019
{: #watson-assistant-nov122019}
{: release-note}

Slot prompt JSON editor
:   You can now use the context or JSON editors for the slot response field where you define the question that your assistant asks to get information it needs from the customer. For more information about slots, see [Gathering information with slots](/docs/watson-assistant?topic=watson-assistant-dialog-slots).

New South Korea location
:   You can now create {{site.data.keyword.assistant_classic_short}} instances in the Seoul location. As with other locations, the {{site.data.keyword.cloud_notm}} Seoul location uses token-based Identity and Access Management (IAM) authentication.

Technology preview
:   A technology preview experience was released. A select set of new users are being presented with a new user interface that takes a different approach to building an assistant.

## 7 November 2019
{: #watson-assistant-nov072019}
{: release-note}

Irrelevance detection has been added
:   When enabled, a supplemental model is used to help identify utterances that are irrelevant and should not be answered by the dialog skill. This new model is especially beneficial for skills that have not been trained on what subjects to ignore. This feature is available for English skills only. For more information, see [Irrelevance detection](/docs/watson-assistant?topic=watson-assistant-irrelevance-detection).

Time zone support for now() method
:   You can now specify the time zone for the date and time that is returned by the `now()` method. See [Now()](/docs/watson-assistant?topic=watson-assistant-dialog-methods#dialog-methods-dates-now).

## 24 October 2019
{: #watson-assistant-oct242019}
{: release-note}

Testing improvement
:   You can now see the top three intents that were recognized in a test user input from the "Try it out" pane.

Error message when opening an instance
:   When you launch {{site.data.keyword.assistant_classic_short}} from the {{site.data.keyword.cloud}} dashboard, you might see an error message that says, `Module 'ui-router' is not available! You either misspelled the module name or forgot to load it.` You can ignore the message. Refresh the web browser page to close the notification.

## 14 October 2019
{: #watson-assistant-oct142019}
{: release-note}

Deploy your assistant in minutes
:   Create a web chat integration to embed your assistant into a page on your website as a chat widget. See [Web chat overview](/docs/watson-assistant?topic=watson-assistant-web-chat-overview).

UI changes
:   The main menu options of **Assistants** and **Skills** have moved from being displayed in the page header to being shown as icons on the side of the page. The tabbed pages for the tools you use to develop a dialog skill were moved to a secondary navigation bar that is displayed when you open the skill.

Rich response types are supported in a dialog node with slots
:   You can display a list of options for a user to choose from as the prompt for a slot, for example.

Change to switching service instances
:   Where you go to switch service instances has changed.

Known issue: Cannot rename search skills
:   You currently cannot rename a search skill after you create it.

## 9 October 2019
{: #watson-assistant-oct092019}
{: release-note}

New system entities changes
:   The following updates have been made:

    - In addition to English and German, the new numeric system entities are now available in these languages: Brazilian Portuguese, Czech, French, Italian, and Spanish.

    - The `part_of_day` property of the `@sys-time` entity now returns a time range instead of a single time value.

## 23 September 2019
{: #watson-assistant-sep232019}
{: release-note}

Dallas updates
:   The updates from 20 September are now available to service instances hosted in Dallas.

## 20 September 2019
{: #watson-assistant-sep202019}
{: release-note}

Inactivity timeout increase
:   The maximum inactivity timeout can now be extended to up to 7 days for Premium plans. See [Inactivity timeout](/docs/watson-assistant?topic=watson-assistant-publish-overview#publish-overview-environment-settings-inactivity).

Pattern entity fix
:   A change that was introduced in the previous release which changed all alphabetic characters to lowercase at the time an entity value was added has been fixed. The case of any alphabetic characters that are part of a pattern entity value are no longer changed when the value is added.

Dialog text response syntax fix
:   Fixed a bug in which the format of a dialog response reverted to an earlier version of the JSON syntax. Standard text responses were being saved as `output.text` instead of `output.generic`. For more information about the `output` object, see [Personalizing the dialog with context](/docs/watson-assistant?topic=watson-assistant-dialog-runtime-context).

## 13 September 2019
{: #watson-assistant-sep132019}
{: release-note}

Improved Entities and Intents page responsiveness
:   The Entities and Intents pages were updated to use a new JavaScript library that increases the page responsiveness. As a result, the look of some graphical user interface elements, such as buttons, changed slightly, but the function did not.

Creating contextual entities got easier
:   The process you use to annotate entity mentions from intent user examples was improved. You can now put the intent page into annotation mode to more easily select and label mentions. See [Adding contextual entities](/docs/watson-assistant?topic=watson-assistant-entities#entities-create-annotation-based).

## 6 September 2019
{: #watson-assistant-sep062019}
{: release-note}

Label character limit increase
:   The limit to the number of characters allowed for a label that you define for an option response type changed from 64 characters to 2,048 characters.

## 12 August 2019
{: #watson-assistant-aug122019}
{: release-note}

New dialog method
:   The `getMatch` method was added. You can use this method to extract a specific occurrence of a regular expression pattern that recurs in user input. For more details, see [dialog methods](/docs/watson-assistant?topic=watson-assistant-dialog-methods#dialog-methods-strings-getMatch).

## 9 August 2019
{: #watson-assistant-aug092019}
{: release-note}

Introductory product tour
:   For some first-time users, a new introductory product tour is shown that the user can choose to follow to perform the initial steps of creating an assistant.

## 1 August 2019
{: #watson-assistant-aug012019}
{: release-note}

Webhook callouts are available
:   Add webhooks to dialog nodes to make programmatic calls to an external application as part of the conversational flow. The new Webhook support simplifies the callout implementation process. (No more `action` JSON objects required.) For more information, see [Making a programmatic call from a dialog node](/docs/watson-assistant?topic=watson-assistant-dialog-webhooks).

Improved dialog page responsiveness
:   In all service instances, the user interface of the Dialog page was updated to use a new JavaScript library that increases the page responsiveness. As a result, the look of some graphical user interface elements, such as buttons, changed slightly, but the function did not.

## 31 July 2019
{: #watson-assistant-jul312019}
{: release-note}

Search skill and autocorrection are generally available
:   The search skill and spelling autocorrection features, which were previously available as beta features, are now generally available.

    - Search skills can be created by users of Plus or Premium plans only.

    - You can enable autocorrection for English-language dialog skills only. It is enabled automatically for new English-language dialog skills.

## 26 July 2019
{: #watson-assistant-jul262019}
{: release-note}

Missing skills issue is resolved
:   In some cases, workspaces that were created through the API only were not being displayed when you opened the {{site.data.keyword.assistant_classic_short}} user interface. This issue has been addressed. All workspaces that you create by using the API are displayed as dialog skills when you open the user interface.

## 23 July 2019
{: #watson-assistant-ju23l2019}
{: release-note}

Dialog search is fixed
:   In some skills, the search function was not working in the Dialog page. The issue is now fixed.

## 17 July 2019
{: #watson-assistant-jul172019}
{: release-note}

Disambiguation choice limit
:   You can now set the maximum number of options to show to users when the assistant asks them to clarify what they want to do. For more information about disambiguation, see [Disambiguation](/docs/watson-assistant?topic=watson-assistant-dialog-runtime#dialog-runtime-disambiguation).

Dialog search issue
:   In some skills, the search function is not working in the Dialog page. A new user interface library, which increases the page responsiveness, is being rolled out to existing service instances in phases. This search issue affects only dialog skills for which the new library is not yet enabled.

Missing skills issue
:   In some cases, workspaces that were created through the API only are not being displayed when you open the {{site.data.keyword.assistant_classic_short}} user interface. Normally, these workspaces are displayed as dialog skills. If you do not see your skills from the UI, don't worry; they are not gone. Contact support to report the issue, so the team can enable the workspaces to be displayed properly.

## 15 July 2019
{: #watson-assistant-jul152019}
{: release-note}

Numeric system entities upgrade available in Dallas
:   The new system entities are now also available as a beta feature for instances that are hosted in Dallas. See [System entities](/docs/watson-assistant?topic=watson-assistant-system-entities).

## 12 June 2019
{: #watson-assistant-jun122019}
{: release-note}

Numeric system entities upgrade
:   New system entities are available as a beta feature that you can enable in dialog skills that are written in English or German. The revised system entities offer better date and time understanding. They can recognize date and number spans, national holiday references, and classify mentions with more precision. For example, a date such as `May 15` is recognized as a date mention(`@sys-date:2019-05-15`), and is *not* also identified as a number mention (`@sys-number:15`). See [System entities](/docs/watson-assistant?topic=watson-assistant-system-entities).

A Plus Trial plan is available
:   You can use the free Plus Trial plan to try out the features of the Plus plan as you make a purchasing decision. The trial lasts for 30 days. After the trial period ends, if you do not upgrade to a Plus plan, your Plus Trial instance is converted to a Lite plan instance.

## 23 May 2019
{: #watson-assistant-may232019}
{: release-note}

Updated navigation
:   The home page was removed, and the order of the Assistants and Skills tabs was reversed. The new tab order encourages you to start your development work by creating an assistant, and then a skill.

Disambiguation settings have moved
:   The toggle to enable disamibugation, which is a feature that is available to Plus and Premium plan users only, has moved. The **Settings** button was removed from the **Dialog** page. You can now enable disambiguation and configure it from the skill's **Options** tab.

An introductory tour is now available
:   A short product tour is now displayed when a new service instance is created. Brand new users are also given help as they start development. A new assistant is created for them automatically. Informational popups are displayed to introduce the product user interface features, and guide the new user toward taking the key first step of creating a dialog skill.

## 10 April 2019
{: #watson-assistant-apr102019}
{: release-note}

Autocorrection is now available
:   Autocorrection is a beta feature that helps your assistant understand what your customers want. It corrects misspellings in the input that customers submit before the input is evaluated. With more precise input, your assistant can more easily recognize entity mentions and understand the customer's intent. See [Autocorrecting user input](/docs/watson-assistant?topic=watson-assistant-autocorrection) for more details.

## 22 March 2019
{: #watson-assistant-mar222019}
{: release-note}

Introducing search skill
:   A search skill helps you to make your assistant useful to customers faster. Customer inquiries that you did not anticipate and so have not built dialog logic to handle can be met with useful responses. Instead of saying it can't help, the assistant can query an external data source to find relevant information to share in its response. Over time, you can build dialog responses to answer customer queries that require follow-up questions to clarify the user's meaning or for which a short and clear response is suitable. And you can use search skill responses to address more open-ended customer queries that require a longer explanation. This beta feature is available to users of Premium and Plus service plans only.

    See [{{site.data.keyword.discoveryfull}} search integration setup](/docs/watson-assistant?topic=watson-assistant-search-add) for more details.

## 4 March 2019
{: #watson-assistant-mar042019}
{: release-note}

Simplified navigation
:   The sidebar navigation with separate *Build*,  *Improve*, and *Deploy* tabs has been removed. Now, you can get to all the tools you need to build a dialog skill from the main skill page.

Improve page is now called Analytics
:   The informational metrics that Watson generates from conversations between your users and your assistant moved from the *Improve* tab of the sidebar to a new tab on the main skill page called **Analytics**.

## 28 February 2019
{: #watson-assistant-feb282019}
{: release-note}

New API version
:   The current API version is now `2019-02-28`. The following changes were made with this version:

    - The order in which conditions are evaluated in nodes with slots has changed. Previously, if you had a node with slots that allowed for digressions away, the `anything_else` root node was triggered before any of the slot level Not found conditions could be evaluated. The order of operations has been changed to address this behavior. Now, when a user digresses away from a node with slots, all the root nodes except the `anything_else` node are processed. Next, the slot level Not found conditions are evaluated. And, finally, the root level `anything_else` node is processed. To better understand the full order of operations for a node with slots, see [Slot usage tips](/docs/watson-assistant?topic=watson-assistant-dialog-slots#dialog-slots-tips).

    - Strings that begin with a number sign (#) in the `context` or `output` objects of a message are no longer treated as intent references.

      Previously, these strings were treated as intents automatically. For example, if you specified a context variable, such as `"color":"#FFFFFF"`, then the hex color code (#FFFFFF) would be treated as an intent. Your assistant would check whether an intent named #FFFFFF was detected in the user's input, and if not, would replace #FFFFFF with `false`. This replacement no longer occurs.

      Similarly, if you included a number sign (#) in the text string in a node response, you used to have to escape it by preceding it with a back slash (`\`). For example, `We are the \#1 seller of lobster rolls in Maine.` You no longer need to escape the `#` symbol in a text response.

      This change does not apply to node or conditional response conditions. Any strings that begin with a number sign (#) which are specified in conditions continue to be treated as intent references. Also, you can use SpEL expression syntax to force the system to treat a string in the `context` or `output` objects of a message as an intent. For example, specify the intent as `<? #intent-name ?>`.

## 25 February 2019
{: #watson-assistant-feb252019}
{: release-note}

Slack integration enhancement
:   You can now choose the type of event that triggers your assistant in a Slack channel. Previously, when you integrated your assistant with Slack, the assistant interacted with users through a direct message channel. Now, you can configure the assistant to listen for mentions, and respond when it is mentioned in other channels. You can choose to use one or both event types as the mechanism through which your assistant interacts with users.

## 11 February 2019
{: #watson-assistant-feb112019}
{: release-note}

Integrate with Intercom
:   Intercom, a leading customer service messaging platform, has partnered with IBM to add a new agent to the team, a virtual {{site.data.keyword.assistant_classic_short}}. You can integrate your assistant with an Intercom application to enable the app to seamlessly pass user conversations between your assistant and human support agents. This integration is available to Plus and Premium plan users only. See [Integrating with Intercom](/docs/watson-assistant?topic=watson-assistant-deploy-intercom) for more details.

## 8 February 2019
{: #watson-assistant-feb082019}
{: release-note}

Version your skills
:   You can now capture a snapshot of the the intents, entities, dialog, and configuration settings for a skill at key points during the development process. With versions, it's safe to get creative. You can deploy new design approaches in a test environment to validate them before you apply any updates to a production deployment of your assistant. See [Managing workflow with versions](/docs/watson-assistant?topic=watson-assistant-versions) for more details.

Arabic content catalog
:   Users of Arabic-language skills can now add prebuilt intents to their dialogs. See [Using content catalogs](/docs/watson-assistant?topic=watson-assistant-catalog) for more information.

## 17 January 2019
{: #watson-assistant-jan172019}
{: release-note}

Czech language support is generally available
:   Support for the Czech language is no longer classified as beta; it is now generally available. See [Supported languages](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-codes) for more information.

Language support improvements
:   The language understanding components were updated to improve the following features:

    - German and Korean system entities

    - Intent classification tokenization for Arabic, Dutch, French, Italian, Japanese, Portuguese, and Spanish

## 4 January 2019
{: #watson-assistant-jan042019}
{: release-note}

IBM Cloud Functions in DC and London locations
:   You can now make programmatic calls to IBM Cloud Functions from the dialog of an assistant in a service instance that is hosted in the London and Washington, DC data centers. See [Making programmatic calls from a dialog node](/docs/watson-assistant?topic=watson-assistant-dialog-actions-client).

New methods for working with arrays
:   The following SpEL expression methods are available that make it easier to work with array values in your dialog:

    - **JSONArray.filter**: Filters an array by comparing each value in the array to a value that can vary based on user input.
    - **JSONArray.includesIntent**: Checks whether an `intents` array contains a particular intent.
    - **JSONArray.indexOf**: Gets the index number of a specific value in an array.
    - **JSONArray.joinToArray**: Applies formatting to values that are returned from an array.

   See the [array method documentation](/docs/watson-assistant?topic=watson-assistant-dialog-methods#dialog-methods-arrays) for more details.

## 13 December 2018
{: #watson-assistant-dec132018}
{: release-note}

London data center
:   You can now create {{site.data.keyword.assistant_classic_short}} service instances that are hosted in the London data center without syndication. See [Data centers](/docs/watson-assistant?topic=watson-assistant-admin-managing-plan#admin-managing-plan-regions) for more details.

Dialog node limit changes
:   The dialog node limit was temporarily changed from 100,000 to 500 for new Standard plan instances. This limit change was later reversed. If you created a Standard plan instance during the time frame in which the limit was in effect, your dialogs might be impacted. The limit was in effect for skills created between 10 December and 12 December 2018. The lower limits will be removed from all impacted instances in January. If you need to have the lower limit lifted before then, open a support ticket.

## 1 December 2018
{: #watson-assistant-dec012018}
{: release-note}

Determine the number of dialog nodes
:   To determine the number of dialog nodes in a dialog skill, do one of the following things:

     - From the tool, if it is not associated with an assistant already, add the dialog skill to an assistant, and then view the skill tile from the main page of the assistant. The *trained data* section lists the number of dialog nodes.

     - Send a GET request to the /dialog_nodes API endpoint, and include the `include_count=true` parameter. For example:

        ```curl
        curl -u "apikey:{apikey}" "https://{service-hostname}/assistant/api/v1/workspaces/{workspace_id}/dialog_nodes?version=2018-09-20&include_count=true"
        ```
        {: codeblock}

        where {service-hostname} is the appropriate URL for your instance. For more details, see [Service endpoint](https://{DomainName}/assistant/assistant-v1#service-endpoint){: external}.

        In the response, the `total` attribute in the `pagination` object contains the number of dialog nodes.

## 27 November 2018
{: #watson-assistant-nov272018}
{: release-note}

A new service plan, the Plus plan, is available
:   The new plan offers premium-level features at a lower price point. Unlike previous plans, the Plus plan is a user-based billing plan. It measures usage by the number of unique users that interact with your assistant over a given time period. To get the most from the plan, if you build your own client application, design your app such that it defines a unique ID for each user, and passes the user ID with each /message API call. For the built-in integrations, the session ID is used to identify user interactions with the assistant. See [User-based plans explained](/docs/watson-assistant?topic=watson-assistant-admin-managing-plan#admin-managing-plan-user-based) for more information.

    | Artifact | Limit |
    | --- | --- |
    | Assistants | 100 |
    | Contextual entities | 20 |
    | Contextual entity annotations | 2,000 |
    | Dialog nodes | 100,000 |
    | Entities | 1,000 |
    | Entity synonyms | 100,000 |
    | Entity values | 100,000 |
    | Intents | 2,000 |
    | Intent user examples | 25,000 |
    | Integrations | 100 |
    | Logs | 30 days |
    | Skills | 50 |
    {: caption="Plus plan limits" caption-side="top"}

User-based Premium plan
:   The Premium plan now bases its billing on the number of active unique users. If you choose to use this plan, design any custom applications that you build to properly identify the users who generate /message API calls. For more information, see [User-based plans](/docs/watson-assistant?topic=watson-assistant-admin-managing-plan#admin-managing-plan-user-based).

    Existing Premium plan service instances are not impacted by this change; they continue to use API-based billing methods. Only existing Premium plan users will see the API-based plan listed as the *Premium (API)* plan option.

    See {{site.data.keyword.assistant_classic_short}} [service plan options](https://www.ibm.com/products/watsonx-assistant/pricing){: external} for more information about all available service plans.

## 20 November 2018
{: #watson-assistant-nov202018}
{: release-note}

Recommendations are discontinued
:   The Recommendations section on the Improve tab was removed. Recommendations was a beta feature available to Premium plan users only. It recommended actions that users could take to improve their training data. Instead of consolidating recommendations in one place, recommendations are now being made available from the parts of the tool where you make actual training data changes. For example, while adding entity synonyms, you can now opt to see a list of synonymous terms that are recommended by Watson.

## 9 November 2018
{: #watson-assistant-nov092018}
{: release-note}

Major user interface revision
:   The {{site.data.keyword.assistant_classic_short}} service has a new look and added features.

    This version of the tool was evaluated by beta program participants over the past several months.

    - **Skills**: What you think of as a *workspace* is now called a *skill*. A *dialog skill* is a container for the natural language processing training data and artifacts that enable your assistant to understand user questions, and respond to them.

    **Where are my workspaces?** Any workspaces that you created previously are now listed in your service instance as skills. Click the **Skills** tab to see them.

    - **Assistants**: You can now publish your skill in just two steps. Add your skill to an assistant, and then set up one or more integrations with which to deploy your skill. The assistant adds a layer of function to your skill that enables {{site.data.keyword.assistant_classic_short}} to orchestrate and manage the flow of information for you.

    - **Built-in integrations**: Instead of going to the **Deploy** tab to deploy your workspace, you add your dialog skill to an assistant, and add integrations to the assistant through which the skill is made available to your users. You do not need to build a custom front-end application and manage the conversation state from one call to the next. However, you can still do so if you want to.

    - **New major API version**: A V2 version of the API is available. This version provides access to methods you can use to interact with an assistant at run time. No more passing context with each API call; the session state is managed for you as part of the assistant layer.

    What is presented in the tooling as a dialog skill is effectively a wrapper for a V1 workspace. There are currently no API methods for authoring skills and assistants with the V2 API. However, you can continue to use the V1 API for authoring workspaces. See [API Overview](/docs/watson-assistant?topic=watson-assistant-api-overview) for more details.

    - **Switching data sources**: It is now easier to improve the model in one skill with user conversation logs from a different skill. You do not need to rely on deployment IDs, but can simply pick the name of the assistant to which a skill was added and deployed to use its data. See [Improving across assistants](/docs/watson-assistant?topic=watson-assistant-logs#logs-deploy-id).

    - **Preview links from London instances**: If your service instance is hosted in London, then you must edit the preview link URL. The URL includes a region code for the region where the instance is hosted. Because instances in London are syndicated to Dallas, you must replace the `eu-gb` reference in the URL with `us-south` for the preview web page to render properly.

## 8 November 2018
{: #watson-assistant-nov082018}
{: release-note}

Japanese data center
:   You can now create {{site.data.keyword.assistant_classic_short}} service instances that are hosted in the Tokyo data center. See [Data centers](/docs/watson-assistant?topic=watson-assistant-admin-managing-plan#admin-managing-plan-regions) for more details.

## 30 October 2018
{: #watson-assistant-oct302018}
{: release-note}

New API authentication process
:   The {{site.data.keyword.assistant_classic_short}} service transitioned from using Cloud Foundry to using token-based Identity and Access Management (IAM) authentication in the following regions:

    - Dallas (us-south)
    - Frankfurt (eu-de)

    For new service instances, you use IAM for authentication. You can pass either a bearer token or an API key. Tokens support authenticated requests without embedding service credentials in every call. API keys use basic authentication.

    For all existing service instances, you continue to use service credentials (`{username}:{password}`) for authentication.

## 25 October 2018
{: #watson-assistant-oct252018}
{: release-note}

Entity synonym recommendations are available in more languages
:   Synonym recommendation support was added for the French, Japanese, and Spanish languages.

## 26 September 2018
{: #watson-assistant-sep262018}
{: release-note}

{{site.data.keyword.assistant_classic_full}} is available in {{site.data.keyword.icpfull}}
:   {{site.data.keyword.assistant_classic_full}} is available in {{site.data.keyword.icpfull}}

## 21 September 2018
{: #watson-assistant-sep212018}
{: release-note}

New API version
:   The current API version is now `2018-09-20`. In this version, the `errors[].path` attribute of the error object that is returned by the API is expressed as a [JSON Pointer](https://tools.ietf.org/html/rfc6901){: external} instead of in dot notation form.

Web actions support
:   You can now call {{site.data.keyword.openwhisk_short}} web actions from a dialog node. See [Making programmatic calls from a dialog node](/docs/watson-assistant?topic=watson-assistant-dialog-actions-client) for more details.

## 15 August 2018
{: #watson-assistant-aug152018}
{: release-note}

Entity fuzzy matching support improvements
:   Fuzzy matching is fully supported for English entities, and the misspelling feature is no longer a Beta-only feature for many other languages. See [Supported languages](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-codes) for details.

## 6 August 2018
{: #watson-assistant-aug062018}
{: release-note}

Intent conflict resolution
:   The tool can now help you to resolve conflicts when two or more user examples in separate intents are similar to one another. Non-distinct user examples can weaken the training data and make it harder for your assistant to map user input to the appropriate intent at run time.

Disambiguation
:   Enable disambiguation to allow your assistant to ask the user for help when it needs to decide between two or more viable dialog nodes to process for a response. See [Disambiguation](/docs/watson-assistant?topic=watson-assistant-dialog-runtime#dialog-runtime-disambiguation) for more details.

Jump-to fix
:   Fixed a bug in the Dialogs tool which prevented you from being able to configure a jump-to that targets the response of a node with the `anything_else` special condition.

Digression return message
:   You can now specify text to display when the user returns to a node after a digression. The user will have seen the prompt for the node already. You can change the message slightly to let users know they are returning to where they left off. For example, specify a response like, `Where were we? Oh, yes...` See [Digressions](/docs/watson-assistant?topic=watson-assistant-dialog-runtime#dialog-runtime-digressions) for more details.

## 12 July 2018
{: #watson-assistant-jul122018}
{: release-note}

Rich response types
:   You can now add rich responses that include elements such as images or buttons in addition to text, to your dialog. See [Rich responses](/docs/watson-assistant?topic=watson-assistant-dialog-overview#dialog-overview-multimedia) for more information.

Contextual entities (Beta)
:   Contextual entities are entities that you define by labeling mentions of the entity type that occur in intent user examples. These entity types teach your assistant not only terms of interest, but also the context in which terms of interest typically appear in user utterances, enabling your assistant to recognize never-seen-before entity mentions based solely on how they are referenced in user input. For example, if you annotate the intent user example, `I want a flight to Boston` by labeling `Boston` as a `@destination` entity, then your assistant can recognize `Chicago` as a `@destination` mention in a user input that says, `I want a flight to Chicago.` This feature is currently available for English only. See [Adding contextual entities](/docs/watson-assistant?topic=watson-assistant-entities#entities-create-annotation-based) for more information.

    When you access the tool with an Internet Explorer web browser, you cannot label entity mentions in intent user examples nor edit user example text.

New API version
:   The current API version is now `2018-07-10`. This version introduces the following changes:

    - The content of the /message `output` object changed from being a `text` JSON object to being a `generic` array that supports multiple rich response types, including `image`, `option`, `pause`, and `text`.
    - Support for contextual entities was added.
    - You can no longer add user-defined properties in `context.metadata`. However, you can add them directly to `context`.

Overview page date filter
:   Use the new date filters to choose the period for which data is displayed. These filters affect all data shown on the page: not just the number of conversations displayed in the graph, but also the statistics displayed along with the graph, and the lists of top intents and entities. See [Controls](/docs/watson-assistant?topic=watson-assistant-logs-overview#logs-overview-controls) for more information.

Pattern limit expanded
:   When using the **Patterns** field to [define specific patterns for an entity value](/docs/watson-assistant?topic=watson-assistant-entities#entities-patterns), the pattern (regular expression) is now limited to 512 characters.

## 2 July 2018
{: #watson-assistant-jul022018}
{: release-note}

Jump-tos from conditional responses
:   You can now configure a conditional response to jump directly to another node. See [Conditional responses](/docs/watson-assistant?topic=watson-assistant-dialog-overview#dialog-overview-multiple) for more details.

## 21 June 2018
{: #watson-assistant-jun212018}
{: release-note}

Language updates for system entities
:   Dutch and Simplified Chinese language support are now generally available. Dutch language support includes fuzzy matching for misspellings. Traditional Chinese language support includes the availability of [system entities](/docs/watson-assistant?topic=watson-assistant-system-entities) in beta release. See [Supported languages](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-codes) for details.

## 14 June 2018
{: #watson-assistant-jun142018}
{: release-note}

Washington, DC data center opens
:   You can now create {{site.data.keyword.assistant_classic_short}} service instances that are hosted in the Washington, DC data center. See [Data centers](/docs/watson-assistant?topic=watson-assistant-admin-managing-plan#admin-managing-plan-regions) for more details.

New API authentication process
:   The {{site.data.keyword.assistant_classic_short}} service has a new API authentication process for service instances that are hosted in the following regions:

    - Washington, DC (us-east) as of 14 June 2018
    - Sydney, Australia (au-syd) as of 7 May 2018

    {{site.data.keyword.cloud}} is migrating to token-based Identity and Access Management (IAM) authentication.

    For new service instances in the regions listed, you use IAM for authentication. You can pass either a bearer token or an API key. Tokens support authenticated requests without embedding service credentials in every call. API keys use basic authentication.

    For all new and existing service instances in other regions, you continue to use service credentials (`{username}:{password}`) for authentication.

    When you use any of the Watson SDKs, you can pass the API key and let the SDK manage the lifecycle of the tokens. For more information and examples, see [Authentication](https://{DomainName}/assistant/assistant-v2#authentication){: external} in the API reference.

    If you are not sure which type of authentication to use, view the {{site.data.keyword.assistant_classic_short}} credentials by clicking the service instance from the Services section of the [{{site.data.keyword.Bluemix_notm}} Resource List](){: external}.

## 25 May 2018
{: #watson-assistant-may252018}
{: release-note}

New sample workspace
:   The sample workspace that is provided for you to explore or to use as a starting point for your own workspace has changed. The **Car Dashboard** sample was replaced by a **Customer Service** sample. The new sample showcases how to use content catalog intents and other newer features to build a bot. It can answer common questions, such as inquiries about store hours and locations, and illustrates how to use a node with slots to schedule in-store appointments.

HTML rendering was added to Try it out
:   The "Try it out" pane now renders HTML formatting that is included in response text. Previously, if you included a hypertext link as an HTML anchor tag in a text response, you would see the HTML source in the "Try it out" pane during testing. It used to look like this:

    `Contact us at <a href="https://www.ibm.com">ibm.com</a>.`

    Now, the hypertext link is rendered as if on a web page. It is displayed like this:

    `Contact us at` [ibm.com](https://www.ibm.com){: external}.

    Remember, you must use the appropriate type of syntax in your responses for the client application to which you will deploy the conversation. Only use HTML syntax if your client application can interpret it properly. Other integration channels might expect other formats.

Deployment changes
:   The **Test in Slack** option was removed.

## 11 May 2018
{: #watson-assistant-may112018}
{: release-note}

Information security
:   The documentation includes some new details about data privacy. Read more in [Securing your assistant](/docs/watson-assistant?topic=watson-assistant-admin-securing).

## 7 May 2018
{: #watson-assistant-may072018}
{: release-note}

Sydney, Australia data center opens
:   You can now create {{site.data.keyword.assistant_classic_short}} service instances that are hosted in the Sydney, Australia data center. See [IBM Cloud global data centers](https://www.ibm.com/cloud/data-centers/){: external} for more details.

## 4 April 2018
{: #watson-assistant-apr042018}
{: release-note}

Search dialogs
:   You can now [search dialog nodes](/docs/watson-assistant?topic=watson-assistant-dialog-tasks#dialog-tasks-search) for a given word or phrase.

## 15 March 2018
{: #watson-assistant-mar152018}
{: release-note}

Introducing {{site.data.keyword.assistant_classic_full}}
:   {{site.data.keyword.ibmwatson}} Conversation has been renamed. It is now called {{site.data.keyword.assistant_classic_full}}. The name change reflects the fact that {{site.data.keyword.assistant_classic_short}} is expanding to provide prebuilt content and tools that help you more easily share the virtual assistants you build. Read [this blog post](https://www.ibm.com/blogs/watson/2018/03/the-future-of-watson-conversation-watson-assistant/){: external} for more details.

New REST APIs and SDKs are available for {{site.data.keyword.assistant_classic_short}}
:   The new APIs are functionally identical to the existing Conversation APIs, which continue to be supported. For more information about the {{site.data.keyword.assistant_classic_short}} APIs, see the [API Reference](https://{DomainName}/assistant/assistant-v1){: external}.

Dialog enhancements
:   The following features were added to the dialog tool:

    - Simple variable name and value fields are now available that you can use to add context variables or update context variable values. You do not need to open the JSON editor unless you want to. See [Defining a context variable](/docs/watson-assistant?topic=watson-assistant-dialog-runtime-context#dialog-runtime-context-var-define) for more details.
    - Organize your dialog by using folders to group together related dialog nodes. See [Organizing the dialog with folders](/docs/watson-assistant?topic=watson-assistant-dialog-tasks#dialog-tasks-folders) for more details.
    - Support was added for customizing how each dialog node participates in user-initiated digressions away from the designated dialog flow. See [Digressions](/docs/watson-assistant?topic=watson-assistant-dialog-runtime#dialog-runtime-digressions) for more details.

Search intents and entities
:   A new search feature has been added that allows you to [search intents](/docs/watson-assistant?topic=watson-assistant-intents#intents-search) for user examples, intent names, or descriptions, or to [search entity](/docs/watson-assistant?topic=watson-assistant-entities#entities-search) values and synonyms.

Content catalogs
:   The new [content catalogs](/docs/watson-assistant?topic=watson-assistant-catalog#catalog-add) contain a single category of prebuilt common intents and entities that you can add to your application. For example, most applications require a general `#greeting-type` intent that starts a dialog with the user. You can add it from the content catalog rather than building your own.

Enhanced user metrics
:   The Improve component has been enhanced with additional user metrics and logging statistics. For example, the Overview page includes several new, detailed graphs that summarize interactions between users and your application, the amount of traffic for a given time period, and the intents and entities that were recognized most often in user conversations.

## 12 March 2018
{: #watson-assistant-mar122018}
{: release-note}

New date and time methods
:   Methods were added that make it easier to perform date calculations from the dialog. See [Date and time calculations](/docs/watson-assistant?topic=watson-assistant-dialog-methods#dialog-methods-date-time-calculations) for more details.

## 16 February 2018
{: #watson-assistant-feb162018}
{: release-note}

Dialog node tracing
:   When you use the "Try it out" pane to test a dialog, a location icon is displayed next to each response. You can click the icon to highlight the path that your assistant traversed through the dialog tree to arrive at the response. See [Testing your dialog](/docs/watson-assistant?topic=watson-assistant-dialog-tasks#dialog-tasks-test) for details.

New API version
:   The current API version is now `2018-02-16`. This version introduces the following changes:

    - A new `include_audit` parameter is now supported on most GET requests. This is an optional boolean parameter that specifies whether the response should include the audit properties (`created` and `updated` timestamps). The default value is `false`. (If you are using an API version earlier than `2018-02-16`, the default value is `true`.) For more information, see the [API Reference](https://{DomainName}/assistant/assistant-v1){: external}.

    - Responses from API calls using the new version include only properties with non-`null` values.

    - The `output.nodes_visited` and `output.nodes_visited_details` properties of message responses now include nodes with the following types, which were previously omitted:

    - Nodes with `type`=`response_condition`
    - Nodes with `type`=`event_handler` and `event_name`=`input`

## 9 February 2018
{: #watson-assistant-feb092018}
{: release-note}

Dutch system entities (Beta)
:   Dutch language support has been enhanced to include the availability of [System entities](/docs/watson-assistant?topic=watson-assistant-system-entities) in beta release. See [Supported languages](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-codes) for details.

## 29 January 2018
{: #watson-assistant-jan292018}
{: release-note}

REST API now supports new request parameters
:   - Use the `append` parameter when updating a workspace to indicate whether the new workspace data should be added to the existing data, rather than replacing it. For more information, see [Update workspace](https://{DomainName}/assistant/assistant-v1?curl=#update-workspace){: external}.

   - Use the `nodes_visited_details` parameter when sending a message to indicate whether the response should include additional diagnostic information about the nodes that were visited during processing of the message. For more information, see [Send message](https://{DomainName}/assistant/assistant-v1?curl=#message){: external}.

## 23 January 2018
{: #watson-assistant-jan232018}
{: release-note}

Unable to retrieve list of workspaces
:   If you see this or similar error messages when working in the tooling, it might mean that your session has expired. Log out by choosing **Log out** from the **User information** icon, and then log back in.

## 8 December 2017
{: #watson-assistant-dec082017}
{: release-note}

Log data access across instances (Premium users only)
:   If you are a Premium user, your premium instances can optionally be configured to allow access to log data from workspaces across your different premium instances.

Copy nodes
:   You can now duplicate a node to make a copy of it and its children. This feature is helpful if you build a node with useful logic that you want to reuse elsewhere in your dialog. See [Copying a dialog node](/docs/watson-assistant?topic=watson-assistant-dialog-tasks#dialog-tasks-copy-node) for more information.

Capture groups in pattern entities
:   You can identify groups in the regular expression pattern that you define for an entity. Identifying groups is useful if you want to be able to refer to a subsection of the pattern later. For example, your entity might have a regex pattern that captures US phone numbers. If you identify the area code segment of the number pattern as a group, then you can subsequently refer to that group to access just the area code segment of a phone number. See [Defining information to look for in customer input](/docs/watson-assistant?topic=watson-assistant-entities#entities-creating-task) for more information.

## 6 December 2017
{: #watson-assistant-dec062017}
{: release-note}

{{site.data.keyword.openwhisk}} integration (Beta)
:   Call {{site.data.keyword.openwhisk}} (formerly IBM OpenWhisk) actions directly from a dialog node. This feature enables you to, for example, call an action to retrieve weather information from within a dialog node, and then condition on the returned information in the dialog response. Currently, you can call an action from a {{site.data.keyword.openwhisk_short}} instance that is hosted in the US South region from instances that are hosted in the US South region. See [Making programmatic calls from a dialog node](/docs/watson-assistant?topic=watson-assistant-dialog-actions-client) for more details.

## 5 December 2017
{: #watson-assistant-dec052017}
{: release-note}

Redesigned UI for Intents and Entities
:   The `Intents` and `Entities` tabs have been redesigned to provide an easier, more efficient workflow when creating and editing entities and intents. See [Creating intents](/docs/watson-assistant?topic=watson-assistant-intents) and [Defining information to look for in customer input](/docs/watson-assistant?topic=watson-assistant-entities) for information about working with these tabs.

## 30 November 2017
{: #watson-assistant-nov302017}
{: release-note}

Eastern Arabic numeral support
:   Eastern Arabic numerals are now supported in Arabic system entities.

## 29 November 2017
{: #watson-assistant-nov292017}
{: release-note}

Improving understanding of user input across workspaces
:   You can now improve a workspace with utterances that were sent to other workspaces within your instance. For example, you might have multiple versions of production workspaces and development workspaces; you can use the same utterance data to improve any of these workspaces. See [Improving across workspaces](/docs/watson-assistant?topic=watson-assistant-logs#logs-deploy-id).

## 20 November 2017
{: #watson-assistant-nov202017}
{: release-note}

GB18030 compliance
:   GB18030 is a Chinese standard that specifies an extended code page for use in the Chinese market. This code page standard is important for the software industry because the China National Information Technology Standardization Technical Committee has mandated that any software application that is released for the Chinese market after September 1, 2001, be enabled for GB18030. The service supports this encoding, and is certified GB18030-compliant.

## 9 November 2017
{: #watson-assistant-nov092017}
{: release-note}

Intent examples can directly reference entities
:   You can now specify an entity reference directly in an intent example. That entity reference, along with all its values or synonyms, is used by the service classifier for training the intent. For more information, see [Directly referencing an entity name in an intent example](/docs/watson-assistant?topic=watson-assistant-intents#intents-entity-as-example).

    Currently, you can only directly reference closed entities that you define. You cannot directly reference [pattern entities](/docs/watson-assistant?topic=watson-assistant-entities#entities-patterns) or [system entities](/docs/watson-assistant?topic=watson-assistant-system-entities).

## 8 November 2017
{: #watson-assistant-nov082017}
{: release-note}

New connector tool
:   You can use the new connector tool to connect your workspace to a Slack or Facebook Messenger app that you own, making it available as a chatbot that Slack or Facebook Messenger users can interact with. This tool is available only for the {{site.data.keyword.Bluemix_notm}} US South region.

## 3 November 2017
{: #watson-assistant-nov032017}
{: release-note}

Dialog updates
:   The following updates make is easier for you to build a dialog. (See [Creating a dialog](/docs/watson-assistant?topic=watson-assistant-dialog-build) for details.)

    - You can add a condition to a slot to make it required only if certain conditions are met. For example, you can make a slot that asks for the name of a spouse required only if a previous (required) slot that asks for marital status indicates that the user is married.

    - You can now choose **Skip user input** as the next step for a node. When you choose this option, after processing the current node, your assistant jumps directly to the first child node of the current node. This option is similar to the existing *Jump to* next step option, except that it allows for more flexibility. You do not need to specify the exact node to jump to. At run time, your assistant always jumps to whichever node is the first child node, even if the child nodes are reordered or new nodes are added after the next step behavior is defined.

    - You can add conditional responses for slots. For both Found and Not found responses, you can customize how your assistant responds based on whether certain conditions are met. This feature enables you to check for possible misinterpretations and correct them before saving the value provided by the user in the slot's context variable. For example, if the slot saves the user's age, and uses `@sys-number` in the *Check for* field to capture it, you can add a condition that checks for numbers over 100, and responds with something like, *Please provide a valid age in years.* See [Adding conditions to Found and Not found responses](/docs/watson-assistant?topic=watson-assistant-dialog-slots#dialog-slots-handler-next-steps) for more details.

    - The interface you use to add conditional responses to a node has been redesigned to make it easier to list each condition and its response. To add node-level conditional responses, click **Customize**, and then enable the **Multiple responses** option.

     The **Multiple responses** toggle sets the feature on or off for the node-level response only. It does not control the ability to define conditional responses for a slot. The slot multiple response setting is controlled separately.

    - To keep the page where you edit a slot simple, you now select menu options to a.) add a condition that must be met for the slot to be processed, and b.) add conditional responses for the Found and Not found conditions for a slot. Unless you choose to add this extra functionality, the slot condition and multiple responses fields are not displayed, which declutters the page and makes it easier to use.

## 25 October 2017
{: #watson-assistant-oct252017}
{: release-note}

Updates to Simplified Chinese
:   Language support has been enhanced for Simplified Chinese. This includes intent classification improvements using character-level word embeddings, and the availability of system entities. Note that the service learning models may have been updated as part of this enhancement, and when you retrain your model any changes will be applied.

Updates to Spanish
:   Improvements have been made to Spanish intent classification, for very large datasets.

## 11 October 2017
{: #watson-assistant-oct112017}
{: release-note}

Updates to Korean
:   Language support has been enhanced for Korean. Note that the service learning models may have been updated as part of this enhancement, and when you retrain your model any changes will be applied.

## 3 October 2017
{: #watson-assistant-oct032017}
{: release-note}

Pattern-defined entities (Beta)
:   You can now define specific patterns for an entity, using regular expressions. This can help you identify entities that follow a defined pattern, for example SKU or part numbers, phone numbers, or email addresses. See [Pattern-defined entities](/docs/watson-assistant?topic=watson-assistant-entities#entities-patterns) for additional details.

    - You can add either synonyms or patterns for a single entity value; you cannot add both.
    - For each entity value, there can be a maximum of up to 5 patterns.
    - Each pattern (regular expression) is limited to 128 characters.
    - Importing or exporting via a CSV file does not currently support patterns.
    - The REST API does not support direct access to patterns, but you can retrieve or modify patterns using the `/values` endpoint.

Fuzzy matching filtered by dictionary (English only)
:   An improved version of fuzzy matching for entities is now available, for English. This improvement prevents the capturing of some common, valid English words as fuzzy matches for a given entity. For example, fuzzy matching will not match the entity value `like` to `hike` or `bike`, which are valid English words, but will continue to match examples such as `lkie` or `oike`.

## 27 September 2017
{: #watson-assistant-sep272017}
{: release-note}

Condition builder updates
:   The control that is displayed to help you define a condition in a dialog node has been updated. Enhancements include support for listing available context variable names after you enter the $ to begin adding a context variable.

## 31 August 2017
{: #watson-assistant-aug312017}
{: release-note}

Improve section rollback
:   The median conversation time metric, and corresponding filters, are being temporarily removed from the Overview page of the Improve section. This removal will prevent the calculation of certain metrics from causing the median conversation time metric, and the conversations over time graph, to display inaccurate information. IBM regrets removing functionality from the tool, but is committed to ensuring that we are communicating accurate information to users.

Dialog node names
:   You can now assign any name to a dialog node; it does not need to be unique. And you can subsequently change the node name without impacting how the node is referenced internally. The name you specify is saved as a title attribute of the node in the workspace JSON file and the system uses a unique ID that is stored in the name attribute to reference the node.

## 23 August 2017
{: #watson-assistant-aug232017}
{: release-note}

Updates to Korean, Japanese, and Italian
:   Language support has been enhanced for Korean, Japanese, and Italian. Note that the service learning models may have been updated as part of this enhancement, and when you retrain your model any changes will be applied.

## 10 August 2017
{: #watson-assistant-aug102017}
{: release-note}

Accent normalization
:   In a conversational setting, users may or may not use accents while interacting with the service. As such, an update has been made to the algorithm so that accented and non-accented versions of words are treated the same for intent detection and entity recognition.

    However, for some languages like Spanish, some accents can alter the meaning of the entity. Thus, for entity detection, although the original entity may implicitly have an accent, your assistant can also match the non-accented version of the same entity, but with a slightly lower confidence score.

    For example, for the word `barrió`, which has an accent and corresponds to the past tense of the verb `barrer` (to sweep), your assistant can also match the word `barrio` (neighborhood), but with a slightly lower confidence.

    The system will provide the highest confidence scores in entities with exact matches. For example, `barrio` will not be detected if `barrió` is in the training set; and `barrió` will not be detected if `barrio` is in the training set.

    You are expected to train the system with the proper characters and accents. For example, if you are expecting `barrió` as a response, then you should put `barrió` into the training set.

    Although not an accent mark, the same applies to words using, for example, the Spanish letter `ñ` versus the letter `n`, such as `uña` versus `una`. In this case the letter `ñ` is not simply an `n` with an accent; it is a unique, Spanish-specific letter.

    You can enable fuzzy matching if you think your customers will not use the appropriate accents, or misspell words (including, for example, putting a `n` instead of a `ñ`), or you can explicitly include them in the training examples.

    **Note:** Accent normalization is enabled for Portuguese, Spanish, French, and Czech.

Workspace opt-out flag
:   The REST API now supports an opt-out flag for workspaces. This flag indicates that workspace training data such as intents and entities are not to be used by IBM for general service improvements. For more information, see the [API Reference](https://{DomainName}/assistant/assistant-v1?curl=#data-collection){: external}

## 7 August 2017
{: #watson-assistant-aug072017}
{: release-note}

`Next` and `last` date interpretation
:   The service treats `last` and `next` dates as referring to the most immediate last or next day referenced, which may be in either the same or a previous week. See the [system entities](/docs/watson-assistant?topic=watson-assistant-system-entities#system-entities-sys-date-time) topic for additional information.

## 3 August 2017
{: #watson-assistant-aug032017}
{: release-note}

Fuzzy matching for additional languages (Beta)
:   Fuzzy matching for entities is now available for additional languages, as noted in the [Supported languages](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-codes) topic.

Partial match (Beta - English only)
:   Fuzzy matching will now automatically suggest substring-based synonyms present in user-defined entities, and assign a lower confidence score as compared to the exact entity match. See [Fuzzy matching](/docs/watson-assistant?topic=watson-assistant-entities#entities-fuzzy-matching) for details.

## 28 July 2017
{: #watson-assistant-jul282017}
{: release-note}

Updates
:   This release includes the following updates:

    - When you set bidirectional preferences for the tooling, you can now specify the graphical user interface direction.
    - The color scheme of the tooling was updated to be consistent with other Watson services and products.

## 19 July 2017
{: #watson-assistant-jul192017}
{: release-note}

REST API now supports access to dialog nodes
:   The REST API now supports access to dialog nodes. For more information, see the [API Reference](https://{DomainName}/assistant/assistant-v1?curl=#listdialognodes){: external}.

## 14 July 2017
{: #watson-assistant-jul142017}
{: release-note}

Slots enhancement
:   The slots functionality of dialogs was enhanced. For example, a *slot_in_focus* property was added that you can use to define a condition that applies to a single slot only. See [Gathering information with slots](/docs/watson-assistant?topic=watson-assistant-dialog-slots) for details.

## 12 July 2017
{: #watson-assistant-jul122017}
{: release-note}

Support for Czech
:   Czech language support has been introduced. See [Supported languages](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-codes) for additional details.

## 11 July 2017
{: #watson-assistant-jul112017}
{: release-note}

Test in Slack
:   You can use the new **Test in Slack** tool to quickly deploy your workspace as a Slack bot user for testing purposes. This tool is available only for the {{site.data.keyword.Bluemix_notm}} US South region.

Updates to Arabic
:   Arabic language support has been enhanced to include absolute scoring per intent, and the ability to mark intents as irrelevant. See [Supported languages](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-codes) for additional details. Note that the service learning models may have been updated as part of this enhancement, and when you retrain your model any changes will be applied.

## 23 June 2017
{: #watson-assistant-jun232017}
{: release-note}

Updates to Korean
:   Korean language support has been enhanced. See [Supported languages](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-codes) for additional details. The service learning models may have been updated as part of this enhancement, and when you retrain your model any changes will be applied.

## 22 June 2017
{: #watson-assistant-jun222017}
{: release-note}

Introducing slots
:   It is now easier to collect multiple pieces of information from a user in a single node by adding slots. Previously, you had to create several dialog nodes to cover all the possible combinations of ways that users might provide the information. With slots, you can configure a single node that saves any information that the user provides, and prompts for any required details that the user does not. See [Gathering information with slots](/docs/watson-assistant?topic=watson-assistant-dialog-slots) for more details.

Simplified dialog tree
:   The dialog tree has been redesigned to improve its usability. The tree view is more compact so it is easier to see where you are within it. And the links between nodes are represented in a way that makes it easier to understand the relationships between the nodes.

## 21 June 2017
{: #watson-assistant-jun212017}
{: release-note}

Arabic support
:   Language support for Arabic is now generally available. For details, [Supported languages](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-codes).

Language updates
:   The service algorithms have been updated to improve overall language support. See [Supported languages](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-codes) for details.

## 16 June 2017
{: #watson-assistant-jun162017}
{: release-note}

Recommendations (Beta - Premium users only)
:   The Improve panel also includes a **Recommendations** page that recommends ways to improve your system by analyzing the conversations that users have with your chatbot, and taking into account your system's current training data and response certainty.

## 14 June 2017
{: #watson-assistant-jun142017}
{: release-note}

Fuzzy matching for additional languages (Beta)
:   Fuzzy matching for entities is now available for additional languages. For more information, see [Supported languages](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-codes). You can turn on fuzzy matching per entity to improve the ability of your assistant to recognize terms in user input with syntax that is similar to the entity, without requiring an exact match. The feature is able to map user input to the appropriate corresponding entity despite the presence of misspellings or slight syntactical differences. For example, if you define giraffe as a synonym for an animal entity, and the user input contains the terms `giraffes` or `girafe`, the fuzzy match is able to map the term to the animal entity correctly. See [Fuzzy matching](/docs/watson-assistant?topic=watson-assistant-entities#entities-fuzzy-matching) for details.

## 13 June 2017
{: #watson-assistant-jun132017}
{: release-note}

User conversations
:   The Improve panel now includes a **User conversations** page, which provides a list of user interactions with your chatbot that can be filtered by keyword, intent, entity, or number of days. You can open individual conversations to correct intents, or to add entity values or synonyms.

Regex change
:   The regular expressions that are supported by SpEL functions like find, matches, extract, replaceFirst, replaceAll and split have changed. A group of regular expression constructs are no longer allowed, including look-ahead, look-behind, possessive repetition and backreference constructs. This change was necessary to avoid a security exposure in the original regular expression library.

## 12 June 2017
{: #watson-assistant-jun122017}
{: release-note}

Updates
:   This release includes the following updates:
    - The maximum number of workspaces that you can create with the **Lite** plan (formerly named the Free plan) changed from 3 to 5.
    - You can now assign any name to a dialog node; it does not need to be unique. And you can subsequently change the node name without impacting how the node is referenced internally. The name you specify is treated as an alias and the system uses its own internal identifier to reference the node.
    - You can no longer change the language of a workspace after you create it by editing the workspace details. If you need to change the language, you can export the workspace as a JSON file, update the language property, and then import the JSON file as a new workspace.

## 6 June 2017
{: #watson-assistant-jun062017}
{: release-note}

Learn
:   A new *Learn about* page is available that provides getting started information and links to service documentation and other useful resources. To open the page, click the icon in the page header.

Bulk export and delete
:   You can now simultaneously export a number of intents or entities to a CSV file, so you can then import and reuse them for another application. You can also simultaneously select a number of entities or intents for deletion in bulk.

Updates to Korean
:   Korean tokenizers have been updated to address informal language support. IBM continues to work on improvements to entity recognition and classification.

Emoji support
:   Emojis added to intent examples, or as entity values, will now be correctly classified/extracted.

    Only emojis that are included in your training data will be correctly and consistently identified; emoji support may not correctly classify similar emojis with different color tones or other variations.

Entity stemming (Beta - English only)
:   The fuzzy matching beta feature recognizes entities and matches them based on the stem form of the entity value. For example, this feature correctly recognizes `bananas` as being similar to `banana`, and `run` being similar to `running` as they share a common stem form. For more information, see [Fuzzy matching](/docs/watson-assistant?topic=watson-assistant-entities#entities-fuzzy-matching).

Workspace import progress
:   When you import a workspace from a JSON file, a tile for the workspace is displayed immediately, in which information about the progress of the import is displayed.

Reduced training time
:   Multiple models are now trained in parallel, which noticeably reduces the training time for large workspaces.

## 26 May 2017
{: #watson-assistant-may262017}
{: release-note}

New API version
:   The current API version is now `2017-05-26`. This version introduces the following changes:

    - The schema of ErrorResponse objects has changed. This change affects all endpoints and methods. For more information, see the [API Reference](https://{DomainName}/assistant){: external}.
    - The internal schema used to represent dialog nodes in exported workspace JSON has changed. If you use the `2017-05-26` API to import a workspace that was exported using an earlier version, some dialog nodes might not import correctly. For best results, always import a workspace using the same version that was used to export it.

## 25 May 2017
{: #watson-assistant-may252017}
{: release-note}

Manage context variables
:   You can now manage context variables in the "Try it out" pane. Click the **Manage context** link to open a new pane where you can set and check the values of context variables as you test the dialog. See [Testing your dialog](/docs/watson-assistant?topic=watson-assistant-dialog-tasks#dialog-tasks-test) for more information.

## 16 May 2017
{: #watson-assistant-may162017}
{: release-note}

Updates
:   This release includes the following updates:

    - A **Car Dashboard** sample workspace is now available when you open the tool. To use the sample as a starting point for your own workspace, edit the workspace. If you want to use it for multiple workspaces, then duplicate it instead. The sample workspace does not count toward your subscription workspace total unless you use it.
    - It is now easier to navigate the tool. The navigation menu options are available from the side of the main page instead of the top. In the page header, breadcrumb links display that show you where you are. You can now switch between service instances from the Workspaces page. To get there quickly, click **Back to workspaces** from the navigation menu. If you have multiple service instances, the name of the current instance is displayed. You can click the **Change** link beside it to choose another instance.
    - When you create a dialog, two nodes are now added to it for you: 1) a **Welcome** node at the start the dialog tree that contains the greeting to display to the user and 2) an **Anything else** node at the end of the tree that catches any user inquiries that are not recognized by other nodes in the dialog and responds to them. See [Creating a dialog](/docs/watson-assistant?topic=watson-assistant-dialog-build) for more details.
    - When you are testing a dialog in the "Try it out" pane, you can now find and resubmit a recent test utterance by pressing the Up key to cycle through your previous inputs.
    - Experimental Korean language support for 5 system entities (`@sys-date`, `@sys-time`, `@sys-currency`, `@sys-number`, `@sys-percentage`) is now available. There are known issues for some of the numeric entities, and limited support for informal language input.
    - An Overview page is available from the Improve tab. The page provides a summary of interactions with your bot. You can view the amount of traffic for a given time period, as well as the intents and entities that were recognized most often in user conversations. For additional information, see [Dialog skill analytics overview](/docs/watson-assistant?topic=watson-assistant-logs-overview).

## 27 April 2017
{: #watson-assistant-apr272017}
{: release-note}

System entities
:   The following system entities are now available as beta features in English only:

    - sys-location: Recognizes references to locations, such as towns, cities, and countries, in user utterances.
    - sys-person: Recognizes references to people's names, first and last, in user utterances.

    For more information, see the [System entities reference](/docs/watson-assistant?topic=watson-assistant-system-entities).

Fuzzy matching for entities
:   Fuzzy matching for entities is a beta feature that is now available in English. You can turn on fuzzy matching per entity to improve the ability of your assistant to recognize terms in user input with syntax that is similar to the entity, without requiring an exact match. The feature is able to map user input to the appropriate corresponding entity despite the presence of misspellings or slight syntactical differences. For examples, if you define **giraffe** as a synonym for an animal entity, and the user input contains the terms `giraffes` or `girafe`, the fuzzy match is able to map the term to the animal entity correctly. See [How fuzzy matching works](/docs/watson-assistant?topic=watson-assistant-entities#entities-fuzzy-matching).

## 18 April 2017
{: #watson-assistant-apr182017}
{: release-note}

Updates
:   This release includes the following updates:

    - The REST API now supports access to the following resources:
        - entities
        - entity values
        - entity value synonyms
        - logs

        For more information, see the [API Reference](https://{DomainName}/assistant/assistant-v1){: external}.

    - The behavior of the /messages `POST` method has changed the handling of entities and intents specified as part of the message input:
        - If you specify intents on input, your assistant uses the intents you specify, but uses natural language processing to detect entities in the user input.
        - If you specify entities on input, your assistant uses the entities you specify, but uses natural language processing to detect intents in the user input.

        The behavior has not changed for messages that specify both intents and entities, or for messages that specify neither.

    - The option to mark user input as irrelevant is now available for all supported languages. This is a beta feature.

    - A new Credentials tab provides a single place where you can find all of the information you need for connecting your application to a workspace, as well as other deployment options. To access the Credentials tab for your workspace, click the icon and select **Credentials**.

## 9 March 2017
{: #watson-assistant-mar092017}
{: release-note}

REST API updates
:   The REST API now supports access to the following resources:

    - workspaces
    - intents
    - examples
    - counterexamples

    For more information, see the [API Reference](https://{DomainName}/assistant/assistant-v1){: external}.

## 7 March 2017
{: #watson-assistant-mar072017}
{: release-note}

Intent name restrictions
:   The use of `.` or `..` as an intent name causes problems and is no longer supported. You cannot rename or delete an intent with this name; to change the name, export your intents to a file, rename the intent in the file, and import the updated file into your workspace. Paying customers can contact support for a database change.

## 1 March 2017
{: #watson-assistant-mar012017}
{: release-note}

System entities are now enabled in German
:   System entities are now enabled in German.

## 22 February 2017
{: #watson-assistant-feb222017}
{: release-note}

Messages are now limited to 2,048 characters
: Messages are now limited to 2,048 characters.

## 3 February 2017
{: #watson-assistant-feb032017}
{: release-note}

Updates
:   This release includes the following updates:

    - We changed how intents are scored and added the ability to mark input as irrelevant to your application.

    - This release introduced a major change to the workspace. To benefit from the changes, you must manually upgrade your workspace.

    - The processing of **Jump to** actions changed to prevent loops that can occur under certain conditions. Previously, if you jumped to the condition of a node and neither that node nor any of its peer nodes had a condition that was evaluated as true, the system would jump to the root-level node and look for a node whose condition matched the input. In some situations this processing created a loop, which prevented the dialog from progressing.

     Under the new process, if neither the target node nor its peers is evaluated as true, the dialog turn is ended. To reimplement the old model, add a final peer node with a condition of `true`. In the response, use a **Jump to** action that targets the condition of the first node at the root level of your dialog tree.

## 11 January 2017
{: #watson-assistant-jan112017}
{: release-note}

Customize node titles
:   In this release, you can customize node titles in dialog.

## 22 December 2016
{: #watson-assistant-dec222016}
{: release-note}

Node title section
:   In this release, dialog nodes display a new section for `node title`. The ability to customize the `node title` is not available. When collapsed, the `node title` displays the `node condition` of the dialog node. If there is not a `node condition`, "Untitled Node" is displayed as the title.

## 19 December 2016
{: #watson-assistant-dec192016}
{: release-note}

Dialog editor UI changes
:   Several changes make the dialog editor easier and more intuitive to use:

    - A larger editing view makes it easier to view all the details of a node as you work on it.
    - A node can contain multiple responses, each triggered by a separate condition. For more information see [Responses](/docs/watson-assistant?topic=watson-assistant-dialog-overview#dialog-overview-responses).

## 5 December 2016
{: #watson-assistant-dec052016}
{: release-note}

Updates
:   This release includes the following updates:

    - New languages are supported, all in Experimental mode: German, Traditional Chinese, Simplified Chinese, and Dutch.
    - Two new system entities are available: @sys-date and @sys-time. For details, see [System entities](/docs/watson-assistant?topic=watson-assistant-system-entities).

## 21 October 2016
{: #watson-assistant-oct212016}
{: release-note}

Updates
:   This release includes the following updates:

    - The service now provides system entities, which are common entities that can be used across any use case.
    - You can now view a history of conversations with users on the Improve page. You can use this to understand the behavior of your chatbot.
    - You can now import entities from a comma-separated value (CSV) file, which helps with when you have a large number of entities.

## 20 September 2016
{: #watson-assistant-sep202016}
{: release-note}

New version 2016-09-20

:   To take advantage of the changes in a new version, change the value of the `version` parameter to the new date. If you're not ready to update to this version, don't change your version date.

    - version **2016-09-20**: `dialog_stack` changed from an array of strings to an array of JSON objects.

## 29 August 2016
{: #watson-assistant-aug292016}
{: release-note}

Updates
:   This release includes the following updates:

    - You can move dialog nodes from one branch to another, as siblings or peers. 
    - You can expand the JSON editor window.
    - You can view chat logs of your bot's conversations to help you understand it's behavior. You can filter by intents, entities, date, and time.

## 11 July 2016
{: #watson-assistant-jul212016}
{: release-note}

General Availability
:    This General Availability release enables you to work with entities and dialogs to create a fully functioning bot.

## 18 May 2016
{: #watson-assistant-may182016}
{: release-note}

Experimental release
:   This Experimental release introduces the user interface and enables you to work with workspaces, intents, and examples.

