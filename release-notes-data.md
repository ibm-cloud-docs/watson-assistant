---

copyright:
  years: 2015, 2023
lastupdated: "2023-10-24"

subcollection: watson-assistant

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}}
{: #release-notes-data}

[{{site.data.keyword.icp4dfull_notm}}]{: tag-cp4d}

Use these release notes to learn about the latest updates to {{site.data.keyword.assistant_classic_full}} for {{site.data.keyword.icp4dfull}}.
{: shortdesc}

## Web chat versions
{: #release-notes-web-chat}

When you install {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}}, the latest available version of the web chat integration is included. See the following table for details about the latest available web chat version for each {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} release. If your web chat version isn't locked, then the web chat integration is upgraded to the latest available version when you upgrade {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}}.

The following table shows the latest version of the web chat integration that is included with each release of {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}}. {{site.data.keyword.icp4dfull}} supports web chat versions 5.1.1 or later. To customize and change version numbers, see [Controlling the web chat version](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-versions).

| {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} version | Latest web chat version available |
|----------------|----------------|
| 4.7.2 | [7.5.0](/docs/watson-assistant?topic=watson-assistant-release-notes-chat#7.5.0) |
| 4.7.1 | [7.4.0](/docs/watson-assistant?topic=watson-assistant-release-notes-chat#7.4.0) |
| 4.7.0 | [7.3.0](/docs/watson-assistant?topic=watson-assistant-release-notes-chat#7.3.0) |
| 4.6.5 | [7.2.0](/docs/watson-assistant?topic=watson-assistant-release-notes-chat#7.2.0) |
| 4.6.3 | [7.1.0](/docs/watson-assistant?topic=watson-assistant-release-notes-chat#7.1.0) |
| 4.6.2 | [7.0.0](/docs/watson-assistant?topic=watson-assistant-release-notes-chat#7.0.0) |
| 4.6.0 | [6.7.0](/docs/watson-assistant?topic=watson-assistant-release-notes-chat#6.7.0) |
| 4.5.3 | [6.6.2](/docs/watson-assistant?topic=watson-assistant-release-notes-chat#6.6.2) |
| 4.5.1 | [6.5.2](/docs/watson-assistant?topic=watson-assistant-release-notes-chat#6.5.2) |
| 4.5.0 | [6.4.1](/docs/watson-assistant?topic=watson-assistant-release-notes-chat#6.4.1) |
| 4.0.8 | [6.2.0](/docs/watson-assistant?topic=watson-assistant-release-notes-chat#6.2.0) |
{: caption="Web chat versions in {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}}" caption-side="top"}

## 30 August 2023
{: #assistant-data-aug302023}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} Version 4.7.2 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.7.2 is compatible with {{site.data.keyword.icp4dfull}} Version 4.7. See the [support matrix](/docs/watson-assistant?topic=watson-assistant-install#install-support-matrix) for more details. 

Multiple validation responses
:   When you edit a validation for a customer response, you can now include several validation responses. For more information, see [Customizing validation for a response](/docs/watson-assistant?topic=watson-assistant-handle-errors#customize-validation).

Multilingual downloads
:   You can download language data files, in CSV format, so that you can translate training examples and assistant responses into other languages for use in other assistants. For more information, see [Using multilingual downloads for translation](/docs/watson-assistant?topic=watson-assistant-admin-language-support).

Algorithm for improved intent detection and action matching
:   You can now use the algorithm version Beta, which includes a new foundation model that is trained with a transformer architecture. The Beta algorithm provides the following improvements:  

   - Improved intent detection and action matching for English, French, German, Portuguese (Brazilian), and Spanish
   - Improved robustness to variations in user inputs such as typos and different inflection forms
   - Reduction in the amount of training data required to reach the same level of performance compared to previous algorithms

   For more information, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

Fallback choice for dynamic options
:   The dynamic options response type now includes a fallback static choice, such as "None of the above", if the options aren't what the customer wants. You can then add a step that is conditioned on this static option to provide further assistance. For more information, see [Dynamic options](/docs/watson-assistant?topic=watson-assistant-dynamic-options).

Option to allow change of topic between actions and dialog
:   If you are using actions and dialog, there is a new setting you can use to ensure that customers can change topics between an action and a dialog node. For more information, see [Allow change of topic between actions and dialog](/docs/watson-assistant?topic=watson-assistant-change-topic).

Action and collection names must now be unique
:   With this release, each action name must be different from other action names, and each collection name must be different from other collection names. If your existing actions or collections have duplicate names, a warning icon will appear in the Status column. For more information, see [Overview: Editing actions](/docs/watson-assistant?topic=watson-assistant-build-actions-overview) and [Organizing actions in collections](/docs/watson-assistant?topic=watson-assistant-collections).

## 26 July 2023
{: #assistant-data-jul262023}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} Version 4.7.1 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.7.1 is compatible with {{site.data.keyword.icp4dfull}} Version 4.7. See the [support matrix](/docs/watson-assistant?topic=watson-assistant-install#install-support-matrix) for more details. 

Edit step titles
:  You can now add and edit titles for each step, which can help you more easily identify what a step does in an action. For more information, see [Editing actions](/docs/watson-assistant?topic=watson-assistant-build-actions-overview).

Filtering the list of actions
:   You can locate specific actions by filtering the list by subactions, by custom extension, or by variable. For more information, see [Filtering actions](/docs/watson-assistant?topic=watson-assistant-filter-actions).

See which actions use a specific variable
:   The Variables page now includes a new *Actions count* column. You can click on the number in the column to see which actions use a variable. For more information, see [Creating a session variable](/docs/watson-assistant?topic=watson-assistant-manage-info#create-session-variable).

New expression choice for setting a session variable
:   Previously, to use an expression to set or modify a variable value, you needed to pick an existing variable or create a new one and select the expression option. Now you can use a new **Expression** choice to write an expression directly without first picking a variable. For more information, see [Storing a value in a session variable](/docs/watson-assistant?topic=watson-assistant-manage-info#store-session-variable).

Changes to validation of OpenAPI specifications 
:   When you build a custom extension, you work with OpenAPI specification files. This release includes changes to the validation of OpenAPI files, which might affect the connection between your actions and extensions 

   You can import an action with references to a custom extension and {{site.data.keyword.assistant_classic_short}} can automatically connect the action and extension. With the validation change, modifications to the OpenAPI specification for your custom extension might affect this automatic connection. For more information, see [Building a custom extension](/docs/watson-assistant?topic=watson-assistant-build-custom-extension).

Changes to the date and number formats in assistant responses
:   You might see changes to the date and number formats in assistant responses.

   Examples of date changes include removed or added periods, such as:
   -  In Spanish, `18 abr. 2021` changes to `18 abr 2021`
   -  In Portuguese, `18 de abr` changes to `18 de abr.`

   The delimiter character changes for numbers in some languages. For example, in French, nonbreaking space (NBSP) changes to narrow no-break space (NNBSP).

   These changes are the result of migrating the {{site.data.keyword.assistant_classic_short}} platform to Java 17, where locale values are updated by using specifications in [CLDR 39](https://cldr.unicode.org/index/downloads/cldr-39){: external}. 
   
   To avoid or minimize the impact of similar changes in the future, you can use [Display formats](/docs/watson-assistant?topic=watson-assistant-actions-global-settings#actions-global-settings-display-formats).

Differences in contextual entity detection for dialog skills with few annotations
:   If you have 10 to 20 examples of contextual entities in your dialog skill, you might see differences in the entities detected due to updates made to address critical vulnerabilities. The impact of these differences is limited to only newly-trained models. Existing models are unaffected. You can mitigate these differences by annotating more examples. For more information, see [Annotation-based method](/docs/watson-assistant?topic=watson-assistant-entities#entities-annotations-overview).

## 28 June 2023
{: #assistant-data-jun282023}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} Version 4.7.0 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.7.0 is compatible with {{site.data.keyword.icp4dfull}} Version 4.7. See the [support matrix](/docs/watson-assistant?topic=watson-assistant-install#install-support-matrix) for more details. 

The new experience is now available for all new instances
:   When you create a new instance, the new experience will be the default interface to use for building your assistants. The new experience makes it easier to use actions to build customer conversations. If you don't want to use the new experience, you can use the Manage menu to switch to the classic experience. For details, see [Welcome to the new {{site.data.keyword.conversationshort}}](/docs/watson-assistant?topic=watson-assistant-welcome-new-assistant).

All languages are now enabled by default
:   You don't need to add languages during installation. All supported languages are now enabled by default with no increase in footprint. For details, see [Supported languages](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-codes).

New algorithm version Latest (20 Dec 2022) provides improved irrelevance detection
:   A new algorithm version is available. The Latest (20 Dec 2022) version includes a new irrelevance detection implementation to improve off-topic detection. For details, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

Actions templates updated with new design and new choices
:   The actions template catalog has a new design. Now you can select multiple templates at the same time. The catalog also has new and updated templates, including starter kits that you can use with external services such as Google and HubSpot. For details, see [Building actions from a template](/docs/watson-assistant?topic=watson-assistant-actions-templates).

Organize actions into collections
:   Now you can put actions into collections, which are folder-style groups based on whatever categorization you need at your organization, such as by use case, internal team, or status. For details, see [Organizing actions in collections](/docs/watson-assistant?topic=watson-assistant-collections).

Display iframe inline in the conversation
:   In the web chat, an assistant can now include an iframe response within the conversation. This new option is useful for smaller pieces of iframe content. For details, see [Adding an iframe response](/docs/watson-assistant?topic=watson-assistant-respond#respond-add-iframe).

New validation choices for date, time, and numeric customer responses
:   For Number, Date, Time, Currency, and Percentage customer responses, you can now customize the validation to check for a specific answer, such as a range of dates or a limited currency amount. For details, see [Customizing validation for a response](/docs/watson-assistant?topic=watson-assistant-handle-errors#customize-validation).

Confirmation to return to previous action
:   If a customer changes to a different topic, assistants now ask a "yes or no" confirmation question to determine whether the customer wants to return to the previous action. Previously, the assistant returned to the previous action without asking. New assistants are set to use this confirmation by default. For details, see [Confirmation to return to previous topic](/docs/watson-assistant?topic=watson-assistant-change-topic#change-topic-confirmation).

New "Never return" choice for when a customer changes topics
:   In some cases, you might not want a customer to return to a previous action after the customer changes the topic. To set up this option, use the new Never return choice in Action settings. For details, see [Disabling returning to the original topic](/docs/watson-assistant?topic=watson-assistant-change-topic#change-topic-never-return).

Allow changing topics in free text and regex responses
:   By default, customers can't change topics when the assistant is asking for a free text response or when an utterance matches the pattern in a regex response. Now free text and regex customer response types have a setting to allow a customer to digress and change topics. For details, see [Enabling changing the topic for free text and regex customer responses](/docs/watson-assistant?topic=watson-assistant-change-topic#change-topic-free-text-regex).

Adding and using multiple environments
:   Each assistant has a draft and live environment. You can now add up to three environments to test your assistant before deployment. You can build content in the draft environment and test versions of your content in the extra environments. For details, see [Adding and using multiple environments](/docs/watson-assistant?topic=watson-assistant-multiple-environments).

Display formats for variables
:   In the Global settings page for actions, you can use the Display formats tab to specify the display formats for variables that use date, time, numbers, currency, or percentages. You can also choose a default locale to ensure that the format of a variable that's displayed in the web chat is what you want for your assistant. For example, you can choose to have the output of a time variable appear in HH:MM format instead of HH:MM:SS. For details, see [Display formats](/docs/watson-assistant?topic=watson-assistant-actions-global-settings#actions-global-settings-display-formats).

Debug custom extensions
:   You can use the new extension inspector in the action editor Preview pane to debug problems with custom extensions. The extension inspector shows detailed information about what data is being sent to and returned from an external API. For details, see [Debugging failures](/docs/watson-assistant?topic=watson-assistant-call-extension#extension-debug).

New expression choice for setting a session variable
:   Previously, to use an expression to set or modify a variable value, you needed to pick an existing variable or create a new one and select the expression option. Now you can use a new Expression choice to write an expression directly without first picking a variable. For details, see [Storing a value in a session variable](/docs/watson-assistant?topic=watson-assistant-manage-info#store-session-variable).

Using the Cloud Object Storage importer to migrate chat logs
:   You can use the Cloud Object Storage importer service to migrate your chat logs from one installation of {{site.data.keyword.assistant_classic_short}} to another.For more information, see [Using the Cloud Object Storage importer to migrate chat logs](/docs/watson-assistant?topic=watson-assistant-cos-importer-data).

## 2 May 2023
{: #assistant-data-may022023}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} Version 4.6.5 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.6.5 is compatible with {{site.data.keyword.icp4dfull}} Version 4.6. See the [support matrix](/docs/watson-assistant?topic=watson-assistant-install#install-support-matrix) for more details. This release of {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} includes various fixes and features.

Algorithm version 01-Jun-2022 uses enhanced intent detection by default
:   The algorithm version **Latest (01-Jun-2022)** now uses enhanced intent detection by default. Before this change, some skills that did not include a specific algorithm version selection inadvertently used **Previous (01-Jan-2022)**. You can notice small changes in intent detection behavior when changes are made to an assistant that previously didn't have enhanced intent detection enabled. For more information, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

Test the **Beta** algorithm version now to prepare for release 4.7.0
:   The **Beta** algorithm version in release 4.6.5 includes a new irrelevance detection implementation to improve off-topic detection accuracy.

   Improvements include:
   - Relevant user inputs are expected to get higher confidence, so they are less likely to be considered irrelevant or require clarification
   - Irrelevance detection is improved in the presence of direct entity references
   - Irrelevance detection is more stable across small changes to input
   - Intent detection is more stable regarding occurrence of numerics, such as postal codes
   - For German-language assistants, intent detection is more robust in the presence of umlauts 

   In the forthcoming 4.7.0 release, it is planned that this **Beta** version will become the **Latest** version, replacing the current **Latest (01 Jun 2022)** version. You can test the **Beta** version in 4.6.5 now to prepare.

For more information, see [Algorithm version and training](/docs/watson-assistant?topic=watson-assistant-algorithm-version).

## 23 February 2023
{: #assistant-data-feb232023}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} Version 4.6.3 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.6.3 is compatible with {{site.data.keyword.icp4dfull}} Version 4.6. See the [support matrix](/docs/watson-assistant?topic=watson-assistant-install#install-support-matrix) for more details. This release of {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} includes various fixes and features.

## 30 January 2023
{: #assistant-data-jan302023}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} Version 4.6.2 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.6.2 is compatible with {{site.data.keyword.icp4dfull}} Version 4.6. See the [support matrix](/docs/watson-assistant?topic=watson-assistant-install#install-support-matrix) for more details. This release of {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} includes various fixes and features.

New {{site.data.keyword.assistant_classic_short}} v2 APIs
:   {{site.data.keyword.assistant_classic_short}} now provides new methods related to assistants, skills, environments, and releases. For details, see the [{{site.data.keyword.assistant_classic_short}} v2 API documentation](https://{DomainName}/assistant/assistant-v2){: external}.

## 30 November 2022
{: #assistant-data-nov302022}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} Version 4.6.0 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.6.0 is compatible with {{site.data.keyword.icp4dfull}} Version 4.6. See the [support matrix](/docs/watson-assistant?topic=watson-assistant-install#install-support-matrix) for more details. This release of {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} includes various fixes and features.

New {{site.data.keyword.conversationshort}} experience
:   With the new experience in {{site.data.keyword.conversationshort}}, you can build, test, publish, and analyze your assistant from one simple and intuitive interface that focuses on using actions to build customer conversations. To learn more about building your assistant with actions, see [Welcome to the new {{site.data.keyword.conversationshort}}](/docs/watson-assistant).

New algorithm version setting
:   You can now choose one of three {{site.data.keyword.assistant_classic_short}} algorithm version settings to apply to your future trainings: **Beta**, **Latest**, or **Previous**. This new **Algorithm Version** setting replaced **Intent Detection** in the **Options** section of a dialog skill. **Beta** and **Latest** use more enhanced intent detection that is available in more languages: Arabic, Chinese (Simplified), Chinese (Traditional) Czech, Dutch, French, German, Japanese, Korean, Italian, Portuguese, and Spanish. See [Algorithm version](/docs/watson-assistant?topic=watson-assistant-algorithm-version){: external}.

Credential rotation
:   You can now rotate your credentials for added data store security. See [Managing security for your {{site.data.keyword.assistant_classic_short}} datastores](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=administering-managing-security-your-datastores){: external}.

Autoscaling
:   Using Red Hat® OpenShift® Horizontal Pod Autoscaler, you can optionally enable autoscaling for {{site.data.keyword.assistant_classic_short}} so that the service dynamically scales up and down to make efficient use of cluster resources. For details, see [Automatically scaling resources for services](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-automatically-scaling){: external}.

New commands for shutting down and restarting services
:   The `cpd-cli` manage command now includes `shutdown` and `restart` sub-commands to make it easier to shut down and restart the {{site.data.keyword.icp4dfull}} services on your cluster. For details, see [Shutting down and restarting services](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=resources-shutting-down-restarting-services){: external}.

Action skills
:   The classic {{site.data.keyword.assistant_classic_short}} experience now supports action skills.


## 13 October 2022
{: #assistant-data-oct132022}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} Version 4.5.3 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.5.3 is compatible with {{site.data.keyword.icp4dfull}} Version 4.5. See the [support matrix](/docs/watson-assistant?topic=watson-assistant-install#install-support-matrix) for more details. This release of {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} includes various fixes and features.

Support for `autoScaleConfig`
:   Support for automatically scaling resources using the Red Hat OpenShift Horizontal Pod Autoscaler (HPA). See [Automatically scaling resources for services](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.5.x?topic=services-automatically-scaling).

## 3 August 2022
{: #assistant-data-aug032022}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} Version 4.5.1 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.5.1 is compatible with {{site.data.keyword.icp4dfull}} Version 4.5. See the [support matrix](/docs/watson-assistant?topic=watson-assistant-install#install-support-matrix) for more details. This release of {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} includes various fixes and features.

New deployment sizes
:   Two new deployment sizes are now available. The two new sizes are `Starter` and `Production`. The `Starter` size is equivalent to the `small` deployment size, and the `Production` size is equivalent to the `medium` deployment size.

## 29 June 2022
{: #assistant-data-jun292022}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} Version 4.5.0 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.5.0 is compatible with {{site.data.keyword.icp4dfull}} Version 4.5. See the [support matrix](/docs/watson-assistant?topic=watson-assistant-install#install-support-matrix) for more details. This release of {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} includes various fixes and features.

Red Hat OpenShift Container Platform support
:   You can deploy {{site.data.keyword.icp4dfull}} Version 4.5 on the following versions of Red Hat OpenShift Container Platform:
    - Version 4.6.29 or later fixes
    - Version 4.8.0 or later fixes
    - Version 4.10.0 or later fixes

New {{site.data.keyword.icp4dfull}} CLI commands and reference
:   Starting in {{site.data.keyword.icp4dfull}} Version 4.5, the `cpd-cli` includes new commands and a new command reference. For more information, see the [cpd-cli command reference](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.5.x?topic=interface-cpd-cli-command-reference){: external}.

Microsoft Edge browser support
:   Beginning in Version 4.5, Microsoft Edge is fully supported for use with {{site.data.keyword.icp4dfull}}. 

Language support improvements
:   Entity recognition and intent classification for Japanese and Korean languages changed to improve the reliability of {{site.data.keyword.assistant_classic_short}}. You might see minor differences in how {{site.data.keyword.assistant_classic_short}} handles entity recognition and intent classification.

   Any visible changes are most likely to be seen in dictionary-based or pattern-based entity matching. For more information about defining entities, see [Adding entities](/docs/watson-assistant?topic=watson-assistant-entities). As a suggested practice, you can test your dialog skill with your current test framework to determine whether your workspace is impacted before you update your production workspace.

   If entity values or synonyms that previously matched no longer match, you can update the entity and add a synonym with white space between the tokens, for example:
   - Japanese: Add “見 た” as a synonym for “見た”
   - Korean: Add “잘 자 요” as a synonym for “잘자요”

Assistant preview link can be disabled
:   Assistant preview now includes a toggle to disable the preview link. This allows you to stop access to the preview link if necessary.

## 27 April 2022
{: #assistant-data-apr272022}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} 4.0.8 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.0.8 is compatible with {{site.data.keyword.icp4dfull}} 4.0 on Red Hat OpenShift 4.8. This release of {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} includes various fixes and features.

Closed entity matching with accent-normalized values in French
:   Closed entities exact matches in French are completed using accent-normalized values or synonyms. For example, if you define a closed entity with a value or synonym with accent marks (for example, garçon or déjà), then variants without accent marks are also recognized (garcon or deja). Likewise, if a closed entity value or synonym is defined without accent marks, then user inputs with accent marks are also recognized. For more information about defining entities, see [Defining information to look for in customer input](/docs/watson-assistant?topic=watson-assistant-entities).

Pattern entities do not prevent spelling autocorrection
:   Pattern entities that match all characters and words that are usually used to count input words do not prevent spelling autocorrection. For example, if a customer defines the `^..{0,19}$` pattern entity that matches the first 20 characters of an input, then the entity match does not affect spelling autocorrection. In this example, an input of `cancl transaction` is autocorrected to `cancel transaction`.

   This change applies to the following languages: English and French. For more information, see [Autocorrecting user input](/docs/watson-assistant?topic=watson-assistant-autocorrection).

Fuzzy matching updates
:   Previously, an update was made so that interactions between the stemming and misspelling fuzzy matching features were not allowed. This change applied to the following languages: English, French, German, and Czech. This was updated so that this change applies only to the English language. For more information, see [How fuzzy matching works](/docs/watson-assistant?topic=watson-assistant-entities#entities-fuzzy-matching).

Improved irrelevance detection for Dutch
:   Irrelevance detection for Dutch disregards any punctuation in an input sentence. For example, you can now expect the same confidence score for the following two inputs: `ik ben een kleine krijger?` and `ik ben een kleine krijger`. In this example, the question mark (`?`) doesn't affect the confidence score.

Improved enhanced intent detection
:   The exact match in enhanced intent detection now better handles small differences between training examples and runtime utterances when the differences do not change the meaning of a sentence.

   For example, suppose in your training examples, `covid-19` is in the `#covid` intent and `@doctortype_facilitytype around Palm Beach` is in the `#find_provide_master` intent. In this example, the `@doctortype_facilitytype` direct entity reference contains entity values, including `hospital`. At run time, `covid19` is predicted as 100% confident for the `#covid` intent, and `hospital around palm beach` is predicted as 100% confident for the `#find_provide_master` intent.

   This update applies to the following languages: English, French, Spanish, Italian, and the universal language model. For more information, see [Accessing intents](/docs/watson-assistant?topic=watson-assistant-expression-language#expression-language-intent).

## 30 March 2022
{: #assistant-data-mar302022}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} 4.0.7 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.0.7 is compatible with {{site.data.keyword.icp4dfull}} 4.0 on Red Hat OpenShift 4.8. This release of {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} includes various fixes and features.

Enhanced irrelevance detection update
:   We revised the enhanced irrelevance detection classification algorithm. Now, enhanced irrelevant detection uses any provided counterexamples in training. This change does not affect workspaces without counterexamples. This update applies to the following languages: English, French, Spanish, Italian, and the universal language model. For more information, see [Defining what's irrelevant](/docs/watson-assistant?topic=watson-assistant-irrelevance-detection).

Fuzzy matching updates
:   Interactions between the stemming and misspelling fuzzy matching features are not allowed. Improve fuzzy matching behavior by limiting the interactions between different fuzzy matching features. This change applies to the following languages: English, French, German, and Czech. For more information, see [How fuzzy matching works](/docs/watson-assistant?topic=watson-assistant-entities#entities-fuzzy-matching).

## 23 February 2022
{: #assistant-data-feb232022}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} 4.0.6 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.0.6 is compatible with {{site.data.keyword.icp4dfull}} 4.0 on Red Hat OpenShift 4.8. This release of {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} includes various fixes and features.

New API version
:   The current API version is now `2021-11-27`. This version introduces the following changes:

    - The `output.text` object is no longer returned in `message` responses. All responses, including text responses, are returned only in the `output.generic` array.

Configure webhook timeout
:   From the **Pre-message webhook** and **Post-message webhook** configuration pages, you can configure the webhook timeout length from a minimum of 1 second to a maximum of 30 seconds. For more information, see [Webhook overview](/docs/watson-assistant?topic=watson-assistant-webhook-overview).

Rich response types
:   Your assistant can now send responses that include elements such as audio, video, or embedded `iframe` content. For more information, see [Rich responses](/docs/watson-assistant?topic=watson-assistant-dialog-overview#dialog-overview-multimedia).

Analytics overview change
:   To improve reliability, the **Values** column has been removed from **Top entities** on the **Analytics Overview** page. **Top Entities** continues to provide counts of entity types. For more information, see [Top intents and top entities](/docs/watson-assistant?topic=watson-assistant-logs-overview#logs-overview-tops).

Dialog skill **Try it out** improvements
:   For dialog skills, the **Try it out** pane now uses the [React](https://reactjs.org/){: external} UI framework similar to the rest of the {{site.data.keyword.assistant_classic_short}} user interface. You shouldn't see any change in behavior or functionality. As a part of the update, dialog skill error handling has been improved within the **Try it out** pane.

Disambiguation feature updates
:   The dialog skill disambiguation feature now includes improved features:

    - **Increased control**: The frequency and depth of disambiguation can now be controlled by using the **sensitivity** parameter in the [workspace API](https://{DomainName}/apidocs/assistant-v1#updateworkspace){: external}. There are 5 levels of sensitivity:
        - `high`
        - `medium_high`
        - `medium`
        - `medium_low`
        - `low`

        The default (`auto`) is `medium_high` if this option is not set.

    - **More predictable**: The new disambiguation feature is more stable and predictable. The choices shown may sometimes vary slightly to enable learning and analytics, but the order and depth of disambiguation is largely stable.

    These new features may affect various metrics, such as disambiguation rate and click rates, as well as influence conversation-level key performance indicators such as containment.

    If the new disambiguation algorithm works differently than expected for your assistant, you can adjust it using the sensitivity parameter in the update workspace API. For more information, see [Update workspace](https://{DomainName}/apidocs/assistant-v1#updateworkspace){: external}.

## 26 January 2022
{: #assistant-data-jan262022}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} 4.0.5 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.0.5 is compatible with {{site.data.keyword.icp4dfull}} 4.0 on Red Hat OpenShift 4.8. This release of {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} includes various fixes. {{site.dassistant_classic_shortrsationshort}} for {{site.data.keyword.icp4dfull}} 4.0.5 is compatible with FIPS-enabled clusters.

## 20 December 2021
{: #assistant-data-dec202021}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} 4.0.4 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.0.4 is compatible with {{site.data.keyword.icp4dfull}} 4.0 on Red Hat OpenShift 4.8. This release of {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} includes critical security fixes. {{site.dassistant_classic_shortrsationshort}} for {{site.data.keyword.icp4dfull}} 4.0.4 is not compatible with FIPS-enabled clusters. The upcoming release of {{assistant_classic_short.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.0.5 will be compatible with FIPS-enabled clusters.

## 4 October 2021
{: #assistant-data-oct042021}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} 4.0.2 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.0.2 is compatible with {{site.data.keyword.icp4dfull}} 4.0 on Red Hat OpenShift 4.8.

Integration with the {{site.data.keyword.icp4dfull}} auditing service
:   {{site.data.keyword.assistant_classic_short}} integrates with the {{site.data.keyword.icp4dfull}} auditing service feature, providing standard auditing records for important lifecycle and security events. The service generates audit records for events such as intent edits, entity creation, dialog node deletion, and more.

## 29 July 2021
{: #assistant-data-jul292021}
{: release-note}

{{site.data.keyword.assistant_classic_full}} Cartridge for {{site.data.keyword.icp4dfull}} 4.0.0 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 4.0.0 is compatible with {{site.data.keyword.icp4dfull}} 4.0 on Red Hat OpenShift 4.6. See the [support matrix](/docs/watson-assistant?topic=watson-assistant-install#install-support-matrix) for more details.

Universal language
:   You now can build an assistant in any language you want to support. If a dedicated language model is not available for your target language, create a skill that uses the universal language model. The universal model applies a set of shared linguistic characteristics and rules from multiple languages as a starting point. It then learns from training data written in the target language that you add to it.

[Premessage](/docs/watson-assistant?topic=watson-assistant-webhook-pre), [postmessage](/docs/watson-assistant?topic=watson-assistant-webhook-post), and [log webhooks](/docs/watson-assistant?topic=watson-assistant-webhook-log)
:   A set of new webhooks are available for each assistant. You can use the webhooks to perform preprocessing tasks on incoming messages and postprocessing tasks on the corresponding responses. You can use the new log webhook feature to log each message with an external service.

Features not included
:   This release does not include the following features, which are available for cloud instances at the time of this release:
   - Service desk support is not included.
   - The phone integration is not supported.
   - The actions skill is not available.
   - The intent recommendations feature and the enhanced intent detection model are not supported.

## 19 March 2021
{: #assistant-data-mar192021}
{: release-note}

{{site.data.keyword.assistant_classic_full}} 1.5.0 patch 1 is available
:   For installations on {{site.data.keyword.icp4dfull}} 3.5, patch 1 includes configuration changes for FIPS compatibility and other fixes. See [Available patches for {{site.data.keyword.assistant_classic_full}} for {{site.data.keyword.icp4dfull}}](https://www.ibm.com/support/pages/node/6240164){: external}

## 9 December 2020
{: #assistant-data-dec092020}
{: release-note}

{{site.data.keyword.assistant_classic_full}} for {{site.data.keyword.icp4dfull}} 1.5.0 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 1.5.0 is compatible with {{site.data.keyword.icp4dfull}} 3.5 and {{site.data.keyword.icp4dfull}} 3.0.1 deployments on Red Hat OpenShift 4.6, 4.5, or 3.11. See the [support matrix](/docs/watson-assistant?topic=watson-assistant-install#install-support-matrix) for more details.

{{site.data.keyword.assistant_classic_full}} for {{site.data.keyword.icp4dfull}} 1.5.0 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 1.5.0 is compatible with {{site.data.keyword.icp4dfull}} 3.5 and {{site.data.keyword.icp4dfull}} 3.0.1 deployments on Red Hat OpenShift 4.5 or 3.11.

Access conversation logs and metrics
:   An **Analytics** page is now available. From this page, you can see conversation logs and metrics that give you insights, such as what topics your customers are asking about and how often the assistant succeeds in addressing customer requests. For more information, see [Metrics overview](/docs/watson-assistant?topic=watson-assistant-logs-overview).

Introducing the *Web chat* integration
:   Deploy your assistant in minutes. Create a web chat integration to embed your assistant into a page on your website as a chat widget. Web chat version 3.3.0 is included in this release.

Introducing the *Preview link* integration
:   Deploy your assistant to an IBM-branded web site for testing purposes. When you add both a dialog skill and search skill to your assistant, you can test the overall interaction between the two skills by using the preview link integration. 

Improved system entities
:   A new `interpretation` property is returned for the system entities in all languages. The new property provides additional information about the recognized entity which can be leveraged by your dialog. For more information, see [System entities](/docs/watson-assistant?topic=watson-assistant-system-entities).

Irrelevance detection
:   The irrelevance detection classification algorithm was updated to make it even smarter out of the box. Now, even before you begin to teach the system about irrelevant requests, it is able to recognize user input that your skill is not designed to address. The new algorithm is enabled by default for any English-language skills that you import or create. For more information, see [Irrelevance detection](/docs/watson-assistant?topic=watson-assistant-irrelevance-detection).

Search was added to the Dialog, Intents, and Entities pages
:   You can now search within the product. For example, if you want to find any dialog nodes that condition on an intent, you can open the Dialog page and search on the intent name.

v2 Logs API is available
:   Use the v2 API logs method to list log events for an assistant. For more information, see the [API reference documentation](https://{DomainName}/apidocs/assistant-data-v2#listlogs).

Features not included
:   This release does not include the following features, which are available for cloud instances at the time of this release:
   - While the web chat integration is now available, service desk support is not included.
   - The Facebook, Slack, Intercom, Phone, SMS with Twilio, and WhatsApp integrations are not supported.
   - The actions skill is not available.
   - You cannot enable FAQ extraction when you add a web crawl data collection to the search skill.
   - You cannot use the Activity Tracker service to track user actions for auditing purposes.
   - You cannot manage user access at the individual skill and assistant level. You can control only who can access the entire service instance, which includes all of its skills and assistants. For more information about granting access to services in {{site.data.keyword.icp4dfull_notm}}, see [3.5 Managing users](https://www.ibm.com/support/knowledgecenter/SSQNUZ_3.5.0/cpd/admin/users.html).

## 19 June 2020
{: #assistant-data-jun192020}
{: release-note}

{{site.data.keyword.assistant_classic_full}} for {{site.data.keyword.icp4dfull}} 1.4.2 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} 1.4.2 is compatible with {{site.data.keyword.icp4dfull}} 3.0.1 on OpenShift Red Hat 3.11 or 4.5 and {{site.data.keyword.icp4dfull}} 2.5 deployments on OpenShift Red Hat 3.11. The 1.4.2 release is certified on Red Hat OpenShift 4.5.

Autocorrection support was added
:   Autocorrection helps your assistant understand what your customers want. It corrects misspellings in the input that customers submit before the input is evaluated. With more precise input, your assistant can more easily recognize entity mentions and understand the customer's intent. This feature is not available in all languages. See [Autocorrecting user input](/docs/watson-assistant?topic=watson-assistant-autocorrection) for more details.

French-language dialog skill improvements
:   Added full support for fuzzy matching and contextual entities and added beta support for autocorrection.

The Covid-19 content catalog is available in Brazilian Portuguese, English, French, and Spanish
:   The content catalog defines a group of intents that recognize the common types of questions people ask about the novel coronavirus. You can use the catalog to jump-start development of chatbots that can answer questions about the virus and help to minimize the anxiety and misinformation associated with it. For more information about how to add a content catalog to your skill, see [Using content catalogs](/docs/watson-assistant?topic=watson-assistant-catalog).

Backup automation
:   Support was added for doing data backups on a schedule.

Stateless v2 message API
:   The v2 runtime API now supports a new stateless `message` method. For more information, see the [API Reference](https://{DomainName}/assistant/assistant-data-v2#message-stateless)}.

Architecture improvements
:   The Skill-conversation microservice was removed. The microservice used to convert v2 API calls to v1 format and the other way around. The conversion is now done within the Store microservice. Reimplementing this function in the Store increased the overall speed with which v2 API requests are processed. The Spellchecker and CLU Embedding microservices were added. The word embeddings that are used by the language understanding pipeline (training, TAS, ED-MM) now are stored in the CLU Embedding microservice instead of MongoDB.

Slot prompt JSON editor
:   You can now use the context or JSON editors for the slot response field where you define the question that your assistant asks to get information it needs from the customer. For more information about slots, see [Gathering information with slots](/docs/watson-assistant?topic=watson-assistant-dialog-slots).

Bug fixes
:   Multiple bug fixes were made.

Features not included
:   This release does not include the following features, which are available for cloud instances at the time of this release:
   - There are no metrics or analytics capabilities. Therefore, the *Analytics* page is not included in the product user interface.
   - There are no deployment connectors or built-in integrations available. You must build a custom client application that can host the assistant. As a result, the *Integrations* page is not included in the product user interface.
   - The @sys-person and @sys-location system entities are not supported and the new version of the numeric system entities is not available.
   - There is no search function in the pages of the product.
   - You cannot use the Activity Tracker service to track user actions.
   - You cannot manage user access at the individual skill and assistant level. You can control only who can access the entire service instance, which includes all of its skills and assistants. For more information about granting access to services in {{site.data.keyword.icp4dfull_notm}}, see [3.0.1 Managing users](https://www.ibm.com/support/knowledgecenter/SSQNUZ_3.0.1/cpd/admin/users.html)}.

## 14 April 2020
{: #assistant-data-apr142020}
{: release-note}

IBM Cloud Private End Of Support
:   Effective 30 September 2020, IBM will withdraw support for {{site.data.keyword.assistant_classic_full}} on IBM Cloud Private. For more information, see the [announcement](https://www-01.ibm.com/common/ssi/cgi-bin/ssialias?infotype=an&subtype=ca&appname=gpateam&supplier=897&letternum=ENUS920-075).

## 28 February 2020
{: #assistant-data-feb282020}
{: release-note}

{{site.data.keyword.assistant_classic_full}} for {{site.data.keyword.icp4dfull}} version 1.4.1 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} version 1.4.1 is compatible with {{site.data.keyword.icp4dfull}} version 2.5.

New backup and restore
:   A new backup and restore script is available.

Webhooks now generally available
:   The Webhooks feature is now generally available. See [Making a programmatic call from dialog](/docs/watson-assistant?topic=watson-assistant-dialog-webhooks).

Bug fixes
:   Multiple bug fixes were made.

Features not included
:   This release does not include the following features, which are available for cloud instances at the time of this release:
   - There are no metrics or analytics capabilities. Therefore, the *Analytics* page is not included in the product user interface.
   - There are no deployment connectors or built-in integrations available. You must build a custom client application that can host the assistant. As a result, the *Integrations* page is not included in the product user interface.
   - The @sys-person and @sys-location system entities are not supported and the updated numeric system entities are not available.
   - There is no search function in the product.
   - You cannot use the Activity Tracker service to track user actions.
   - Autocorrection, intent recommendations, and the new irrelevance detection model are not supported.
   - The product tour that is available to some first-time users of the cloud-based product is not available.

## 27 November 2019
{: #assistant-data-nov272019}
{: release-note}

{{site.data.keyword.assistant_classic_full}} for {{site.data.keyword.icp4dfull}} version 1.4 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} version 1.4 is compatible with {{site.data.keyword.icp4dfull}} version 2.5.

Czech language not automatically enabled
:   The Czech language is not enabled automatically anymore.

Assistants and Skills navigation menu update
:   The main menu options of **Assistants** and **Skills** have moved from being displayed at the top of the page to being shown as icons in a new navigation pane.

Skills secondary navigation menu update
:   The tabbed pages for the tools that you use to develop a dialog skill were moved to a secondary navigation bar that is displayed when you open the skill.

Rich response types support
:   Rich response types are now supported in a dialog node with slots. You can display a list of options for a user to choose from as the prompt for a slot, for example. For more information, see [Gathering information with slots](/docs/watson-assistant?topic=watson-assistant-dialog-slots).

Improved Entities, Dialog, and Intents page responsiveness
:   The Entities, Dialog, and Intents pages were updated to use a new JavaScript library that increases the page responsiveness. As a result, the look of some graphical user interface elements, such as buttons, changed slightly, but the function did not.

Creating contextual entities is easier
:   The process you use to annotate entity mentions from intent user examples was improved. You can now put the intent page into annotation mode to more easily select and label mentions. For more information, see [Adding contextual entities](/docs/watson-assistant?topic=watson-assistant-entities#entities-create-annotation-based).

Webhook callouts are available
:   Add webhooks to dialog nodes to make programmatic calls to an external application as part of the conversational flow. This capability is being introduced as a beta feature. For more details, see [Making a programmatic call from dialog](/docs/watson-assistant?topic=watson-assistant-dialog-webhooks).

Testing improvement
:   You can now see the top three intents that were recognized in a test user input from the **Try it out** pane.

## 3 September 2019
{: #assistant-data-sep032019}
{: release-note}

{{site.data.keyword.assistant_classic_full}} for {{site.data.keyword.icp4dfull}} version 1.3 is available
:   {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}} version 1.3 is compatible with {{site.data.keyword.icp4dfull}} versions 2.1.0.1 and 2.1.0.2. There is now added support for installing {{site.data.keyword.icp4dfull_notm}} with Red Hat OpenShift.

Federal Information Security Management Act support
:   Federal Information Security Management Act (FISMA) support is available for {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull_notm}} for this version (V1.3). FISMA support is also available to those who purchased V1.2 (28 June 2019) and upgraded to V1.3. {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull_notm}} is FISMA High Ready.

Provision more instances in a single deployment
:   You can now provision up to 30 instances of {{site.data.keyword.assistant_classic_short}} in a single deployment.

Search skill now generally available
:   The search skill is now generally available.

Features not included
:   This release does not include the following features, which are currently available for cloud instances:
   - Autocorrection, intent recommendations, and webhooks are not supported.
   - The product tour that is available to some first time users of the cloud-based product is not available.
   - The new JavaScript library that is being used in cloud instances to increase the page responsiveness is not in use.

## 28 June 2019
{: #assistant-data-jun282019}
{: release-note}

{{site.data.keyword.assistant_classic_full}} for {{site.data.keyword.icp4dfull}} version 1.2 is available
:   The {{site.data.keyword.assistant_classic_short}} tool now works with {{site.data.keyword.icp4dfull_notm}} 2.1. It does not work with stand-alone {{site.data.keyword.icpfull_notm}}. The following changes were made in this release:

Assistants are now available
:   An assistant can manage user sessions on your behalf.

Search skill is a new beta feature
:   You can create a search skill to trigger a search in an external data source that you configure in Watson Discovery. 

Introducing dialog skills
:   Instead of creating a workspace as the container for your training data and dialog, you create a dialog skill. 

Intent conflict resolution is available
:   Prevent your assistant from answering the wrong question by keeping your intents distinct from one another. Intent conflict resolution is now available. It can find intents with overlapping user examples, and gives you a graphical user interface in which to fix them. Nondistinct intents can result in misclassifications of user input. 

## 21 February 2019
{: #assistant-data-feb212019}
{: release-note}

{{site.data.keyword.assistant_classic_full}} for {{site.data.keyword.icpfull}} version 1.1 is available
:   The {{site.data.keyword.assistant_classic_short}} tool now works with {{site.data.keyword.icpfull_notm}} 3.1.0. It does not work with {{site.data.keyword.icpfull_notm}} 2.1.0.3. {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icpfull_notm}} version 1.1 is compatible with {{site.data.keyword.icp4dfull}} version 1.2.

Decrease in the number of required Virtual Private CPUs
:   The number of required Virtual Private CPUs has decreased from its previous number (of 60 VPCs).

Improvements to language support
:   Language support was improved, which means you do not need as many additional resources when you add support for more languages.

## 23 November 2018
{: #assistant-data-nov232018}
{: release-note}

{{site.data.keyword.assistant_classic_full}} for {{site.data.keyword.icpfull}} version 1.0.1 runs on IBM Cloud Private 2.1.0.3
:   A revised Helm chart (version 1.0.1) was published, which improves the Helm chart and packaging.

New configuration settings
:   New configuration settings were added that allow you to specify domain names and IP addresses for the coordinator and proxy nodes of the {{site.data.keyword.icpfull}} cluster. A new checkbox is visible for enabling recommendations; however, do not select it as the feature is not fully supported yet.

Development deployment required resources
:   The resources required for a development deployment changed for Minio from one 20 GB replica to four 5 GB replicas. This change means you need to create 13 persistent volumes instead of 10 to support the deployment.

## 5 October 2018
{: #assistant-data-oct052018}
{: release-note}

{{site.data.keyword.assistant_classic_full}} for {{site.data.keyword.icpfull}} version 1.0.0.1 runs on IBM Cloud Private 2.1.0.3
:   A revised Helm chart (version 1.0.0.1) was published, which improves the installation process.

## 26 September 2018
{: #assistant-data-sep262018}
{: release-note}

{{site.data.keyword.assistant_classic_full}} for {{site.data.keyword.icpfull}} 1 is available
:   {{site.data.keyword.assistant_classic_full}} for {{site.data.keyword.icpfull}} version 1 runs on IBM Cloud Private 2.1.0.3.

Introducing the **Build** tab
:   The {{site.data.keyword.assistant_classic_full}} tool includes a **Build** tab that offers pre-built intents you can add to your workspace from a content catalog, the ability to define your own intents and entities, and has a graphical user interface you can use to build a dialog. The following key features are also available:

   - Dialog: Digression and disambiguation support, nodes with slots, rich responses (including *Connect to human agent*)
   - Entities: Contextual entities, system entities for currency, date, number, percentage, and time.
   - Intents: Content catalog

Features not included
:   These features are not available from {{site.data.keyword.icpfull}}, but are available in the public IBM Cloud instance at the time of this release:
   - There are no metrics or analytics capabilities. Therefore, the *Improve* tab is not included in the tool.
   - There are no deployment connectors or built-in integrations available. You must build a custom client application that can host the assistant. As a result, the *Deploy* tab is not included in the tool.
   - You cannot search within the tool.
   - The @sys-person and @sys-location system entities are not supported.
   - You cannot make programmatic calls to Cloud Functions actions from the dialog.
   - No entity synonym recommendations are available.
   - No intent conflict detection is available.
