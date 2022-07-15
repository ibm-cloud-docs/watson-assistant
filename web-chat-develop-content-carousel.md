---

copyright:
  years: 2022
lastupdated: "2022-07-13"

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

# Tutorial: Rendering a custom response as a content carousel
{: #web-chat-develop-content-carousel}

This tutorial shows how you might use custom responses to render information in the form of a content carousel.
{: shortdesc}

For a complete, working version of the example described in this tutorial, see [Content carousel for {{site.data.keyword.conversationshort}} web chat](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/webchat/examples/content-carousel){: external}.
{: note}

A _content carousel_ (or _slider_) is a type of interactive element that shows options as a scrollable series of slides.

{{site.data.keyword.conversationshort}} does not have a built-in response type for content carousels. But that isn't a problem: you can use the `user_defined` response type to send a custom response with the information you want to show, and extend the web chat to render the content carousel using standard JavaScript libraries.

![Content carousel in web chat](images/web-chat-tutorial-content-carousel.png)

This example shows how you can use the [Swiper](https://swiperjs.com/){: external} library to render a custom response as a content carousel:

1. In the action step that you want to create a content carousel, use the JSON editor to define a `user_defined` custom response. 

1. Add a step to your action that returns a `user_defined` response. Use the JSON editor to send the following response. This embeds the carousel data inside the `user_defined` object, but you could also put the data into skill variables that can be accessed by web chat from the context object.
```json
{
  "generic": [
    {
      "user_defined": {
        ... // Data for what to display in the carousel.
      },
      "response_type": "user_defined"
    }
  ]
}
```
2. Register a listener for the custom response event. When web chat receives a `user_defined` response from the assistant, it will fire this event.
```javascript
instance.on({ type: 'customResponse', handler: customResponseHandler });
```
3. Create the handler that will display the information from the assistant.
```javascript
function customResponseHandler(event) {
  const { message, element, fullMessage } = event.data;
  // You could also look up variables from context using something like "fullMessage.context.skills['actions skill'].skill_variables"
  const messageData = message.user_defined;
  element.innerHTML = `<div>...the carousel will go here</div>`;
  // Use a library such as Swiper to render the slides and provide the interactive functionality for the
  // carousel. The linked example will show the details for this.
}
```

For complete working code see [the example in our GitHub repository](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/webchat/examples/content-carousel).