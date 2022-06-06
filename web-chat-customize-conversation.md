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

# Customizing the conversation
{: #web-chat-customize-conversation}

The core of the conversation is defined in your actions. If you use more than one integration type, focus on defining an engaging conversation in the underlying actions flow. The same actions setup is used for all integrations. To customize the conversation for the web chat only, you can take the following actions:

- Update the text of a message before it is sent or after it is received, such as to hide personally-identifiable information.
- Pass contextual information, such as the customer's name, from the web chat to your actions. For examples of how to complete common tasks, see [Passing values](#web-chat-config-context).
- Change the language that is used by the web chat. For more information, see [Supporting global audiences](#web-chat-customize-global).
- Render your own custom response types inside the web chat widget, including responses that incorporate code from your website at run time. For a tutorial that shows you how, see [Creating a custom response](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-user-defined-response){: external}.
- Use React portals to render your custom response type as part of your application. For a tutorial that shows you how, see [Custom responses with React](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-react-portals){: external}.

