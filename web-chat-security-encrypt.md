---

copyright:
  years: 2019, 2022
lastupdated: "2022-12-08"

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

# Encrypting sensitive data
{: #web-chat-security-encrypt}

By using the public key that is provided by IBM, you can add an additional level of encryption to hide sensitive data you send from the web chat.
{: shortdesc}

To use this method for encrypting data, you must first enable the web chat security feature. For more information, see [Enabling web chat security](/docs/watson-assistant?topic=watson-assistant-web-chat-security-enable).
{: note}

Use this method to send sensitive information in messages that come from your website, such as information about a customer's loyalty level, a user ID, or security tokens to use in webhooks that you call from your actions. Information that is passed to your assistant in this way is stored in a private context variable. (Private variables cannot be seen by customers and are never sent back to the web chat.)

For example, you might start a business process for a VIP customer that is different from the process you start for less important customers. You do not want non-VIPs to know that they are categorized as such, but you must pass this information to your action so it can change the flow of the conversation. To do this, you can pass the customer MVP status as an encrypted variable. This private context variable is available for use by the action, but not by anything else.

![development icon](images/development-icon.png) **Tutorial:** For a tutorial that shows an example of using web chat security to authenticate users and protect sensitive data, see [Tutorial: Authenticating a user in the middle of a session](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-security).
{: tip}

To encrypt sensitive data, follow these steps:

1. On the **Security** tab of the web chat integration settings, copy the public key from the **IBM provided public key** field. (This field is available only if [web chat security is enabled](#web-chat-security-enable).)

1. In the JavaScript function you use to create your JWT, include in the payload a private claim called `user_payload`. Use this claim to contain the sensitive data, encrypted with the IBM public key.

    For example, the following code snippet shows a function that accepts a userID and user payload. If a user payload is provided, its content is encrypted and signed with the IBM public key. (In this example, the public key is stored in an environment variable.)

    ```javascript
    // Example code snippet to encrypt sensitive data in JWT payload.
    const jwt = require('jsonwebtoken');
    const RSA = require('node-rsa');

    const rsaKey = new RSA(process.env.PUBLIC_IBM_RSA_KEY);

    /**
    * Returns a signed JWT. Optionally, also adds an encrypted user payload
    * as stringified JSON in a private claim.
    */
    function mockLogin(userID, userPayload) {
      const payload = {
        sub: userID, // Required
        // The exp claim is automatically added by the jsonwebtoken library.
    };
    if (userPayload) {
        // If there is a user payload, encrypt it using the IBM public key
        // and base64 format.
        payload.user_payload = rsaKey.encrypt(userPayload, 'base64');
    }
    const token = jwt.sign(payload, process.env.YOUR_PRIVATE_RSA_KEY, { algorithm: 'RS256', expiresIn: '1h' });
    return token;
    }
    ```
    {: codeblock}

    The user payload must be valid JSON data. The web chat uses the default options of the [Node-RSA](https://www.npmjs.com/package/node-rsa){: external} library, which expects the encryption scheme `pkcs1_oaep` and the encryption encoding `base64`.
    {: tip}

1. When the web chat integration receives a message signed with this JWT, the content of the `user_payload` claim is decrypted and saved as the `context.integrations.chat.private.user_payload` object. Because this is a private variable, it will not be included in logs.

