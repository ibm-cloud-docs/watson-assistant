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

# Web chat customization overview
{: #web-chat-customize}

If you are comfortable with JavaScript code, you can extensively customize and extend the web chat by modifying the embed script and using the web chat API.
{: shortdesc}

For detailed reference about the web chat API, see the web chat [developer documentation](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=){: external}.

## Web chat API
{: #web-chat-customize-api}

The web chat API consists of several components:

- **Configuration object**: The embed script defines a configuration object named `watsonAssistantChatOptions`, which specifies configuration objects for the web chat widget. By editing the configuration object, you can customize the appearance and behavior of the web chat before it is rendered. For more information about the available configuration options, see [Configuration options object](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#configurationobject){: external} in the web API reference.
- **Instance methods**: The web chat instance methods provide low-level control of the web chat widget. You can use the instance methods to implement custom behavior such as changing how the web chat widget opens, showing and hiding content, and setting identity information. For more information about the available instance methods, see [List of methods and properties](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#listofmethods){: external} in the web chat API reference.
- **Events**: The web chat event system makes it possible for your website to respond to web chat events (such as opening or closing the web chat window, sending or receiving messages). By subscribing to events, you can implement custom behavior or even intercept and modify message content. For more information about the event system, see [Events](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events){: external} in the web chat API reference.

## Customizing phrases
{: #web-chat-customize-phrasing}

You can edit the hardcoded phrases that are displayed in the web chat to customize them for branding or style. Whether your web chat responds in English or another language, you can customize the wording that is used. For example, you might want to replace the phrase that says, `The live agent is typing` with the phrase, `A customer support agent is typing`.

The language files contain [ICU Message Format](http://userguide.icu-project.org/formatparse/messages){: external} JSON representations of all of the languages that are supported by the web chat. You can edit all or a subset of the phrases in a JSON file, and then configure the web chat to use your version by specifying the `instance.updateLanguagePack()` method.

For more information, see [Languages](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#languages){: external}.

## Versioning
{: #web-chat-customize-versions}

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

## Managing user identity
{: #web-chat-customize-userid}

Watson Assistant charges based on the number of unique monthly active users (MAU).

The web chat uses the following methods to track users:

- You can pass in a de—identified user ID either as part of a secure JWT or as a string passed to the [`instance.updateUserID`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateuserid){: external} method. If you are using advanced security features, the user ID is derived from the sub claim in the JWT.
- If you do not pass an identifier for the user when the session begins, the web chat creates one for you. It creates a first-party cookie with a generated anonymous ID. The cookie remains active for 45 days. If the same user returns to your site later in the month and chats with your assistant again, the web chat integration recognizes the user. And you are charged only once when the same anonymous user interacts with your assistant multiple times in a single month.

### Apple devices
{: #web-chat-customize-billing-apple}

On Apple devices, the Intelligent Tracking Prevention feature automatically deletes any client-side cookie after 7 days. This means that if an anonymous customer accesses your website and then visits again two weeks later, the two visits are treated as two different MAUs.

To avoid this problem, use a server-side first-party cookie in your web application. For example, when an anonymous user visits your website for the first time, you can generate a unique user ID and store it in a server-side cookie with any expiration date you choose. Then, your code can use the [`updateUserID()`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateuserid){: external} instance method to set the user ID. You can then use the same cookie to set the same user ID for this customer on any future visits until it expires.

### More information

For more information about billing, see [User-based plans explained](/docs/watson-assistant?topic=watson-assistant-services-information#services-information-user-based-plans).

For more information about MAU limits per plan, see [Billing](/docs/watson-assistant?topic=watson-assistant-web-chat-overview#web-chat-architecture-billing).

For more information about deleting a user's data, see [Labeling and deleting data](/docs/watson-assistant?topic=watson-assistant-information-security#information-security-gdpr-wa).
