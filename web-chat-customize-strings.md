---

copyright:
  years: 2019, 2022
lastupdated: "2022-06-06"

subcollection: watson-assistant

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:deprecated: .deprecated}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:preview: .preview}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:video: .video}

{{site.data.content.classiclink}}

# Customizing strings
{: #web-chat-customize-strings}

You can edit the hardcoded strings that are displayed in the web chat to customize them for branding or style. Whether your web chat responds in English or another language, you can customize the wording that is used. For example, you might want to replace the phrase that says, `The live agent is typing` with the phrase, `A customer support agent is typing`.

The language files contain [ICU Message Format](http://userguide.icu-project.org/formatparse/messages){: external} JSON representations of all of the languages that are supported by the web chat. You can edit all or a subset of the phrases in a JSON file, and then configure the web chat to use your version by specifying the `instance.updateLanguagePack()` method.

For more information, see [Languages](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#languages){: external}.

