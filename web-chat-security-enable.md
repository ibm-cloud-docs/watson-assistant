---

copyright:
  years: 2019, 2023
lastupdated: "2023-10-26"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Enabling web chat security
{: #web-chat-security-enable}

To enable web chat security, you must make changes to your web application server code and the web chat embed script, as well as the web chat integration settings.
{: shortdesc}

## Before you begin
{: #web-chat-security-enable-prereq}

Before you enable security, you must create an RS256 public/private key pair. You can use a tool such as OpenSSL or PuTTYgen.

For example, to create the key pair at a command prompt using OpenSSL, you would use the command `openssl genrsa -out key.pem 2048`.

Save the generated key pair in a secure location.

Make sure these keys are accessible only by your server code. Never pass them to a client browser through your website.
{: important}

## Generating a JWT
{: #web-chat-security-enable-jwt}

To use web chat security, you must configure the web chat on your website to send a JSON Web Token (JWT) with each message to the assistant. The JWT is used to verify the origin of messages sent from your website, and optionally to carry additional encrypted data. Your website will need to be able to generate a new JWT at the beginning of each session, and also whenever an existing JWT expires.

Do not hardcode a JWT in your website code or share JWTs between users.
{: important}

On your server, implement a function that generates and returns a JSON Web Token (JWT) that is signed with your private key. You will use this token to verify the origin of messages sent from your website, and optionally to carry additional encrypted data.

Most programming languages offer JWT libraries that you can use to generate a token. To validate signed JWTs, the web chat integration uses the [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken){: external} library with the `RS256` algorithm.

The JWT payload must specify the following claims:

- `sub`: A unique user ID that identifies the customer who is interacting with the web chat. This can be either a generated unique identifier (for anonymous users) or an authenticated user ID. For more information about how the `sub` value is used, see [Authenticating users](/docs/watson-assistant?topic=watson-assistant-web-chat-security-authenticate).

    To ensure security, the JWT should be specific to each user. Use either the user's authenticated login information, or a unique generated ID. Do not reuse the same JWT, or the same `sub` value, for more than one user.

- `exp`: The expiration time after which the JWT is no longer valid. Many JWT libraries set this value for you automatically. Set a short-lived `exp` claim (for example, `1h`).

    Do not create a JWT without an `exp` claim. Although this claim is not formally required, omitting it represents a security exposure because anyone with access to the JWT could copy it and use it later to access your assistant. Setting an expiration time limits this exposure.
    {: tip}

The following JavaScript example shows how you might generate a JWT using the `jsonwebtoken` library:

```javascript
// Sample NodeJS code on your server.
const jwt = require('jsonwebtoken');

// Returns a signed JWT signed with the RS256 algorithm.
function createJWT() {
  const payload = {
    sub: 'some-user-id', // Identifies user for billing purposes
  };
  // The "expiresIn" option adds an "exp" claim to the payload.
  return jwt.sign(payload,
    process.env.YOUR_PRIVATE_RSA_KEY,
    { algorithm: 'RS256', expiresIn: '1h' });
}
```
{: codeblock}

## Configuring the web chat to include JWTs
{: #web-chat-security-include-messages}

Now that you have implemented a function to generate a signed JWT, you must update your web chat instance to include the signed JWT with each message it sends. After you enable web chat security, any messages that are not signed with the proper private key are rejected.

In your website HTML, update the web chat embed script to specify a new JWT at the beginning of each session, and also whenever the existing JWT expires. The simplest way to do this is to subscribe to the [`identityTokenExpired`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#identityexpired){: external} event and generate a new JWT when that event is received. The `identityTokenExpired` event is fired in both of the following situations:

- At the beginning of a new session, if no JWT was provided using the `identityToken` configuration option.

- When the previously specified JWT expires.

In your `onLoad` event handler, use the [`on()`](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#on){: external} instance method to subscribe to the `identityTokenExpired` event. 

In the callback, call the function on your server that you implemented to generate a new JWT. Then use the `identityToken` parameter of the event to specify the new JWT, as in this example:

```javascript
instance.on({ type: 'identityTokenExpired',
              handler: async function(event) {
                const jwtFromServer = await fetch('http://example.com:3001/createJWT');
                event.identityToken = jwtFromServer;
}});
```
{: codeblock}

The new JWT you specify is automatically sent with each subsequent message from the web chat instance on your web site (until the token expires).

You can also specify the JWT at the beginning of the session by using the `identityToken` property in the web chat configuration object. However, you will still need to create an event handler for `identityTokenExpired`, unless you are certain your JWTs will never expire during a session.
{: note}

## Updating the web chat settings
{: #web-chat-security-enable-update}

Now that you have configured the web chat to send signed JWTs, you can enable web chat security in the web chat integration settings.

After you enable web chat security, messages from any origin other than your web chat instance (which you have configured to send signed JWTs) are rejected. This means that enabling web chat security disables the shareable preview link, which does not send JWTs with messages. For more information about the preview link, see [Copying a link to share](/docs/watson-assistant?topic=watson-assistant-preview-share#preview-share-link).
{: important}

To enable security, complete the following steps:

1. On the **Security** tab of the web chat integration settings, set the **Secure your web chat** switch to **On**.

1. In the **Your public key** field, paste your [public key](#web-chat-security-enable-prereq).

    {{site.data.keyword.conversationshort}} uses the public key to verify that incoming messages originate from your website.

The following diagram shows the flow of messages between the web chat and the assistant when web chat security is enabled:

![Web chat security message flow](images/web-chat-security.png)

