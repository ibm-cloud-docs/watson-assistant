---

copyright:
  years: 2023
lastupdated: "2023-01-19"

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



# Tutorial: Authenticating a user in the middle of a session
{: #web-chat-develop-security}

If you have web chat security enabled, you must set a user ID for the customer at the beginning of the session as part of the JSON Web Token (JWT) you use to sign messages. For users who are not authenticated, this is typically a generated ID, and it cannot be changed after the JWT is created. However, you can use a private variable to authenticate a user later in the session.
{: shortdesc}

With web chat security enabled, the user ID associated with each message is based on the `sub` claim in the JWT payload. This value must be set at the beginning of the session, when the JWT is created, and cannot be changed during the life of the session. For unauthenticated (anonymous) users, you would typically use a generated ID, saved to a cookie, to ensure that each unique customer is counted only once for billing purposes.

However, you might want your customers to be able to authenticate in the middle of a session (for example, to complete an action that updates the user's account information). Because the generated user ID in the `sub` claim cannot be changed, you need another way to authenticate the user securely. You can do this by storing the customer's actual authenticated user ID as a private variable in the user payload of the JWT. (You could store the user ID in an ordinary context variable, but this would not be secure, because such variables can be modified.)

For a complete, working version of the example described in this tutorial, see [Enabling security for {{site.data.keyword.conversationshort}} web chat](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/webchat/examples/web-chat-security){: external}.
{: note}

This example in this tutorial, which is based on an Express server for Node.js, shows how to start a session with an anonymous user ID and then authenticate the user during the session.

1. Create a function called `getOrSetAnonymousID()` that generates a unique anonymous user ID for each customer and stores it in a cookie (or, if the cookie already exists, uses the stored user ID).

    Use a cookie that lasts for at least 45 days. If you do not store the user ID for more than 30 days, the same customer might be counted as multiple different users during the same billing period. (This can still happen if the same user deletes the cookie or uses a different browser.)
    {: tip}
    
```javascript
function getOrSetAnonymousID(request, response) {
  let anonymousID = request.cookies['ANONYMOUS-USER-ID'];
  if (!anonymousID) {
    anonymousID = `anon-${uuid()}`;
  }

  response.cookie('ANONYMOUS-USER-ID', anonymousID, {
    expires: new Date(Date.now() + 1000 * 60 * 60 * 24 * 45), // 45 days.
    httpOnly: true,
  });

  return anonymousID;
}
```

1. In the function you use to create a JWT, use the anonymous ID returned from the `getOrSetAnonymousID()` function as the value of the `sub` claim. This sets the value of the user ID that will be used to uniquely identify the customer for billing purposes.

    In addition, retrieve any value from the `SESSION_INFO` cookie, which we will use to store authenticated login information. If a value exists, store it in the `user_payload` private claim of the JWT. (If the user has not yet authenticated, this cookie does not yet exist.)

```javascript
const jwtContent = {
  sub: anonymousUserID,
  user_payload: {
    name: 'Anonymous',
    custom_user_id: anonymousUserID,
  },
};

if (sessionInfo) {
  jwtContent.user_payload.name = sessionInfo.userName;
  jwtContent.user_payload.custom_user_id = sessionInfo.customUserID;
}
```

1. Create a function to handle user authentication. In our example, we are using a simple `authenticate()` function that sets a hardcoded user ID, but in a real application the user ID would probably be retrieved from a database after a secure authentication check. Store the user information in the `SESSION_INFO` cookie.

```javascript
function authenticate(request, response) {

  const userInfo = {
    userName: 'Cade',
    customUserID: 'cade-id',
  };

  response.cookie('SESSION_INFO', JSON.stringify(userInfo), { encode: String });

  response.send('Ok');
}
```

1. When a user logs in, call the `authenticate()` function to store the user information in the `SESSION_INFO` cookie. Then call the `createJWT()` function to regenerate the JWT, using the updated session info to populate the `user_payload` claim.

    In [our example](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/webchat/examples/web-chat-security){: external}, authentication is simulated with a simple button click. The same button also simulates logging out by deleting the cookie:

    ```javascript
    async function onClick() {
      if (getCookieValue('SESSION_INFO')) {
        document.cookie = 'SESSION_INFO=; Max-Age=0';
      } else {
        await fetch('http://localhost:3001/authenticate');
      }

      const result = await fetch('http://localhost:3001/createJWT');
      const newToken = await result.text();

      webChatInstance.updateIdentityToken(newToken);

      updateUI();
    }
    ```

    The anonymous ID in the `sub` claim will continue to be used to track the customer for billing purposes, but now the customer's real user ID is stored separately in the user payload.

1. In your actions, you can now access the customer's real user ID by referencing the `user_payload` private context variable:

```text
${system_integrations.chat.private.user_payload}.custom_user_id
```

For complete working code, see the [Enabling security for {{site.data.keyword.conversationshort}} web chat](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/webchat/examples/web-chat-security){: external} example.

If you are required to comply with GDPR requirements, you might need to persistently store any generated anonymous user IDs, especially for anonymous users who later log in with user credentials. Storing these user IDs makes it possible for you to later delete all data associated with an individual customer if requested to do so.
{: important}

