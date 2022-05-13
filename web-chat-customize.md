---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-10"

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
{: #web-chat-customize}

If you are comfortable with JavaScript code, you can extensively customize and extend the web chat by modifying the embed script and using the web chat API.
{: shortdesc}

For detailed reference about the web chat API, see the web chat [developer documentation](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=){: external}.

## API overview
{: #web-chat-customize-api}

The web chat API consists of several components:

- **Configuration object**: The embed script defines a configuration object named `watsonAssistantChatOptions`, which specifies configuration objects for the web chat widget. By editing the configuration object, you can customize the appearance and behavior of the web chat before it is rendered. For more information about the available configuration options, see [Configuration options object](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#configurationobject){: external} in the web API reference.
- **Instance methods**: The web chat instance methods provide low-level control of the web chat widget. You can use the instance methods to implement custom behavior such as changing how the web chat widget opens, showing and hiding content, and setting identity information. For more information about the available instance methods, see [List of methods and properties](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#listofmethods){: external} in the web chat API reference.
- **Events**: The web chat event system makes it possible for your website to respond to web chat events (such as opening or closing the web chat window, sending or receiving messages). By subscribing to events, you can implement custom behavior or even intercept and modify message content. For more information about the event system, see [Events](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events){: external} in the web chat API reference.

## Change how the web chat opens and closes
{: #web-chat-customize-open-close}

You can change the color of the launcher icon from the *Style* tab of the web chat configuration page. If you want to make more advanced customizations, you can make the following types of changes:

- Change the launcher icon that is used to open the web chat widget. For a tutorial that shows you how, see [Using a custom launcher](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-launcher){: external}.
- Change how the web chat widget opens. For example, you might want to launch the web chat from some other button or process that exists on your website, or maybe open it in a different location, or at a different size. For a tutorial that shows you how, see [Render to a custom element](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-example-element){: external}.
- Hide the launcher icon entirely and automatically start the web widget in open state, at its full length. For more information, see the [`openChatByDefault` method](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#configurationobject){: external}.
- Hide the close button so users cannnot close the web chat widget. For more information, see the [`hideCloseButton` method](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#configurationobject){: external}.

## Change the home screen
{: #web-chat-customize-home-screen}

If enabled, the home screen greets the customer and shows a list of suggested conversation starters. You can customize the style and content of the home screen:

- A **Get started** heading is displayed before the list of conversation starter messages. You change this heading text by replacing the `homeScreen_conversationStarterLabel` in the web chat language strings file. For more information, see the [instance.updateLanguagePack() method](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updatelanguagepack){: external} documentation.
- You can use the web chat API to add other elements to the home screen. For more information, see the [instance.writeableElements() method](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#writeableelements){: external} documentation.
- You can use CSS helper classes to change the home screen style. For more information, see the [prebuilt templates](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-render#html){: external} documentation.

## Change the conversation
{: #web-chat-customize-conversation}

The core of the conversation is defined in your actions. If you use more than one integration type, focus on defining an engaging conversation in the underlying actions flow. The same actions setup is used for all integrations. To customize the conversation for the web chat only, you can take the following actions:

- Update the text of a message before it is sent or after it is received, such as to hide personally-identifiable information.
- Pass contextual information, such as the customer's name, from the web chat to your actions. For examples of how to complete common tasks, see [Passing values](#web-chat-config-context).
- Change the language that is used by the web chat. For more information, see [Global audience support](/docs/watson-assistant?topic=watson-assistant-customize-web-chat#web-chat-customize-global).
- Render your own custom response types inside the web chat widget, including responses that incorporate code from your website at run time. For a tutorial that shows you how, see [Creating a custom response](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-user-defined-response){: external}.
- Use React portals to render your custom response type as part of your application. For a tutorial that shows you how, see [Custom responses with React](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-react-portals){: external}.

## Change the look of the web chat
{: #web-chat-customize-look}

You can make simple changes to the color of things like the text font and web chat header from the *Style* tab of the web chat configuration page. To make more extensive style changes, you can set the CSS style color theme to a different theme or specify your own theme.

- You can choose to use a different base Carbon Design theme. The supported base themes are color themes that are defined by [IBM Carbon Design](https://www.carbondesignsystem.com/guidelines/color/usage/){: external}. For more information, see [Theming](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#theming){: external}.
- Alternatively, you can set individual variables within the theme to customize specific UI elements. For example, the text that is displayed in the chat window uses the fonts `IBMPlexSans, Arial, Helvetica, sans-serif`. If you want to use a different font, you can specify it by using the `instance.updateCSSVariables()` method.
- Apply style settings to user-defined response types. If you enable the web chat to return custom response types, be sure to apply existing or custom CSS classes to them. For more information, see [Custom content](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-render){: external}.
- Change the style of the home screen that can be displayed when the web chat is opened. For more information about the home screen, see [Adding a home screen](/docs/watson-assistant?topic=watson-assistant-deploy-web-chat#deploy-web-chat-home-screen). For more information about how to customize it, see [HTML content](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-render#html){: external}

The web chat is embedded directly on your page, not inside an iframe. Therefore, the cascading style sheet (CSS) rules for your website can sometimes override the web chat CSS rules. The web chat applies aggressive CSS resets, but the resets can be affected if your website uses the `!important` property in elements where style is defined.
{: note}

## Add user identity information
{: #web-chat-customize-userid}

If you do not enable security, and you want to perform tasks where you need to know the user who submitted the input, then you must pass the user ID to the web chat integration.

If you do enable security, you set the user ID in the JSON Web Token instead. For more information, see [Authenticating users](/docs/watson-assistant?topic=watson-assistant-web-chat-security#web-chat-security-authenticate).

Choose a non-human-identifiable ID. For example, do not use a person's email address as the `user_id`.

User information is used in the following ways:

- User-based service plans use the `user_id` associated with user input for billing purposes.
<!--- See [User-based plans](/docs/assistant?topic=assistant-services-information#services-information-user-based-plans){: external}. --->

- The ability to delete any data created by someone who requests to be forgotten requires that a `customer_id` be associated with the user input. When a `user_id` is defined, the product can reuse it to pass a `customer_id` parameter.
    <!--- See [Labeling and deleting data](/docs/assistant?topic=assistant-information-security#information-security-gdpr-wa){: external}. --->

    Because the `user_id` value that you submit is included in the `customer_id` value that is added to the `X-Watson-Metadata` header in each message request, the `user_id` syntax must meet the requirements for header fields as defined in [RFC 7230](https://tools.ietf.org/html/rfc7230#section-3.2).
    {: note}

To support these user-based capabilities, add the [`updateUserID()` method](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateuserid){: external} in the code snippet before you paste it into your web page.

In the following example, the user ID `L12345` is added to the script.

```html
<script>
  window.watsonAssistantChatOptions = {
      integrationID: 'YOUR_INTEGRATION_ID',
      region: 'YOUR_REGION',
      serviceInstanceID: 'YOUR_SERVICE_INSTANCE',
      onLoad: function(instance) {
        instance.updateUserID('L12345');
        instance.render();
        }
    };
  setTimeout(function(){
    const t=document.createElement('script');
    t.src='https://web-chat.global.assistant.dev.watson.appdomain.cloud/versions/' +
      (window.watsonAssistantChatOptions.clientVersion || 'latest') +
      '/WatsonAssistantChatEntry.js';
    document.head.appendChild(t);
  });
</script>
```
{: codeblock}

## Supporting global audiences
{: #web-chat-customize-global}

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

For more information about MAU limits per plan, see [Web chat integration limits](/docs/watson-assistant?topic=watson-assistant-web-chat-overview#web-chat-overview-limits).

For more information about deleting a user's data, see [Labeling and deleting data](/docs/watson-assistant?topic=watson-assistant-information-security#information-security-gdpr-wa).
