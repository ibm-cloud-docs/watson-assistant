---

copyright:
  years: 2019, 2023
lastupdated: "2023-10-26"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Overview: Securing a web chat
{: #web-chat-security}

If you enable security, you can configure the web chat to authenticate users, protect private data, and restrict access to your assistant.
{: shortdesc}

All messages that are sent between the web chat and the assistant are encrypted using Transport Layer Security (TLS), which protects sensitive data as it travels through the network. However, there are still potential security exposures that you might need to protect against. By enabling the web chat security feature and updating your website code appropriately, you can add the following protections:

- You can prevent unauthorized websites from sending messages to your assistant, even if they copy your web chat embed script. (The unique identifiers in the embed script, such as the integration ID and service instance ID, are visible to anyone who has access to your website.)

- You can securely authenticate customers to control access to features of your assistant that require authorization.

- You can encrypt sensitive data so customers cannot see it, while still allowing your assistant to access it.

Web chat security uses JSON Web Tokens (JWTs), which are data objects that are sent with each message from your website to the {{site.data.keyword.conversationshort}} service. Because a JWT is digitally signed using a private encryption key that only you have, it ensures that each message originates with your website. The JWT payload can also be used to securely authenticate users and carry encrypted private data.

For detailed information about JSON Web Tokens, see the [JWT specification](https://tools.ietf.org/html/rfc7519){: external}).
{: tip}

Enabling web chat security involves making the following customizations:

- Implementing web application server code that generates a JWT signed with your private encryption key

- Customizing the web chat configuration to provide the generated JWT

- Enabling security in the web chat security settings

    After you enable web chat security, any message received by the web chat integration that is not accompanied by a properly signed JWT will be rejected.
    {: important}

For detailed information about how to complete these steps, see [Enabling web chat security](/docs/watson-assistant?topic=watson-assistant-web-chat-security-enable).

With web chat security enabled, you can optionally implement additional security measures as needed:

- You can use JWTs to securely authenticate customers by user ID, which makes it possible for your assistant to control access to functions that require authorization.

    Without web chat security enabled, each customer who uses your assistant is identified only by the `user_id` property that is part of the message request. This is sufficient for identifying unique users for billing purposes, but it is not secure, because it could be modified.

    By encoding user identity information as part of the JWT payload, you can authenticate users securely. The JWT is signed and cannot be modified by the user.

    For more information about using JWTs for secure authentication, see [Authenticating users](/docs/watson-assistant?topic=watson-assistant-web-chat-security-authenticate).

- You can prevent unauthorized access to sensitive customer information by encrypting it and including it as part of the JWT user payload.

    The user payload is a part of the JWT you can use to send information you want your assistant to have access to, but you do not want customers to see. This information is stored only in private variables, which cannot be seen by customers and are never included in logs.

    For more information about using the user payload to protect sensitive information, see [Encrypting sensitive data](/docs/watson-assistant?topic=watson-assistant-web-chat-security-encrypt).

![development icon](images/development-icon.png) **Tutorial:** For a developer tutorial that shows an example of using web chat security to authenticate users and protect sensitive data, see [Tutorial: Authenticating a user in the middle of a session](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-security).

