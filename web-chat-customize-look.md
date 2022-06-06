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

## Customizing the look of the web chat
{: #web-chat-customize-look}

You can make simple changes to the color of things like the text font and web chat header from the *Style* tab of the web chat configuration page. To make more extensive style changes, you can set the CSS style color theme to a different theme or specify your own theme.

- You can choose to use a different base Carbon Design theme. The supported base themes are color themes that are defined by [IBM Carbon Design](https://v10.carbondesignsystem.com/guidelines/color/usage/){: external}. For more information, see [Theming](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#theming){: external}.
- Alternatively, you can set individual variables within the theme to customize specific UI elements. For example, the text that is displayed in the chat window uses the fonts `IBMPlexSans, Arial, Helvetica, sans-serif`. If you want to use a different font, you can specify it by using the `instance.updateCSSVariables()` method.
- Apply style settings to user-defined response types. If you enable the web chat to return custom response types, be sure to apply existing or custom CSS classes to them. For more information, see [Custom content](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-render){: external}.
- Change the style of the home screen that can be displayed when the web chat is opened. For more information about the home screen, see [Adding a home screen](/docs/watson-assistant?topic=watson-assistant-deploy-web-chat#deploy-web-chat-home-screen). For more information about how to customize it, see [HTML content](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-render#html){: external}

The web chat is embedded directly on your page, not inside an iframe. Therefore, the cascading style sheet (CSS) rules for your website can sometimes override the web chat CSS rules. The web chat applies aggressive CSS resets, but the resets can be affected if your website uses the `!important` property in elements where style is defined.
{: note}

