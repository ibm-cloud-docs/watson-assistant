---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-29"

subcollection: watson-assistant

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}


# Release notes for {{site.data.keyword.conversationshort}} for {{site.data.keyword.IBM_notm}} Software Hub
{: #release-notes-hub}

[{{site.data.keyword.IBM_notm}} Software Hub]{: tag-teal}

Use these release notes to learn about the latest updates to {{site.data.keyword.conversationshort}} for {{site.data.keyword.IBM_notm}} Software Hub.
{: shortdesc}

## Web chat versions
{: #release-notes-web-chat-hub}

When you install {{site.data.keyword.conversationshort}} for {{site.data.keyword.IBM_notm}} Software Hub, the latest available version of the web chat integration is included. See the following table for details about the latest available web chat version for each {{site.data.keyword.conversationshort}} for IBM Software Hub release. If your web chat version is not locked, then the web chat integration is upgraded to the latest available version when you upgrade {{site.data.keyword.conversationshort}} for IBM Software Hub.

The following table shows the latest version of the web chat integration that is included with each release of {{site.data.keyword.conversationshort}} for {{site.data.keyword.IBM_notm}} Software Hub. {{site.data.keyword.IBM_notm}} Software Hub supports web chat versions 8.3.2 or later. To customize and change version numbers, see [Controlling the web chat version](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-versions).



| {{site.data.keyword.conversationshort}} for {{site.data.keyword.IBM_notm}} Software Hub version | Latest web chat version available |
|----------------|----------------|
| 5.1.2 | [8.6.0](/docs/watson-assistant?topic=watson-assistant-release-notes-chat#8.6.0) |
| 5.1.1 | [8.5.1](/docs/watson-assistant?topic=watson-assistant-release-notes-chat#8.5.1) |
| 5.1.0 | [8.3.2](/docs/watson-assistant?topic=watson-assistant-release-notes-chat#8.3.2) |
{: caption="Web chat versions in {{site.data.keyword.conversationshort}} for {{site.data.keyword.IBM_notm}}  Software Hub" caption-side="top"}





## 5.1.2 release, 26 March 2025
{: #assistant-hub-mar262025}
{: release-note}

**New features**

Use LLMs for your watsonx Assistant
: Large language models (LLMs) are now available for you to configure to improve the capabilities of your assistants. From the Base LLM section of the new Generative AI page, you can enable LLM features for the existing actions in your assistants to improve the conversation capabilities of your assistants. You can choose the foundation model that best interacts with your assistants for conversational search. For more information, see [Supported foundation models for GPU features](https://www.ibm.com/docs/en/software-hub/5.1.x?topic=administering-configuring-gpu-features-models#assistant-config-GPU-features__supported-llm-models__title__1){: external}.

**Updates**

Evaluate testing message limits
You no longer have a limit on the number of tests in a test run to evaluate and analyze your {{site.data.keyword.conversationshort}}'s performance but each test can include a maximum of 250 messages. For more information, see [Testing limits for the set of data](/docs/watson-assistant?topic=watson-assistant-evaluating-the-assistant).


## 5.1.1 release, 27 February 2025
{: #assistant-hub-feb272025}
{: release-note}

**New features**

Hide or display the skill output
: You can now choose to hide or display the skill output that is stored as an assistant variable. For more information, see [Passing values to a subaction](/docs/watson-assistant?topic=watson-assistant-step-what-next#step-what-next-pass-value-to-subaction).

Integrate your {{site.data.keyword.conversationshort}} with Slack
: You can integrate your {{site.data.keyword.conversationshort}} with Slack. Then you can configure the assistant to support certain events so that your assistant can respond to questions that are asked in Slack direct messages or in Slack channels where the assistant is directly mentioned. For more information, see [Integrating with Slack](/docs/watson-assistant?topic=watson-assistant-deploy-slack).

Evaluate assistant's performance
: You can now evaluate the performance of your {{site.data.keyword.conversationshort}} by uploading a comprehensive, relevant collection of utterances and sending the utterances to your assistant in a test run. . For more information, see [Evaluating the assistant](/docs/watson-assistant?topic=watson-assistant-evaluating-the-assistant).

Post-process the conversational search responses
: You can now save your conversational search responses in action variables of your watsonx Assistant for post-processing. For more information, see [Search for the answer](/docs/watson-assistant?topic=watson-assistant-step-what-next#search-for-answer).

**Updates**

Updated conversational search user query
: To improve integration with Elasticsearch, the question mark (?) is no longer automatically added to the user query in conversational search. In rare cases, this change might alter the conversational search responses.

Limit on number of entries for translation download
: You can enable language data files to be downloaded for translation, only if the total number of entries in your assistant is 400000 or less. For more information, see [Using multilingual downloads for translation](/docs/watson-assistant?topic=watson-assistant-admin-language-support#admin-language-support-multilingual).


Updated LLM models for Conversational search
: As granite-13b-chat-v2 model is deprecated, you can now use the updated foundation model granite-3-8b-instruct for Conversational search. For more information, see [Mirroring images directly to the private container registry](https://www.ibm.com/docs/en/software-hub/5.1.x?topic=registry-mirroring-images-directly-private-container){: external}.

## 5.1.0 release, 11 December 2024
{: #assistant-hub-dec112024}

For the list of {{site.data.keyword.conversationshort}} known issues, see [Limitations and Known issues in {{site.data.keyword.conversationshort}}](https://www.ibm.com/docs/en/software-hub/5.1.x?topic=issues-watsonx-assistant){: external}.

For a list of new features and fixes, see [What's new and changed in {{site.data.keyword.conversationshort}}](https://www.ibm.com/docs/en/software-hub/5.1.x?topic=new-watsonx-assistant){: external}.
