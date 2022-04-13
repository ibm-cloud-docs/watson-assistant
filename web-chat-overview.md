---

copyright:
  years: 2019, 2022
lastupdated: "2022-04-12"

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

The web chat is a chat widget you can embed on your website, providing an easy-to-use chatbot interface for your customers.
{: shortdesc}

For each assistant you create, the web chat integration provides a JavaScript code snippet that you can copy and paste into any web page where you want users to be able to ask your assistant for help. This script creates an instance of the web chat widget, saving you the time and effort that would be required to build your own custom user interface.

Building a custom user interface yourself would require spending time and effort solving typical UI problems. For example, you would need to design the layout and styling, keep up with browser changes, manage scrolling behavior, and validate input. The time you spend building and maintaining a custom UI is better spent building a high-quality assistant instead.

The web chat widget uses cutting-edge functionality from IBM Design and Research to deliver an exceptional user experience. It is also extensively customizable, which means that you can take advantage of the web chat functionality while still maintaining consistency with your website style and branding.

## How the web chat works

To learn more about web chat, watch the following 3-minute video.

![Web chat overview](https://www.youtube.com/embed/52bpMKVigGU){: video output="iframe" id="youtubeplayer" frameborder="0" width="560" height="315" webkitallowfullscreen mozallowfullscreen allowfullscreen}

To read a transcript of the video, [open the video on YouTube.com](https://www.youtube.com/watch?v=52bpMKVigGU&feature=emb_imp_woyt), click the *More actions* icon, and then choose *Open transcript*.

To learn more about how the web chat can help your business, read [the Medium blog post called Building a Virtual Assistant that Your Customers Want to Talk to](https://medium.com/ibm-watson/building-an-engaging-virtual-assistant-cf39cd0c3730){: external}.


### (Miscellaneous details moved from elsewhere)

![Plus or higher plans only](images/plus.png) For environments where private endpoints are in use, keep in mind that the web chat integration sends traffic over the internet.
<!--- For more information, see [Private network endpoints](/docs/assistant?topic=assistant-security#security-private-endpoints){: external}.
{: note} --->

If you don't extend the session timeout setting for the assistant, the flow for the current session is restarted after 5 minutes of inactivity. This means that if a user stops interacting with the assistant, after 5 minutes, any context variable values that were set during the previous conversation are set to null or back to their initial values.

## Browser support
{: #deploy-web-chat-browsers}

The web chat supports a variety of devices and platforms. As a general rule, if the last two versions of a browser account for more than 1% of all desktop or mobile traffic, the web chat supports that browser.

The following list specifies the minimum required browser software for the web chat (including the two most recent versions, except as noted):

- Google Chrome
- Apple Safari
- Mobile Safari
- Chrome for Android
- Microsoft Edge (Chromium and non-Chromium)
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

## Accessibility
{: #deploy-web-chat-accessibility}

IBM strives to provide products with usable access for everyone, regardless of age or ability.

The web chat integration is enabled for [Web Content Accessibility 2.1 Level AA](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/){: external} compliance. It is tested with both screen readers and automated tools on a continual basis.

## Billing
{: #deploy-web-chat-billing}

Watson Assistant charges based on the number of unique monthly active users (MAU).

By default, the web chat creates a unique, anonymous ID the first time a new user starts a session. This identifier is stored in a first-party cookie, which remains active for 45 days. If the same user returns to your site and chats with your assistant again while this cookie is still active, the web chat integration recognizes the user and uses the same user ID. This means that you are charged only once per month for the same anonymous user.

On Apple devices, the Intelligent Tracking Prevention feature might cause you to be billed multiple times within a month for the same user. You can avoid this problem by using a server-side cookie in your web application. For more information, see [Apple devices](/docs/watson-assistant?topic=watson-assistant-customize-web-chat#customize-web-chat-billing-apple).
{: #note}

For non-anonymous users who log in to your website, you can customize the web chat code to pass in user IDs that you manage. For more information, see [Apple devices](/docs/watson-assistant?topic=watson-assistant-customize-web-chat#customize-web-chat-billing).

### Web chat integration limits
{: #deploy-web-chat-limits}

The usage is measured differently depending on the plan type. For Lite plans, usage is measured by the number of `/message` calls (API) are sent to the assistant from the web chat integration. For all other plans, usage is measured by the number of monthly active users (MAU) that the web chat interacts with. The maximum number of allowed MAUs differs depending on your {{site.data.keyword.conversationshort}} plan type.

| Plan       |              Maximum usage |
|------------|---------------------------:|
| Enterprise |              Unlimited MAU |
| Premium (legacy) |        Unlimited MAU |
| Plus       |              Unlimited MAU |
| Trial      |                  5,000 MAU |
| Lite       | 10,000 API (approximately 1,000 MAU) |
{: caption="Plan details" caption-side="top"}
