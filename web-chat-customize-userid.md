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

# Managing user identity information
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

