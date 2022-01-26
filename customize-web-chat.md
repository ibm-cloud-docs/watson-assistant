---

copyright:
  years: 2019, 2021
lastupdated: "2021-09-23"

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

# Customizing the web chat
{: #customize-web-chat}

The web chat integration provides a ready-to-use JavaScript script you can use to make your assistant available on your website with a minimum of HTML coding. You can optionally customize and extend this script to customize how the web chat widget looks and behaves.
{: shortdesc}

For more information about how to deploy the web chat, see [Adding the web chat to your website](/docs/watson-assistant?topic=watson-assistant-deploy-web-chat).

For detailed information about how to customize and extend the web chat, see the web chat [developer documentation](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=){: external}.

## Global audience support
{: #customize-web-chat-global}

You can build an assistant that understands customer messages in any of the languages that are supported by the service. <!-- For more information, see [Supported languages](/docs/watson-assistant?topic=watson-assistant-language-support).--> The responses from your assistant are defined by you and can be written in any language you want.

However, some of the phrases that are displayed in the web chat widget are part of the web chat itself and do not come from the assistant. By default, these hardcoded phrases are specified in English, but you can apply a different language by adding lines to the embedded web chat script.

The hardcoded phrases used by the web chat widget are specified in *language pack* files. The web chat provides language packs that contain translations of each English-language phrase that is used by the web chat. You can instruct the web chat to use one of these other languages files by using the `instance.updateLanguagePack()` method.

Likewise, the web chat applies an American English locale to content that is added by the web chat unless you specify something else. The locale setting affects how values such as dates and times are formatted. 

To configure the web chat for customers outside the US, follow these steps:

1.  To apply the appropriate syntax to dates and times *and* to use a translation of the English-language phrases, set the locale. Use the `instance.updateLocale()` method.

    For example, if you apply the Spanish locale (`es`), the web chat uses Spanish-language phrases that are listed in the `es.json` file, and uses the `DD-MM-YYYY` format for dates instead of `MM-DD-YYYY`. 
    
    The locale you specify for the web chat does not impact the syntax of dates and times that are returned by the underlying skill.
    {: note}

1.  To change only the language of the hardcoded English phrases, use the `instance.updateLanguagePack()` method.

    For more information, see [Instance methods](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#languages){: external}.

1.  To change the text direction of the page from right to left, use the `direction` method. For more information, see [Configuration](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#configurationobject){: external}.

### Customizing phrases
{: #customize-web-chat-phrasing}

You can edit the hardcoded phrases that are displayed in the web chat to customize them for branding or style. Whether your web chat responds in English or another language, you can customize the wording that is used. For example, you might want to replace the phrase that says, `The live agent is typing` with the phrase, `A customer support agent is typing`.

The language files contain [ICU Message Format](http://userguide.icu-project.org/formatparse/messages){: external} JSON representations of all of the languages that are supported by the web chat. You can edit all or a subset of the phrases in a JSON file, and then configure the web chat to use your version by specifying the `instance.updateLanguagePack()` method.

For more information, see [Languages](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#languages){: external}.

## Versioning
{: #customize-web-chat-versions}

The web chat JavaScript code follows semantic versioning practices. Starting with web chat version 2.0.0, you can set the version of the web chat that you want to use as a configuration option.

If you don't specify a version, the latest version is used automatically (`clientVersion: "latest"`). When you apply the latest version, you benefit from the continuous improvements, feature additions, and bug fixes that are made to the web chat regularly.

However, if you apply extensive customizations to your deployment, such as overriding the theme with your own custom theme, you might want to lock your deployment to a specific version. Locking on a version enables you to test new versions before you apply them to your live web chat.

To use a specific version (`clientVersion: "major.minor.patch"`), specify it as follows:

The following examples show what to specify when the current version is `2.3.1`.

- If you want to stay on a major version, but get the latest minor and patch releases, specify `clientVersion: "2"`.
- If you want to stay on a minor version, but get the latest patch releases, specify `clientVersion: "2.3"`. 
- If you want to lock on to a specific minor version and patch release, specify `clientVersion: "2.3.1"`.

To test the updates in a version release of the web chat before you apply the version to your live web chat, follow these steps:

1.  Lock the web chat that is running in your production environment to a specific version. 
1.  Embed your web chat deployment into a new page in a test environment, and then override the version lock setting. For example, specify `clientVersion: "latest"`.
1.  Test the web chat, and make adjustments to the configuration if necessary.
1.  Update your production deployment to use the latest version and apply any other configuration changes that you determined to be necessary after testing.

For more information about features that were introduced in previous web chat versions, see the [Web chat release notes](/docs/watson-assistant?topic=watson-assistant-release-notes-chat).

## Billing
{: #customize-web-chat-billing}

Watson Assistant charges based on the number of unique monthly active users (MAU).

The web chat uses the following methods to track users:

- You can pass in a de—identified user ID either as part of a secure JWT or as a string passed to the [`instance.updateUserID`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateuserid){: external} method. If you are using advanced security features, the user ID is derived from the sub claim in the JWT.
- If you do not pass an identifier for the user when the session begins, the web chat creates one for you. It creates a first-party cookie with a generated anonymous ID. The cookie remains active for 45 days. If the same user returns to your site later in the month and chats with your assistant again, the web chat integration recognizes the user. And you are charged only once when the same anonymous user interacts with your assistant multiple times in a single month.

### Apple devices
{: #customize-web-chat-billing-apple}

On Apple devices, the Intelligent Tracking Prevention feature automatically deletes any client-side cookie after 7 days. This means that if an anonymous customer accesses your website and then visits again two weeks later, the two visits are treated as two different MAUs.

To avoid this problem, use a server-side first-party cookie in your web application. For example, when an anonymous user visits your website for the first time, you can generate a unique user ID and store it in a server-side cookie with any expiration date you choose. Then, your code can use the [`updateUserID()`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateuserid){: external} instance method to set the user ID. You can then use the same cookie to set the same user ID for this customer on any future visits until it expires.

### More information

For more information about billing, see [User-based plans explained](/docs/watson-assistant?topic=watson-assistant-services-information#services-information-user-based-plans).

For more information about MAU limits per plan, see [Web chat integration limits](/docs/watson-assistant?topic=watson-assistant-deploy-web-chat#deploy-web-chat-limits).

For more information about deleting a user's data, see [Labeling and deleting data](/docs/watson-assistant?topic=watson-assistant-information-security#information-security-gdpr-wa).
