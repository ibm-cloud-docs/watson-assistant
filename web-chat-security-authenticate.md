---

copyright:
  years: 2019, 2023
lastupdated: "2023-10-26"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Authenticating users in web chat
{: #web-chat-security-authenticate}

With web chat security enabled, you can securely authenticate customers by user ID.
{: shortdesc}

The default behavior of the web chat integration is to identify unique users by setting the value of the `user_id` property that is sent as part of each message to the assistant. (For more information, see [Managing user identity information in web chat](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-userid).)

This approach is sufficient for tracking unique users for billing purposes, but it is not secure and should not be used for access control. If you enable web chat security, you can use JSON Web Tokens (JWTs) to securely authenticate your users and control access to functions of your assistant that require authorization.

## Authenticating with the `sub` claim
{: #web-chat-security-authenticate-sub}

To use this method for authenticating users, you must first enable the web chat security feature. For more information, see [Enabling web chat security](/docs/watson-assistant?topic=watson-assistant-web-chat-security-enable).
{: note}

When you create a JWT for the web chat, you must specify a value for the `sub` (subject) claim, which identifies the user. (For anonymous users, you can use a generated unique ID.)

When you generate a user ID for an anonymous user, be sure to save the generated ID in a cookie to prevent being billed multiple times for the same customer.
{: tip}

When the web chat integration receives a message signed with this JWT, it stores the user ID from the `sub` claim as `context.global.system.user_id`. For user-based plans, this user ID is used for billing purposes. (You cannot use the `updateUserID()` instance method to set the user ID if web chat security is enabled.) The same user ID is also used as the customer ID, which can be used to make requests to delete user data. Because the customer ID is sent in a header field, the ID you specify must meet the requirements for header fields as defined in [RFC 7230](https://tools.ietf.org/html/rfc7230#section-3.2){: external}.

If you are required to comply with GDPR requirements, you might need to persistently store any generated anonymous user IDs, especially for anonymous users who later log in with user credentials. Storing these user IDs makes it possible for you to later delete all data associated with an individual customer if requested to do so.
{: important}

For more information about user-based billing, see [User-based plans explained](/docs/watson-assistant?topic=watson-assistant-admin-managing-plan#admin-managing-plan-user-based). For more information about deleting user data, see [Labeling and deleting data](/docs/watson-assistant?topic=watson-assistant-admin-securing#securing-gdpr-wa).

If your customers are required to log in before starting a web chat session, you can use the authenticated user ID as the value of the `sub` claim when you create the JWT. Because the web chat integration validates the JWT and uses the `sub` claim to set the user ID, your assistant can now rely on `context.global.system.user_id` for secure access control to functions that require authorization.

After you specify the JWT for the web chat, you cannot change to a JWT with a different `sub` claim during the session. If you need to add authenticated login information in the middle of a session, you can store it as part of the user payload instead. For an example of how to do this, see [Tutorial: Authenticating a user in the middle of a session](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-security).
{: important}

## Logging out
{: #web-chat-security-logout}

To log out a customer, you must destroy the web chat.

If you reload the page when a customer logs out, call the [`destroySession()`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#destroySession){: external} instance method to remove any reference to the current session from the browser's cookies and storage. If you do not call this method, information that is protected by the JWT is not at risk, but the web chat will try to connect to the previous session and fail.

If you do not perform a full page reload when a customer logs out, call the [`destroy()`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#destroy){: external} instance method. The `destroy` method removes the current instance of the web chat that is configured for the current userID from the DOM and browser memory. Next, call the [`destroySession()`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#destroySession){: external} instance method.

