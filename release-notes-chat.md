---

copyright:
  years: 2015, 2025
lastupdated: "2025-06-26"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Web chat release notes
{: #release-notes-chat}

Find out what's new in the web chat integration.
{: shortdesc}

The web chat changelog lists changes ordered by version number. For more information about the web chat, see [Integrating the web chat with your website](/docs/watson-assistant?topic=watson-assistant-deploy-web-chat).

For information about new features and improvements to the core {{site.data.keyword.conversationshort}} product, see [Release notes](/docs/watson-assistant?topic=watson-assistant-watson-assistant-release-notes).

## Controlling the web chat version
{: #release-notes-chat-version}

If you want to evaluate changes that are introduced in a web chat release before you apply them to your deployment, you can set a version of your web chat. For more information, see [Controlling the web chat version](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-versions).

## 8.10.0
{: #8.10.0}
*Release date: 26 June 2025*

- Performance and accessibility updates.

## 8.9.0
{: #8.9.0}
*Release date: 18 June 2025*

- Increased the response timeout limit from 40 seconds to 120 seconds to support more complex or time-consuming operations in custom extensions and conversational skills.
- Minor bug fixes.

## 8.8.0
{: #8.8.0}
*Release date: 9 May 2025*

- Added a new [`updateLauncherConfig`](https://web-chat.assistant.test.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateLauncherConfig) instance method.
- Added a new [`allow_return`](https://web-chat.assistant.test.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateHomeScreenConfig) property on `updateHomeScreenConfig`.
- Minor bug fixes.

## 8.7.1
{: #8.7.1}
*Release date: 20 March 2025*

- Fixed a bug with the date picker closing when a user clicks on it.
- Fixed a bug that occurs when using a `pre:receive` event to change a context property from a single value to an array.
- Fixed an accessibility bug with disambiguation responses.
- Updated the launcher icon used when using the chat with the IBM AI theme.
- Fixed a bug with the ZenDesk agent app zip file that would prevent the agent app from loading in ZenDesk.

## 8.7.0
{: #8.7.0}
*Release date: 17 February 2025*

- Bug fixes.

## 8.6.0
{: #8.6.0}
*Release date: 3 February 2025*

- **Stop Streaming:** Web chat has added a "Stop Response" button to stop streamed responses that can be canceled.
  - When the user clicks the "Stop response" button, it fires a [stopStreaming event](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#stopStreaming) that you can hook into.
- Bug fixes.

## 8.5.3
{: #8.5.3}
*Release date: 21 January 2025*

- **Changes to conversational search:** Made some UI changes to conversational search responses. This includes the removal of the "Accuracy of generated answers may vary." disclaimer.
- Bug fixes.

## 8.5.2
{: #8.5.2}
*Release date: 6 January 2025*

- Bug fixes.

## 8.5.1
{: #8.5.1}
*Release date: 5 December 2024*

- Enhanced table response type to allow users to change the number of rows visible per page.

- Fixed bug that caused the typing indicator to not be visible in browsers other than Chrome.

## 7.11.0
{: #7.11.0}
*Release date: 21 November 2024*

- Added an `asyncCallout` option to the `instance.send` method that can be used to ensure a call to an extension is done using a one step process instead of the default two step process.

## 8.5.0
{: #8.5.0}
*Release date: 18 November 2024*

- Fixed a minor accessibility issue.

## 8.4.0
{: #8.4.0}
*Release date: 21 October 2024*

- **Table response type:** Beta support for the new table response type is now available in web chat. For more information, see [Response types reference](/docs/watson-assistant?topic=watson-assistant-response-types-reference).

- Fixed styling issues for single card carousels.

- Fixed a bug that would sometimes cause an error message to be shown when the user clicks a link.

## 8.3.3
{: #8.3.3}
*Release date: 14 October 2024*

- **Accessibility fixes:** Added elements to web chat to make it easier to navigate the chat using the next and previous heading keys while using a screen reader.

- Fixed a focus issue with the custom menu. The menu will remain focused after the user selects an item from within the menu.

- Extensions can no longer cause the input field to become disabled while waiting for the extension to complete.

## 8.3.2
{: #8.3.2}
*Release date: 23 September 2024*

- Fixed a bug that broke the Journeys feature.

## 8.3.1
{: #8.3.1}
*Release date: 13 September 2024*

- Bug fixes.

## 8.3.0
{: #8.3.0}
*Release date: 9 September 2024*

- **Rich text support in conversational search:** Conversational search responses now support rich text formatting in responses, including Markdown.

- **Changes to conversational search sources:** Sources are no longer highlighted in conversational search responses by default. To see the highlights, you must expand the sources carousel and select the source.

- Added the region `aws-eu-central-1`.

- Fixed a bug in the NiceDFO service desk integration that made custom fields unavailable in some cases.

- Fixed a bug with the `aiTooltipAfterDescriptionElement` writeable element that prevented the content from being visible for some occurrences of the tooltip.

- Fixed a bug with the `instance.send` method when called from a `restartConversation` event that would cause web chat to incorrectly display the greeting message.

## 8.2.6
{: #8.2.6}
*Release date: 20 August 2024*

- Minor improvements.

## 8.2.5
{: #8.2.5}
*Release date: 12 August 2024*

- **Updated behavior of a search result:** You can now click the web chat card to see more information about the search result if the result is not contained in a URL or PDF file.

- Updated styling for errors received by the web chat.

## 8.2.4
{: #8.2.4}
*Release date: 5 August 2024*

- Fixed a bug that could cause the web chat to stop working if streaming from an extension is used.

## 8.2.3
{: #8.2.3}
*Release date: 29 July 2024*

- **Updated markdown behavior:** Fixed a problem with numbers in ordered lists not showing the right numbers.

- **Improved message responsiveness:** Removed or reduced the delay added to longer responses.

- Bug fixes.

## 8.2.2
{: #8.2.2}
*Release date: 15 July 2024*

- **Updated visuals for search results:** The visuals for search responses are updated to make it more consistent with conversational search. In addition, the web chat now displays the search results in a carousel.

- **Updates to dropdown fields:** The maximum width for the dropdown fields for `option` responses are removed. The width of the dropdown fields is now set to 100% of the width of the chat window. However, if you use the `hasContentMaxWidth: true` option, the width is limited to 380px.

- Bug fixes.

## 8.2.1
{: #8.2.1}
*Release date: 1 July 2024*

- Reverted the changes related to the line breaks and bullets in your assistant’s responses, which was introduced per improvements in markdown rendering in the previous release.

## 8.2.0
{: #8.2.0}
*Release date: 20 June 2024*

- **New layout configuration:** You can customize a full-screen chat window by setting a max-width and removing the drop shadow that provides seamless integration for your assistant. For more information, see [Layout configuration](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#layout-config).

- **New instance method:** You can change the title in the header of the chat with the new `updateMainHeaderTitle`. For more information, see [instance.updateMainHeaderTitle](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateMainHeaderTitle).

- **New Theme config option:** You can change the type of corners to give the web chat widget to be either "rounded" or "squared". For more information, see [Theming configuration](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#theme-config).

- **New Home Screen config option:** You can hide the **Home Screen** avatar, greeting message, and starters using the `homeScreenConfig.custom_content_only` so only custom content is visible. For more information, see [instance.updateHomeScreenConfig](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateHomeScreenConfig).

- Improved markdown handling of tables, code blocks, block quotes, and fenced code blocks.

- You can now see a change in line breaks and bullets in your assistant’s responses due to the improvements made in rendering markdown in the web chat.

- Bug fixes

## 8.1.3
{: #8.1.3}
*Release date: 10 June 2024*

- Minor bug fixes.

## 8.1.2
{: #8.1.2}
*Release date: 3 June 2024*

- Minor bug fixes.

## 8.1.1
{: #8.1.1}
*Release date: 10 May 2024*

- Minor bug fixes.

## 8.1.0
{: #8.1.0}
*Release date: 15 April 2024*

- **Support for conversational search streaming**: You can now enable or disable the conversational search streaming in web chat. To enable the conversational search streaming, go to **Integrations** > **Web chat** > **Style** in your assistant. Currently, you can enable streaming only for conversational search responses. However, your customers can see the search message stream in real time in their web chat. 

- **Accent colors for home screen**: You can now apply accent colors instead of the default background colors on the web chat home screen. You can also control the gradient that is displayed on the default home screen background. To change the background color on the web chat home screen, go to **Integrations** > **Web chat** > **Home screen** in your assistant.

- **Updates to `restartConversation()` method**: You can now use the `restartConversation()` method to delete the {{site.data.keyword.conversationshort}} session from the server in addition to deleting the {{site.data.keyword.conversationshort}} session from the client.
 
- **New `sessionExpired` event**: Your assistant now triggers a new `sessionExpired` event before the assistant session expires. For more information, see [sessionExpired event](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#sessionExpired){: external}.

## 8.0.1
{: #8.0.1}
*Release date: 2 April 2024*

- Fixed a bug that would prevent the web chat from loading if `clientVersion` was set to `'latest'`, `'8'`, or `'8.0'`. This bug did not affect web chats locked on previous versions.

## 8.0.0
{: #8.0.0}
*Release date: 1 April 2024*

- **New Carbon UI for web chat**: The web chat has an upgraded Carbon UI for AI, Carbon 11, that helps in AI explainability and adding visual cues to make your interaction AI responsive.

   You must update the Carbon design before you upgrade to web chat 8.0.0 because the new Carbon UI conflicts with the user defined responses and writeable elements.

   In addition, the new Carbon 11 design system does not support Carbon 10 components. Therefore, addition of the Carbon 10 components in to a web chat with the Carbon 11 design system might disrupt the design styling. However, you can add the Carbon 11 components in to an existing web chat with the Carbon 10 design system because the Carbon 11 components work along with the Carbon 10 components in the same code base without any design disruption. Therefore, you can upgrade any individual Carbon 10 component to Carbon 11 component in an existing web chat without disrupting the remaining Carbon 10 components.

   The new updated home screen design is no longer a solid accent color, although a future update will introduce control to the colors.

- **New theme configuration option**: You can now use a new` themeConfig` property object in web chat that replaces the `carbonTheme` configuration property. The following new options are available in the configuration object:

    - **`carbonTheme`** 
      
      Select a Carbon theme for your widget per the [Carbon Design System](https://carbondesignsystem.com/elements/color/tokens/).

    - **`useAITheme`** 
      
      To add IBM Carbon for AI branding to the web chat.
  
   For more information, see [Web chat theme configuration](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#theme-config){: external}.

- **Updated message API version**: Web chat now uses the `2023-06-15` version of the {{site.data.keyword.conversationshort}} API. The previous version was `2021-09-08`. For more information about changes in behavior for {{site.data.keyword.conversationshort}} with the new API version, see [Release notes for {{site.data.keyword.conversationshort}}](/docs/watson-assistant?topic=watson-assistant-watson-assistant-release-notes) .
  
- **New CSP requirements**: You must use the new CSP requirements for web chat. For more information, see [Web chat architecture security](/docs/watson-assistant?topic=watson-assistant-web-chat-architecture#web-chat-architecture-security).

- **Changes in custom service desk**: All the custom service desks must now implement a `getName()` function. If you are using a custom service desk without the `getName()` function, you must update your service desks before you upgrade to Web chat `8.0.0`. For more information, see [Custom Service Desk API details](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=service-desks-custom-sd#api-details){: external}.

- **Changes in page direction setting**: The `direction` configuration option is not available in web chat now because web chat now uses the `dir` attribute in the `html` element. In addition, the direction configuration is set to left-to-right by default.

- **Native Carbon classes replace the home screen help classes**: The native Carbon classes now replace the home screen help classes in web chat. For more information, see [Web chat CSS helper classes](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-render#helper-classes){: external}.

- **The loadWatsonAssistant.js file is no longer updated**: Starting from version 8.0.0, the `loadWatsonAssistantChat.js` file, which was used by the embed script to load the web chat, is no longer updated. Therefore, for web chat version 8.0.0, you must use the `WatsonAssistantChatEntry.js` file in the embed script to load the web chat instead of the `loadWatsonAssistantChat.js` file. For web chat versions `7.x` and earlier, you can continue to use the `loadWatsonAssistantChat.js` file  in the embed script even though it is replaced with the `WatsonAssistantChatEntry.js` file. To make any changes to the embed script, you access the full embed script in the `Embed` tab in the web chat settings.
 
- **Deprecated window methods**: In web chat version 8.0.0, the following window methods are deprecated:
        - `openWindow`
        - `closeWindow`
        - `toggleOpen` 
        
        However, {{site.data.keyword.conversationshort}} continues to support these window methods in web chat version 8.0.0. For more information about migrating from window to view methods, see [Migrating from window to view events and methods](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#windowviewmigration){: external}.
        
- **Deprecated events**: In web chat version 8.0.0, the following events are deprecated:
        - `window:pre:open` 
        - `window:open`
        - `window:pre:close`
        - `window:close`
        
        However, {{site.data.keyword.conversationshort}} continues to support these events in web chat version 8.0.0. For more information about migrating from window to view events, see [Migrating from window to view events and methods](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#windowviewmigration){: external}.


## 7.10.0
{: #7.10.0}

*Release date: 31 January 2024*

- **Show timestamps on messages**: You can now display timestamps on top of messages in the web chat with the `enableMessageTimestamps` configuration option. For more information, see [web chat configuration](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#configuration-object){: external}.
- **New response types**: You now have the option in web chat to render the new card, grid, carousel and button response types. For more information, see [Response types reference](/docs/watson-assistant?topic=watson-assistant-response-types-reference).

## 7.9.0
{: #7.9.0}

*Release date: 11 December 2023*

- **Enhanced sources view for conversational search**: In the conversational search feature of web chat, you can now access _sources_ of the highlighted response texts in a collapsible carousel. In addition, you can select and find the source for each highlighted text in a response by clicking on it. For more information, see [Conversational search](/docs/watson-assistant?topic=watson-assistant-conversational-search).
- **Added error handling to the built-in PDF viewer**: If any error occurs while opening a PDF document in its viewer, the web chat now automatically opens the document in a new tab of the web browser by using the native PDF viewer. This acts as a workaround for the issues such as unsupported CORS (Cross-origin resource sharing). However, in some browsers, the web chat generates a `popup-blocked` error while opening the document.
- **Added an option to disable the built-in PDF viewer**:  You can now disable the PDF viewer in web chat by configuring `disablePDFViewer`. When the PDF viewer is `disabled`, the documents open in a new tab by using the native PDF viewer in the web browser. For more information, see [web chat configuration](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#configuration-object){: external}.
- **New property in web chat state object**: In the object returned from the [getState()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#getState){: external} instance method, the new `userID` property contains the current ID of the web chat. For example, by using this feature, you can get information about the anonymous user ID that web chat assigns to a user by default if no user ID is created.

## 7.8.0
{: #7.8.0}

*Release date: 13 November 2023*

- **Added a built-in PDF viewer**: A built-in viewer for PDF files can be used for search results from watsonx Discovery that contains links to the PDF documents. The document links must support CORS (Cross-origin resource sharing) to open in web chat.
- **Enhanced routing configuration for the Salesforce integration**: The `additional_routing_info` data passed from your assistant to web chat now has `button_id` and `button_overrides` properties that can further control how web chat routes the user to an agent. The `button_ids` property is deprecated, and `button_overrides` is used instead. And all properties in the `additional_routing_info` objects are optional. If the value for a property is not included, web chat defaults to the value in live agent settings from the {{site.data.keyword.conversationshort}} web chat configuration. For more information, see [Routing information](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=service-desks-salesforce){: external}.
- **Modified the destroySession method**: The [destroySession](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#destroySession){: external} instance method was enhanced to delete the session from the {{site.data.keyword.conversationshort}} servers and remove session information from the browser memory when called.

## 7.7.1
{: #7.7.1}

*Release date: 16 October 2023*

- Bug fixes.

## 7.7.0
{: #7.7.0}

*Release date: 5 October 2023*

- **Added `fullWidth` to custom responses**: The `customResponse` event includes a `fullWidth` property that can be set to indicate to web chat of a custom response to be rendered full width in the main window. For more information, see [customResponse event](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#customresponse){: external}.

- **Longer message input is allowed**: The maximum number of characters in the message input field is increased from 300 to 2048.

- **File uploads to Salesforce**: The Salesforce integration supports the ability for users to upload files to an agent when the agent requests a file from the user. If your website has a content security policy, you might need to add `*.salesforce.com` to allow web chat to connect to the Salesforce endpoint used for uploading files.

- **Reconnecting to Salesforce agents**: The Salesforce integration automatically reconnects the user to the agent if web chat reloads while a user is engaged in conversation with an agent.

- **New branding**: The IBM watermark reflects the new IBM watsonx brand.

## 7.6.0
{: #7.6.0}

*Release date: 21 August 2023*

- **Added transaction ID to `onError` function:** Information in the `onError` config function contains the transaction ID in the `transactionID` property when some errors communicating with {{site.data.keyword.conversationshort}} occur. For more information, see [Listening for errors](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#onerrordetail){: external}.

- Fixed a bug that occurred when sending two messages to an extension without waiting.

- Fixed a bug where the web chat launcher did not render when canceling the `window:open` event during session history.

- Bug fixes.

## 7.5.0
{: #7.5.0}

*Release date: 31 July 2023*

- **New viewing options for the Journeys beta feature**: With Journeys adding a third view to web chat -- the other two views being the launcher and main window -- we moved away from methods and events that focused on opening and closing the main window. These events were deprecated in favor of a more generic view change system that includes a new [instance.changeView](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#changeView){: external} method, and [view:pre:change](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#viewprechange){: external} and [view:change](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#viewchange){: external} events. You have more flexibility and can open multiple views at the same time.

    Window methods and events are supported for existing assistants. If you add tours to your assistant, or are using tours, your window events and methods might not work as expected and might not be supported. If you wish to add tours to your assistant, you need to update your custom code to use the new view change methods and events.

    The current window methods and events are still supported for existing web chats and assistants but are deprecated and will be removed in a future version. For more information, see [Migrating from window to view events and methods](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#windowviewmigration){: external}.

- **New Genesys Web Messenger service desk integration**: The service desk integration for Genesys Web Messenger is no longer in beta, and now includes support for user information strings in more languages. For more information, see [Integrating with Genesys Web Messenger](/docs/watson-assistant?topic=watson-assistant-deploy-genesys).

- **New NICE CXone service desk integration**: The service desk integration for NICE CXone Digital First Omnichannel is released. For more information, see [Integrating with NICE CXone Digital First Omnichannel](/docs/watson-assistant?topic=watson-assistant-deploy-nice-cxone).

- **Added a restart button**: A new `showRestartButton` configuration option specifies whether the web chat interface needs to display a restart button in the header, in addition to the existing **`-`** (Minimize) button. A customer can click this button to end the conversation or end any conversation with a live agent, while keeping the chat open. The chat transcript is cleared, but any transcript of a conversation with a live agent is preserved. For more information, see [showRestartButton](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration){: external}.

- **Carbon charts**: [Carbon charts](https://v10.carbondesignsystem.com/data-visualization/getting-started/){: external} are supported in custom responses.

- **Reconnecting with a custom service desk integration**: Web chat now provides support to custom service desk integrations to allow them to reconnect the user to an agent when web chat is reloaded. For more information, see [Reconnecting sessions](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=service-desks-custom-sd#reconnect){: external}.

- **Screen sharing with a custom service desk integration**: Web chat provides support to custom service desk integrations to allow and to give the user options to agree to or stop a screen-sharing session with a service desk. The actual screen sharing capability is not provided by web chat; it must be provided by the service desk integration. [Screen sharing](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=service-desks-custom-sd#screen-sharing){: external}.

- The `history` property in message objects has a newly added `from_history` property that indicates whether the message came from session history. For more information, see [Message object extensions](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#messageextensions){: external}.

## 7.4.0
{: #7.4.0}

*Release date: 12 June 2023*

- **Added CSS variables for customizing the launcher**: For more information, see [instance.updateCSSVariables](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updatecssvariables){: external}.

## 7.3.0
{: #7.3.0}

*Release date: 30 May 2023*

- **Released a beta of Genesys Web Messenger service desk integration**, which currently includes user information strings in English. For more information, see [Genesys Web Messenger](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=service-desks-genesys){: external}. 
- **Added beta support for file sharing with custom service desk integrations** that currently includes user information strings in English. For more information, see [Custom service desks](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=service-desks-custom-sd){: external}. 

## 7.2.2
{: #7.2.2}

*Release date: 1 May 2023*

- Bug fixes.

## 7.2.1
{: #7.2.1}

*Release date: 24 April 2023*

- Bug fixes.

## 7.2.0
{: #7.2.0}

*Release date: 10 April 2023*

- Added support for inline iframe responses. For more information, see [Response types reference](/docs/watson-assistant?topic=watson-assistant-response-types-reference#response-types-json-iframe).

- Redesigned the agent conversation experience.

- Bug fixes.

## 7.1.1
{: #7.1.1}

*Release date: 13 February 2023*

- **New journey events**: The new [tour:start](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#tourstart){: external}, [tour:end](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#tourend){: external}, and [tour:step](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#tourstep){: external} events provide details about the user's progress through a journey (also known as a *tour*). These events can be used to navigate to a specific page when the user starts a journey or reaches a certain step, or to show a survey after a journey ends.

- **New journey instance methods**: The new [tours](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#tours){: external} object supports instance methods that provide better control over journeys. You can use these methods to start or end a journey, or to automatically navigate through a journey in response to user actions.

- **Added journey strings to the language pack**: New strings for journeys were added to the language pack. You can modify the strings in the language pack by using the [updateLanguagePack()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updatelanguagepack){: external} instance method. For more information about language packs, see [Languages](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-render#languages){: external}.

For more information about the journeys beta feature, see [Guiding customers with journeys](/docs/watson-assistant?topic=watson-assistant-journeys).

## 7.1.0
{: #7.1.0}

*Release date: 17 January 2023*

- **Updated Zendesk agent app**: The agent app for Zendesk is compatible with Zendesk workspaces.

- In the service desk starter kits, the instance of the web chat integration was added to the [serviceDeskFactory parameters](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=service-desks-custom-sd){: external} to make it accessible to custom service desk implementations.

- **New instance methods**: The new [elements.getMessageInput()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#elements-get-message-input){: external} and [elements.getHomeScreenInput()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#elements-get-home-screen-input){: external} instance methods enable access to the input fields used by the customer to send messages. You can use these methods to change the input or to execute an action as the user is typing (for example, to implement for a type-ahead feature).

- **New event**: The new [agent:pre:sessionHistory](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#agentpresessionhistory){: external} event filters potential PII from messages sent from a customer or service desk agent before the messages are sent to the assistant for storage in the session history.

- **New property in web chat state object**: In the object returned from the [getState()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#getState){: external} instance method, the new `isDebugEnabled` property indicates whether the web chat debug flag is set to `true`.

## 7.0.0
{: #7.0.0}

*Release date: 5 December 2022*

- **Streamlined live agent handoff**: The live agent handoff experience is streamlined and simplified. Instead of opening the live agent chat in a separate window, the web chat now shows the live agent entering the conversation in the same window.

    Because of this change, the [updateCustomMenuOptions](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updatecustommenuoptions){: external} instance method reflects a single view, with a single list of custom menu options. If you want to customize menu options only during a live agent chat, you can subscribe to the [agent:pre:startChat](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#agentprestartchat){: external} and [agent:endChat](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#agentendchat){: external} events to trigger your customizations.

- **`agent:endChat` changes**: The [agent:endChat](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#agentendchat){: external} event now also fires if the customer cancels a live agent request before the agent joins. If you want to show a post-chat form only after a live agent chat, you can use the new `requestCancelled` flag on the event to determine whether the request was canceled.

- **New configuration options**: The following new options are available in the configuration object:
    - `serviceDesk.availabilityTimeoutSeconds`: Specifies how long the web chat waits for an available agent before automatically canceling the live agent request.
    - `serviceDesk.disableAgentSessionHistory`: Disables storage of live agent chats in the session history. If this option is set to `true`, live agent chat history is not stored; this means that if the web chat is reloaded, the live agent chat history is lost.

    For more information, see [Service desk options](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#servicedeskoptions){: external}.

- **`elements` instance property**: A new [elements](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#servicedeskoptions){: external} instance property provides methods that you can use to apply CSS styles to individual elements used by the web chat. (Only the main window is supported.)

- **`skip_card` option for journeys**: Support added for a new `skip_card` property in the journeys beta feature. You can use this property to start a journey immediately without waiting for the customer to click the introductory card, or even to start a journey from your website without opening the web chat at all. For more information, see [Guiding customers with journeys](/docs/watson-assistant?topic=watson-assistant-journeys).

- **Path changes**: Some internal paths for communication with the assistant were changed. If you have firewall or proxy rules that are configured to allow specific paths, you might need to update your configuration to allow the following paths:

    - `/<SUBSCRIPTION_ID>/chat/<INTEGRATION_ID>/config`
    - `/<SUBSCRIPTION_ID>/chat/<INTEGRATION_ID>/message`

## 6.9.0
{: #6.9.0}

*Release data: 14 November 2022*

- You can now create _journeys_ to guide your customers through tasks they can already complete on your website. A journey is an interactive, multipart response that can combine text, video, and images, presented in sequence in a small window superimposed over your website.

    Journeys are available as a beta feature. For more information, see [Guiding customers with journeys](/docs/watson-assistant?topic=watson-assistant-journeys).

## 6.8.1
{: #6.8.1}

*Release date: 7 November 2022*

- Bug fixes.

## 6.8.0
{: #6.8.0}

*Release date: 31 October 2022*

- Added support for sending pre-chat information to the Salesforce integration.

## 6.7.0
{: #6.7.0}

*Release date: 10 October 2022*

- **New `updateIsTypingCounter()` method**: The new `updateIsTypingCounter()` instance method updates the counter that determines whether the typing indicator is displayed. For more information, see [instance.updateIsTypingCounter()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateistypingcounter){: external}.

- **New `updateBotUnreadIndicatorVisibility()` method**: The new `updateBotUnreadIndicatorVisibility()` instance method specifies whether the unread indicator on the launcher icon is shown or hidden. For more information, see [instance.updateBotUnreadIndicatorVisibility()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updatebotunreadindicatorvisibility){: external}.

- Connect to Agent and custom cards now have rounded corners.

- Bug fixes.

## 6.6.2
{: #6.6.2}

*Release date: 15 August 2022*

- Bug fixes

## 6.6.1
{: #6.6.1}

*Release date: 8 August 2022*

- The `servers` property now supports a new `webChatScriptPrefix` option. Use this property to configure a proxy between your users' browsers and the {{site.data.keyword.cloud_notm}} servers that host the web chat JavaScript code. For more information, see [Setting up a proxy](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#serversconfig){: external}.

## 6.6.0
{: #6.6.0}

*Release date: 25 July 2022*

- A new `servers` property is now available in the web chat configuration options. You can use this property to set up a proxy between your users' browsers and {{site.data.keyword.conversationshort}}. For more information, see [Setting up a proxy](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#serversconfig){: external}.

## 6.5.2
{: #6.5.2}

*Release date: 11 July 2022*

- Bug fix for `date` response type.

## 6.5.1
{: #6.5.1}

*Release date: 15 June 2022*

- Bug fix for the Zendesk integration.

## 6.5.0
{: #6.5.0}

*Release date: 6 June 2022*

- **New agent events**: New events are now fired by the web chat when messages are sent or received during a conversation with a live agent using a service desk integration. For more information, see [Agent events summary](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#agent-summary){: external}.

- Bug fixes.

## 6.4.1
{: #6.4.1}

*Release date: 16 May 2022*

- **Minimum size**: Reduced the minimum allowed size of the rendered web chat window to satisfy the accessibility requirements defined by the [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG21/){: external} standard.

- **Pop-up windows and tabs from iframes**: The web chat now allows pop-up windows and new tabs to be opened from content rendered inside `iframe` responses.

- **Faster responses**: Responses from the assistant are displayed more quickly and without a **`...`** typing indicator.

## 6.4.0
{: #6.4.0}

*Release date: 18 April 2022*

- **Date picker**: If you configure a step to collect a **Date** customer response, the step uses the new `date` response type to request that a graphical date picker displays so the customer can select a date, as an alternative to typing the date in the input field. Existing steps do not automatically inherit this behavior; if you want to use the date picker, you must delete the existing Date response and then re-add it.

- **Skip "connect to agent" card**: A new `serviceDesk.skipConnectAgentCard` configuration option is available. If this option is enabled, the web chat immediately connects to an agent when it receives a _Connect to agent_ response, without first displaying a card and waiting for the user to click.

- **Close button**: A new `showCloseAndRestartButton` configuration option specifies whether the web chat interface shows an **`X`** (Close) button in addition to the existing **`-`** (Minimize) button. A customer can click this button to close the web chat, end the conversation, and end any conversation with a live agent. The chat transcript is also cleared, but any transcript of a conversation with a live agent is preserved.

## 6.3.0
{: #6.3.0}

*Release date: 24 March 2022*

- **Search cards**: Search cards have a new design.

- **New `restartConversation()` method**: The new `restartConversation()` instance method restarts the conversation with the assistant by clearing the web chat transcript and starting a new session. It also fires two new events (`pre:restartConversation` and `restartConversation`).

    For more information, see [instance.restartConversation()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#restartconversation){: external}, [pre:restartConversation](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#prerestartconversation){: external}, and [restartConversation](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#restartconversation){: external}.
  
- **New `agentEndConversation()` method**: The new `agentEndConversation()` instance method immediately ends the conversation with a live agent without requesting confirmation from the user. For more information, see [instance.agentEndConversation()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#agentendconversation){: external}.

- Bug fixes.

## 6.2.0
{: #6.2.0}

*Release date: 7 March 2022*

- **Navigation**: Added navigation features for web chat. For example, new “Back” and “Minimize” buttons make it easier to navigate between the home screen, the chat view, and panels. A new customizable drop-down menu appears near the avatar in both the assistant and agent chat views. Add new options to the menu of the web chat. For more information, see [updateCustomMenuOptions](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updatecustommenuoptions {: external}.

    The experience of connecting to a live agent is also improved to make it clearer how a user requests an agent, returns to chatting with the assistant, and ends the conversation.

    Animations for the web chat panels were improved to make the whole experience more seamless and cohesive.

- **Launcher**: The new web chat launcher bounces on two different occasions to attract attention and encourage customer engagement. For more information, see [Launcher appearance and behavior](/docs/watson-assistant?topic=watson-assistant-web-chat-architecture#web-chat-architecture-launcher).

- **Launcher**: Support added to control what text the launcher greets the user with, and when the greeting message is shown. For more information, see [Launcher](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#launcher){: external}.

- **Locale**: The web chat no longer sets the locale in the system context to `en-us` when no locale is configured. The locale is set in the system context only if it is configured for web chat.

- Bug fixes.

## 6.1.0
{: #6.1.0}

*Release date: 7 February 2022*

- Updated to support internal changes to the preview link feature.

## 6.0.1
{: #6.0.1}

*Release date: 24 January 2022*

- Bug fix for the disclaimer. For more information, see [Configuration options object](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#configurationobject){: external}.

## 6.0.0
{: #6.0.0}

*Release date: 19 January 2022*

- **API version**: The web chat now uses the `2021-11-27` version of the {{site.data.keyword.conversationshort}} API. Previously it used the `2020-09-24` API version. For information about API changes introduced since the `2020-09-24` version, see the release notes for [27 November 2021](/docs/watson-assistant?topic=watson-assistant-watson-assistant-release-notes#watson-assistant-nov272021) and [16 July 2021](/docs/watson-assistant?topic=watson-assistant-watson-assistant-release-notes#watson-assistant-jul162021).

- **Launcher**: The new web chat launcher welcomes and engages customers so they know where to find help if they need it. For more information, see [Launcher appearance and behavior](/docs/watson-assistant?topic=watson-assistant-web-chat-architecture#web-chat-architecture-launcher).

- **Home screen**: Web chat home screen updated with a more modern look. For more information, see [Configuring the home screen](/docs/watson-assistant?topic=watson-assistant-web-chat-configure-home-screen).

- **Agent events**: New events are fired when using a service desk integration and interacting with a live agent. If you use a custom service desk integration based on the [starter kit](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter){: external}, you can use these events to create a pre-chat form before the agent escalation occurs, to create a post-chat form after the agent conversation ends, or to specify what happens if an agent is not available (for example, create a ticket submission form). For more information, see [Agent events summary](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#summary){: external}.

- **Markdown support**: The web chat now fully supports common Markdown formatting in messages received from an assistant. You might need to review existing assistant output that contains strings that might be recognized as Markdown. (For example, a line of text that begins with a greater-than (`>`) character is interpreted as a block quote.)

- **Time zone**: The time zone set in the context by the web chat no longer overrides any time zone set by the assistant.

- **Locale**: Any locale that is configured for the web chat is sent to the assistant as part of the context.

- **Window open events**: The `window:pre:open` and `window:open` events now fire any time that the chat window is opened, regardless of the reason. In previous releases, these events only fired if the window was opened by a customer clicking the built-in launcher. Other methods of opening the chat window, such as session history or custom launchers, did not fire these events.

    Event data passed to the listener has a new `reason` property that indicates the reason the window was opened. If you want to preserve the previous behavior, you can modify your handler to check this property:

    ```javascript
    instance.on({ type: "window:open", handler: event => {
      if (event.data.reason === 'default_launcher') {
        // Previous code.
      }
    }});
    ```

    For more information, see [Window open reasons](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#windowopenreasons){: external}.

- **hideCloseButton property renamed**: The `hideCloseButton` property for custom panels is renamed `hideBackButton`. The behavior of the property is unchanged. For more information, see [customPanel.open()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#custompanelopen){: external}.

## 5.1.2
{: #5.1.2}

*Release date: 11 December 2021*

- Bug fix for Salesforce integration.

## 5.1.1
{: #5.1.1}

*Release date: 5 November 2021*

- **"User is typing" support**: The web chat now supports displaying the "user is typing" message for service desks. This feature is supported for the Salesforce and Zendesk integrations, as well as any [starter kit](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter){: external} integration that implements it.
- Bug fixes.

## 5.1.0
{: #5.1.0}

*Release date: 28 October 2021*

- **Custom Panels**: The web chat now supports customizable panels that you can use to display any custom HTML content (for example, a feedback form or a multistep process). Your code can use instance methods to dynamically populate a custom panel, and open and close it. For more information, see [Custom Panels](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#custompanels){: external}.

## 5.0.2
{: #5.0.2}

*Release date: 4 October 2021*

- A [new tutorial](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-react-portals){: external} is now available that shows how to use Carbon components to customize user-defined responses and writeable elements.
- Bug fixes.

## 5.0.1
{: #5.0.1}

*Release date: 20 September 2021*

- Bug fixes.

## 5.0.0
{: #5.0.0}

*Release date: 16 September 2021*

- **New response types**: The web chat now supports the new `video`, `audio`, and `iframe` response types. For more information about these response types, see [Rich responses](/docs/watson-assistant?topic=watson-assistant-dialog-overview#dialog-overview-multimedia).

- **Link to start web chat**: You can now create a set of HTML links that go directly to your web chat and start conversations on specific topics. For example, you might want to send an email to invite customers to update their account information; you can include a link that opens the web chat on your site and sends the initial message `I want to update my account`. For more information, see [Creating links to web chat](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#pageLinks){: external}.

- **CSS improvements**: Improved CSS to change the way the web chat resets styles in areas where you can include your own custom content, such as user-defined responses and writeable elements. The new approach better protects custom content from accidental style overrides. For more information, see [Theming and custom content](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-render){: external}.

    If you have custom content (such as user-defined responses or writeable elements), verify that any styling is still rendering as you expect. Consider the new [ibm-web-chat--default-styles class](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-render#helper_classes){: external} to maintain consistency with the web chat default styles.
    {: note}

- **Support for Carbon components**: As part of the new styling support, you can now use [Carbon components](https://carbondesignsystem.com/components/overview/components/){: external} in user-defined responses and web chat writeable elements. These components inherit any theming customizations that you made to the web chat.

- **New embedded script**: The embedded script that you use to add web chat to your website is updated to avoid unexpected code changes when you lock onto a web chat version. The previous version of the script continues to work but is now deprecated. If you want to upgrade your existing web chat deployments to use the new script, copy the updated code snippet from the **Embed** tab of the web chat integration settings. (Remember to reapply any customizations you made.)
- **Removal of deprecated methods and events**:
    - The `error` event is replaced by the `onError` method in the [configuration object](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#configurationobject){: external}.
    - The `getID` method is removed.
- Microsoft Internet Explorer 11 is no longer a supported browser.

## 4.5.1
{: #4.5.1}

*Release date: 30 August 2021*

- Bug fixes for the interactive launcher beta feature. (For more information, see the `launcherBeta` at [Configuration options object](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#configurationobject){: external}.)

## 4.5.0
{: #4.5.0}

*Release date: 29 July 2021*

- A new `scrollToMessage` method is available for scrolling the web chat view to a specified message in the chat history. For more information, see [instance.scrollToMessage()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#scrollToMessage){: external}.
- A new `pre:open` event is available. This event is fired when the web chat window is opened, but before the welcome message or chat history are loaded. For more information, see [window:pre:open](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#windowpreopen){: external}.
- A new chat history widget is available for embedding in service desk agent UIs. This new widget is based on a read-only view of the standard web chat widget. For information about using the new chat history widget in integrations that are built with the starter kit, see [Embedded agent application](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=service-desks-custom-sd#agent-app){: external}.

## 4.4.1
{: #4.4.1}

*Release date: 6 July 2021*

- Bug fixes.

## 4.4.0
{: #4.4.0}

*Release date: 25 June 2021*

- Bug fixes.

## 4.3.0
{: #4.3.0}

*Release date: 7 June 2021*

- **Search suggestions**: If a search skill is configured for your assistant, the suggestions include a new **View related content** section, which contains search results that are relevant to the user input.
- **Focus trap**: A new `enableFocusTrap` option enables maintaining focus inside the web chat widget while it is open. For more information, see [Configuration options object](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#configurationobject){: external}.

## 4.2.1
{: #4.2.1}

*Release date: 6 May 2021*

- **Service URLs updated**: The URLs used by the web chat to communicate with the Assistant service were updated to remove the dependency on the deprecated `watsonplatform.net` domain. This change applies retroactively to version 3.3.0 and all subsequent web chat releases. Make sure the system that hosts the web chat widget has access to the new URL.

## 4.2.0
{: #4.2.0}

*Release date: 27 April 2021*

- **Conversation starters in suggestions**: The conversation starters that you configure for the home screen are now shown as suggestions. If suggestions are enabled, the conversation starters appear in a new section titled **People are also interested in** so customers can change the subject or start the conversation over.

- **`onError` callback**: The new `onError` callback option in the web chat configuration enables you to specify a callback function that is called if errors occur in the web chat; and makes it possible for you to handle any errors or outages that occur with the web chat. For more information, see [Listening for errors](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#onerror-detail){: external}.

- **Session ID available in widget state**: The state information returned by the `getState()` instance method now includes the session ID for the current conversation. For more information, see [instance.getState()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#getState){: external}.

- **IBM watermark**: The web chat can now display a **Built with IBM Watson** watermark to users. This watermark is always enabled for any new web chat integrations on Lite plans.

- **Fixes to rendering of list items**: Updated the rendering of HTML list items in the web chat widget.

## 4.1.0
{: #4.1.0}

*Release date: 8 April 2021*

- **Home screen now generally available**: Ease your customers into the conversation by adding a home screen to your web chat window. The home screen greets your customers and shows conversation starter messages that customers can click to easily start chatting with the assistant.

- **Home screen enabled by default**: The home screen feature is now enabled by default for all new web chat deployments.

- **Home screen context support**: You can now access context variables from the home screen. Initial context must be set using a `conversation_start` node.

## 4.0.0
{: #4.0.0}

*Release date: 16 March 2021*

- **Session history now generally available**: Session history allows your web chats to maintain conversation history and context when users refresh a page or change to a different page on the same website. It is enabled by default. For more information about this feature, see [Session history](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-session-history){: external}.

  Session history persists within only one browser tab, not across multiple tabs. The dialog provides an option for links to open in a new tab or the same tab. For more information, see [this example](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-session-history#Tutorial1) on how to format links to open in the same tab.

  Session history saves changes that are made to messages with the [pre:receive event](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#prereceive) so that messages still look the same on rerender. This data is only saved for the length of the session. If you prefer to discard the data, set `event.updateHistory = false;` so the message is rerendered without the changes that were made in the pre:receive event.

  [instance.updateHistoryUserDefined()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateHistoryUserDefined) provides a way to save state for any message response. With the state saved, a response can be rerendered with the same state. This saved state is available in the `history.user_defined` section of the message response on reload. The data is saved during the user session. When the session expires, the data is discarded.

  Two new history events, [history:begin](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#historybegin) and [history:end](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#historyend) announce the beginning and end of the history of a reloaded session. These events can be used to view the messages that are being reloaded. The history:begin event allows you to edit messages before they are displayed.

  For more information, see this example on saving the state of [customResponse](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#customresponse) types in session history.

- **Channel switching**: You can now create a dialog response type to functionally generate a connect-to-agent response within channels other than web chat. If a user is in a channel such as Slack or Facebook, they can trigger a channel transfer response type. The user receives a link that forwards them to your organization's website where a connection to an agent response can be started within web chat.

## 3.5.0
{: #3.5.0}

*Release date: 17 February 2021*

- **Session history (beta)**: Web chat session history (beta) is now available. This feature makes it possible to maintain conversation history and context when customers refresh the page or navigate to a different page on the same website. For more information, see [Session history (beta)](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-session-history).

## 3.4.1
{: #3.4.1}

*Release date: 2 February 2021*

- Made an accessibility enhancement to the chat history. Now, you can use keys to navigate the messages by clicking the chat history, and pressing Enter and the arrow keys to move from one message to the next.
- Added the `instance.updateAssistantInputFieldVisibility()` to hide or show the text input field. For example, you might use the `pre:receive` event to check whether an options response type is returned and if so, hide the text field so the user is forced to pick one of the available options only.
- Added the `instance.getState()` method. You can use it to check for specific conditions, such as `isWebChatOpen`, before you perform an action that might rely on the condition being true.

For more information, see [Instance methods](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods){: external}.

## 3.3.2
{: #3.3.2}

*Release date: 17 December 2020*

- Addressed accessibility issues.

## 3.3.1
{: #3.3.1}

*Release date: 3 December 2020*

- The translated strings in the [language files](https://github.com/watson-developer-cloud/assistant-web-chat/tree/main/languages) were revised and improved.
- An error message is shown now if a Java Web Token (JWT) that is provided with an incoming message is invalid. If the first JWT fails when the web chat opens, an error message is displayed in place of the web chat window that says, `There was an error communicating with {{site.data.keyword.conversationshort}}`. If the initial JWT is valid, but the token for a subsequent message is invalid, a more discreet error message is displayed in response to the insecure input.
- Bug fixes.

## 3.3.0
{: #3.3.0}

*Release date: 23 November 2020*

- Added support for passing contextual information to a service desk agent from web chat.
- You can now customize a `user_defined` response type. For more information, see the [Custom response type tutorial](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-user-defined-response).
- Bug fixes.

## 3.2.1
{: #3.2.1}

*Release date: 2 November 2020*

- **Bug fix**: Fixing a bug that prevented the web chat integration preview from working after security was enabled.

## 3.2.0
{: #3.2.0}

*Release date: 26 October 2020*

- **Security improvement**: If you enable security, you no longer need to include the `identityToken` property when the web chat is loaded on a web page. If a token is not initially provided, the existing identityTokenExpired event fires when the web chat is first opened to obtain one from your handler.

- **Starter kit update**: Customize the timeout that occurs when the web chat integration checks whether any service desk agents are online.

## 3.1.1
{: #3.1.1}

*Release date: 22 October 2020*

- **Accessibility improvement**: Changed how the announcement text is generated to prevent announcements from being duplicated. Announcement text is hidden text that is provided for use by screen readers to indicate when dynamic web page changes occur.

## 3.1.0
{: #3.1.0}

*Release date: 8 October 2020*

- **Suggestions now allow for trial and error**: If customers select a suggestion and find that the response is not helpful, they can open the suggestions list again and try a different suggestion.

## 3.0.0
{: #3.0.0}

*Release date: 22 September 2020*

- **Choose when a link to support is included in suggestions**: The Suggestions beta feature has moved to its own tab. You can enable suggestions even if your web chat is not set up to connect to a service desk solution. You can control if and when the option to connect to customer support is available from the suggestions list.

- **Search result format change**: To support the ability to show more than 3 search results in a response, the search skill response type format changed. If you are using `pre:receive` or `receive` handlers to process search results, you might need to update your code. The `results` property was replaced by the `primary_results` and `additional_results` properties. For more information about the search skill response type format, see the [API reference](/apidocs/assistant-v2#message){: external}.

- **Language pack key change**: Due to improvements that were made to allow you to specify separate chat transfer messages for situations where agents are available and unavailable, the [language source file](https://github.com/watson-developer-cloud/assistant-web-chat/tree/main/languages) was updated. The `agent_chatDescription` was renamed to `default_agent_availableMessage` and another key (`default_agent_unavailableMessage`) was added. If you defined a custom string for the `agent_chatDescription` key, you must modify your code to reflect this change.

## 2.4.0
{: #2.4.0}

*Release date: 2 September 2020*

- **Add a home screen**: Ease your customers into the conversation by adding a home screen to your web chat window. The home screen greets your customers and shows conversation starter messages that customers can click to submit to the assistant.

## 2.3.0
{: #2.3.0}

*Release date: 10 August 2020*

- **Introducing *Suggestions***: Enable this beta feature to show a helper icon in the chat that customers can click to see alternate topics or to connect to an agent.

- **Search results are now expandable**: When search results are displayed in the web chat, users can click **Show more** to see more of the search result text.

## 2.2.0
{: #2.2.0}

*Release date: 29 July 2020*

- **Introduced the `instance.writeableElements()` method**: The `instance.writeableElements()` method gives you zones in the web chat user interface where you can embed your own content. For example, you can add content to the end of the header where it is displayed even as the chat content changes. Or you can add custom content that is displayed before the welcome node. For more information, see [Instance methods](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#writeableelements){: external}.

- **Gave the *Send* button a new look**

  Changed the icon from ![Arrow send icon](images/web-chat-send-old.png) to ![Paper airplane send icon](images/web-chat-send.png).

- **Securing your web chat is easier**: You no longer need to specify the `acr` claim when you define the JWT. The Authentication Context Class reference is managed by the web chat automatically.

- Improved the quality of non-English translations.

- Made a few minor bug fixes.

## 2.1.2
{: #2.1.2}

*Release date: 2 July 2020*

- **Loading issue**: Fixed an issue that prevented the web chat from loading properly for some deployments with short JWT expiration claims.

## 2.1.1
{: #2.1.1}

*Release date: 1 July 2020*

- **Service desk agent initials are displayed**: When the web chat transfers a user to a service desk agent, the agent's avatar is displayed in the chat window to identify messages sent from the service desk agent. If the agent does not have an avatar, the first initial of the agent's name is displayed instead.

## 2.0
{: #2.0}

*Release date: 16 June 2020*

- **Versioning was added to web chat**: For more information, see [Versioning](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=key-concepts#versioning){: external}.

- **Added bidirectional support**: You can now use the `direction` parameter to choose whether to show text and elements in the web chat in right-to-left or left-to-right order. For more information, see  [Configuration](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration){: external}.

- **Introduced the `instance.destroySession()` method**: The `instance.destroySession()` method removes all cookie and browser storage that is related to the current web chat session. You can use this method as part of your website logout sequence. For more information, see [Instance methods](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#destroySession){: external}.

## 1.5.3
{: #1.5.3}

*Release date: 14 April 2020*

- **The *Font family* field was removed from the configuration page**: The text that is displayed in the chat window uses the fonts: `IBMPlexSans, Arial, Helvetica, sans-serif`. If you want to use a different set of fonts, you can customize the CSS for your web chat implementation. For more information, see [Theming](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#theming).
- When your implementation does not specify a unique user ID, the web chat adds a first party cookie with a generated anonymous ID to use to identify the unique user. The generated cookie now expires after 45 days. For more information, see [GDPR and cookie policies](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=key-concepts#datapolicy){: external}.

## 1.5.2
{: #1.5.2}

*Release date: 2 April 2020*

- **Introduced the `learningOptOut` parameter**: You can add the `learningOptOut` parameter and set it to `true` to add the `X-Watson-Learning-Opt-Out` header to each `/message` request that originates from the Web Chat. For more information about the header, see [Data collection](/apidocs/assistant-v2#data-collection){: external}. For more information, see [Configuration](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration){: external}.

## 1.4.0
{: #1.4.0}

*Release date: 20 March 2020*

- **Customize the CSS theme**: For more information, see [Theme configuration](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration#theme-config){: external}.

- **Shadow DOM is no longer used**: When you use custom response types or HTML in your dialog, you can apply CSS styles that are defined in your web page to the assistant's response. To override any default styling in the web chat, you must specify the `!important` modifier in your CSS.
