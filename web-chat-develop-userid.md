---

copyright:
  years: 2019, 2023
lastupdated: “2023-08-29”

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}


# Managing user identity information
{: #web-chat-develop-userid}

{{site.data.keyword.conversationshort}} charges based on the number of unique monthly active users (MAU).

If you do not pass an identifier for the user when the session begins, the web chat creates one for you. It creates a first-party cookie with a generated anonymous ID. The cookie remains active for 45 days. If the same user returns to your site later in the month and chats with your assistant again, the web chat integration recognizes the user. And you are charged only once when the same anonymous user interacts with your assistant multiple times in a single month.

If you want to perform tasks where you need to know the user who submitted the input, then you must pass the user ID to the web chat integration. Choose a non-human-identifiable ID. For example, do not use a person's email address as the user ID.

In addition, the ability to delete any data created by someone who requests to be forgotten requires that a `customer_id` be associated with the user input. When a `user_id` is defined, the product can reuse it to pass a `customer_id` parameter. (For more information about deleting user data, see [Labeling and deleting data](/docs/watson-assistant?topic=watson-assistant-admin-securing#securing-gdpr-wa).)

Because the `user_id` value that you submit is included in the `customer_id` value that is added to the `X-Watson-Metadata` header in each message request, the `user_id` syntax must meet the requirements for header fields as defined in [RFC 7230](https://tools.ietf.org/html/rfc7230#section-3.2).

To support these user-based capabilities, add the [`updateUserID()` method](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateuserid){: external} in the code snippet before you paste it into your web page.

If you enable security, you set the user ID in the JSON Web Token instead. For more information, see [Authenticating users](/docs/watson-assistant?topic=watson-assistant-web-chat-security#web-chat-security-authenticate).
{: note}

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

## Apple devices
{: #web-chat-develop-billing-apple}

On Apple devices, the Intelligent Tracking Prevention feature automatically deletes any client-side cookie after 7 days. This means that if an anonymous customer accesses your website and then visits again two weeks later, the two visits are treated as two different MAUs.

To avoid this problem, use a server-side first-party cookie in your web application. For example, when an anonymous user visits your website for the first time, you can generate a unique user ID and store it in a server-side cookie with any expiration date you choose. Then, your code can use the [`updateUserID()`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateuserid){: external} instance method to set the user ID. You can then use the same cookie to set the same user ID for this customer on any future visits until it expires.

## More information

For more information about billing, see [User-based plans explained](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-admin-managing-plan).

For more information about MAU limits per plan, see [Pricing](https://www.ibm.com/products/watsonx-assistant/pricing).

For more information about deleting a user's data, see [Labeling and deleting data](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-admin-securing).

