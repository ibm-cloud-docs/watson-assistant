---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-24"

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

# Web chat overview
{: #web-chat-overview}

You can use the web chat integration to deploy your assistant on your website without writing any code. The web chat integration provides an easy-to-use chatbot interface that can integrate seamlessly with your site, without requiring the time and effort that would be required to build your own custom user interface.
{: shortdesc}

The web chat can help your customers start the conversation with common questions or tasks; it can display multimedia and interactive elements such as forms, and it can transfer customers to human agents for more help. A developer can customize the web chat to add even more capabilities.

## Why use the web chat?

Building a custom user interface requires spending time and effort solving typical UI problems. For example, you need to design the layout and styling, keep up with browser changes, manage scrolling behavior, validate input, and comply with accessibility requirements. The time you spend building and maintaining a custom UI is better spent building a high-quality assistant instead.

The web chat widget uses cutting-edge functionality from IBM Design and Research to engage your users when they need help, answer their questions quickly and efficiently, and provide fallback options so there is always a path to a solution. The web chat is easy for you to deploy and easy for customers to use it is secure and supports a wide range of desktop and mobile browsers.

The web chat is also customizable, which means that you can take advantage of the web chat functionality while still maintaining consistency with your website style and branding, adding custom UI elements, and integrating with external systems (such as live agent tools or CRM systems).

## How the web chat works

For each assistant, the web chat integration provides a preconfigured JavaScript code snippet that you can copy and paste into any web page where you want users to be able to interact with the assistant.

After you add the web chat script to your website, your customers will see a launcher icon that they can click to open the chat window and start a conversation with the assistant. The appearance of the launcher icon adapts to desktop and mobile browsers.

![web chat launcher in desktop browser](images/web-chat-desktop-highlighted.png)

When a customer clicks the launcher, the web chat window opens, initially displaying the _home screen_. The home screen displays a greeting and a set of suggested conversation starters for common questions and problems. The customer can either click a conversation starter or type a message in the input field to start the conversation with the assistant.

![web chat example home screen](images/web-chat-home-screen-lendyr.png)

The appearance and behavior of the launcher icon, the home screen, and most other aspects of the web chat can be configured and extensively customized to match your website style and branding. For more information, see [Configuring the web chat](/docs/watson-assistant?topic=watson-assistant-web-chat-config).
{: tip}

## Launcher appearance and behavior
{: #web-chat-overview-launcher}

The web chat launcher welcomes and engages customers so they know where to find help if they need it. By default, the web chat launcher appears in a small initial state as a circle in the bottom right corner:

![An example of the initial launcher](images/web-chat-icon.png)

After 15 seconds, the launcher expands to show a greeting message to the user. In this expanded state, a customer can still click the launcher to open the web chat. (If the customer reloads the page or navigates to a different page before the launcher has expanded, the 15-second timer restarts.)

The appearance of this expanded state differs slightly depending on whether the customer is using a desktop browser or a mobile browser:

- For desktop browsers, the expanded launcher shows two primary buttons the customer can click to open the web chat, and a **Close** button that closes the launcher.

    ![An example of the desktop launcher](images/desktop-launcher.png)

    The expanded launcher remains in its expanded state even if the customer reloads the page or navigates to a different page. It stays in its expanded state until the customer either opens it by clicking on either of the two primary buttons, or closes it, at which point it returns to its initial small state for the rest of the session.

- For mobile browsers, the launcher shows only a single primary button.

    ![An example of the mobile launcher](images/mobile-launcher.png)

    The customer can close the launcher by scrolling on the page, swiping right on the expanded launcher, or waiting 10 seconds, at which point the expanded launcher shrinks back to its initial small state automatically. If the user reloads the page or navigates to a different page while the laucher is expanded, it stays in its expanded state, and the 10-second timer restarts.

After the next page refresh, if the launcher remains in its small state without being clicked, it bounces up and down to attract the customer's attention. The first bounce happens 15 seconds after the page refresh; if the customer still does not click the launcher, it bounces again 60 seconds later. (The timing of the second bounce might be affected if the user refreshes the page or navigates to a different page.) If the user still does not click the launcher, it does not bounce again.

The language of the default text shown within the launcher depends on the locale configured for the web chat. If you customize the greeting text, the text you provide is used regardless of the locale settings.

You can configure the color of the launcher, as well as the greeting message text, in the web chat settings. For more information, see [Configuring the web chat](/docs/watson-assistant?topic=watson-assistant-web-chat-config).

## Rendering assistant output

In addition to plain text, {{site.data.keyword.conversationshort}} supports many response types that can be used to output multimedia and interactive elements. The web chat includes built-in support for a wide variety of response types:

- **Text formatting**: The web chat supports formatting text using either Markdown or HTML. You can use text formatting to apply text highlighting such as italics, or to include elements like paragraphs and headings.
- **URLs**: Valid URLS (such as `http://example.com`) are automatically rendered as clickable links. When a customer clicks a link in the web chat, the target website opens in a new browser tab.
- **Options**: Options responses (when the assistant asks the customer to select from a set of choices) are automatically rendered as interactive elements. (By default, a set of fewer than five options is rendered as a set of clickable buttons; five or more options are rendered as a drop-down list.)
- **Dates**: When the assistant asks the customer to specify a date, the web chat displays an interactive date picker. The customer can specify the date either by clicking the date picker or by typing a valid date value in the input field.
- **Multimedia responses**: The web chat supports all multimedia response types (`audio`, `image`, and `video`).
- **iframe**: The web chat supports the `iframe` response type, which embeds HTML content (such as a form or interactive map) directly in the web chat window.

For more information about how the web chat handles specific response types, see the [Response types reference](/docs/watson-assistant?topic=watson-assistant-response-types-reference#iframe).

## Human agent transfer

The web chat supports transferring the customer to a human agent in situations the assistant can't handle. If you configure one of the supported service desk integrations, the web chat can open a separate chat window in which the customer can communicate with a human agent.

Your assistant can then initiate a transfer in situations when the assistant is unable to handle a customer's requests. (For more information about initiating a transfer, see [Connecting to a human agent](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-human-agent).)

For information about how to add a service desk integration to the web chat, see [Adding service desk support](/docs/watson-assistant?topic=watson-assistant-deploy-web-chat-haa).

## Technical details

The web chat is displayed on your web site by a short JavaScript code snippet, which calls additional JavaScript code that is hosted by IBM Cloud. The hosted code is automatically updated with new features and fixes, so by default you will always have the latest version. (You can optionally [lock to a specific version](/docs/watson-assistant?topic=watson-assistant-web-chat-customize) if you prefer to control upgrades yourself.)

The code snippet that creates the web chat widget includes a configuration object, which you can modify to change the appearance and behavior of the web chat. The configuration object also specifies details that enable the web chat to connect to your assistant. If you are comfortable writing JavaScript code, you can extensively customize the web chat by modifying the code snippet and using the web chat API. For more information about the configuration object and the web chat API, see the [web chat developer documentation](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-overview){: external}.

The web chat uses the {{site.data.keyword.conversationshort}} v2 stateful API to communicate with the assistant. If the customer stops interacting with the assistant for a period of time longer than the inactivity timeout for your assistant, the session ends. However, if the customer keeps the window open and later sends another message, the web chat recreates the session, making it possible to continue the conversation.

### Browser support
{: #web-chat-overview-browsers}

The web chat supports a variety of devices and platforms. As a general rule, if the last two versions of a browser account for more than 1% of all desktop or mobile traffic, the web chat supports that browser.

The following list specifies the minimum required browser software for the web chat (including the two most recent versions, except as noted):

- Google Chrome
- Apple Safari
- Mobile Safari
- Chrome for Android
- Microsoft Edge
- Mozilla Firefox
- Firefox ESR (most recent ESR only)
- Opera
- Samsung Mobile Browser
- UC Browser for Android
- Mobile Firefox

For optimal results when rendering the web chat on mobile devices, the `<head>` element of your web page must include the following metadata element:

```html
<meta name="viewport" content="width=device-width, initial-scale=1" />
```
{: codeblock}

### Accessibility

IBM strives to provide products with usable access for everyone, regardless of age or ability.

The web chat integration complies with the [Web Content Accessibility 2.1 Level AA](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/){: external} standard. It is tested with both screen readers and automated tools on a continual basis.

### Language support

By default, the web chat displays hardcoded labels and messages in English, but support is built in for all of the languages supported by {{site.data.keyword.conversationshort}}. You can also choose from a wide selection of locales to customize the display of strings like dates and times for global audiences.

In whichever language you are using, you can also customize the text of any hardcoded strings.

For more information, see [Supporting global audiences](/docs/watson-assistant?topic=watson-assistant-web-chat-customize#web-chat-customize-global).

### Billing
{: #web-chat-overview-billing}

Watson Assistant charges based on the number of unique monthly active users (MAU).

By default, the web chat creates a unique, anonymous ID the first time a new user starts a session. This identifier is stored in a first-party cookie, which remains active for 45 days. If the same user returns to your site and chats with your assistant again while this cookie is still active, the web chat integration recognizes the user and uses the same user ID. This means that you are charged only once per month for the same anonymous user.

On Apple devices, the Intelligent Tracking Prevention feature automatically deletes any client-side cookie after 7 days. This means that if an anonymous customer accesses your website and then visits again two weeks later, the two visits are treated as two different MAUs. For information about how to avoid this problem, see [Managing user identity](/docs/watson-assistant?topic=watson-assistant-web-chat-customize#web-chat-customize-userid).
{: important}

For information about how to customize the handling of user identity information for billing purposes, see [Managing user identity](/docs/watson-assistant?topic=watson-assistant-web-chat-customize#web-chat-customize-userid).

The usage is measured differently depending on the plan type. For Lite plans, usage is measured by the number of `/message` calls (API) are sent to the assistant from the web chat integration. For all other plans, usage is measured by the number of monthly active users (MAU) that the web chat interacts with. The maximum number of allowed MAUs differs depending on your {{site.data.keyword.conversationshort}} plan type.

| Plan       |              Maximum usage |
|------------|---------------------------:|
| Enterprise |              Unlimited MAU |
| Premium (legacy) |        Unlimited MAU |
| Plus       |              Unlimited MAU |
| Trial      |                  5,000 MAU |
| Lite       | 10,000 API (approximately 1,000 MAU) |
{: caption="Plan details" caption-side="top"}

