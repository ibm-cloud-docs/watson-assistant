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

## Launcher appearance and behavior
{: #deploy-web-chat-launcher}

The web chat launcher welcomes and engages customers so they know where to find help if they need it. By default, the web chat launcher appears in a small initial state as a circle in the bottom right corner:

![An example of the initial launcher](images/web-chat-icon.png)

After 15 seconds, the launcher expands to show a greeting message to the user. In this expanded state, a customer can still click the launcher to open the web chat. (If the customer reloads the page or navigates to a different page before the launcher has expanded, the 15-second timer restarts.) There are two slightly different appearances for this expanded state, depending on whether the user is using a desktop browser or a mobile browser. 

- For desktop browsers, the expanded launcher shows two primary buttons the customer can click to open the web chat, and a **Close** button that closes the launcher:

    ![An example of the desktop launcher](images/desktop-launcher.png)

    The expanded launcher remains in its expanded state even if the customer reloads the page or navigates to a different page. It stays in its expanded state until the customer either opens it by clicking on either of the two primary buttons, or closes it, at which point it returns to its initial small state for the rest of the session.

- For mobile browsers, the launcher shows only a single primary button:

    ![An example of the mobile launcher](images/mobile-launcher.png)

    The customer can close the launcher by scrolling on the page, swiping right on the expanded launcher, or waiting 10 seconds, at which point the expanded launcher shrinks back to its initial small state automatically. If the user reloads the page or navigates to a different page while the laucher is expanded, it stays in its expanded state, and the 10-second timer restarts.

After the next page refresh, if the launcher remains in its small state without being clicked, it bounces up and down to attract the customer's attention. The first bounce happens 15 seconds after the page refresh; if the customer still does not click the launcher, it bounces again 60 seconds later. (The timing of the second bounce might be affected if the user refreshes the page or navigates to a different page.) If the user still does not click the launcher, it does not bounce again.

The color of the launcher is specified by the **Accent color** field on the **Style** tab of the web chat settings. To change the color, specify a new color using a standard hexadecimal RGB value.

You can customize the greeting message displayed by the launcher on the **Launcher** tab of the web chat settings. The settings include separate greeting messages for the desktop and mobile versions of the launcher.

The language of the default text shown within the launcher depends on the locale configured for the web chat. For more information, see [Languages](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#languages){: external}. If you customize the greeting text, the text you provide is used regardless of the locale settings.
{: note}

## Rich responses
{: #deploy-web-chat-dialog}

The rich responses that you add to an action are displayed in the web chat as expected, with the following exceptions:

- **Connect to human agent**: If service desk support is enabled for the web chat, this response type triggers a chat transfer. If service desk support is not configured, this response type is ignored.
- **Option**: If your option list contains up to four choices, they are displayed as buttons. If your list contains five or more options, then they are displayed in a drop-down list.

<!--- For more information about rich response types, see [Rich responses](/docs/assistant?topic=assistant-dialog-overview#dialog-overview-multimedia){: external}. --->

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
