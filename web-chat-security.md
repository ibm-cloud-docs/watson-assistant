---

copyright:
  years: 2019, 2022
lastupdated: "2022-11-01"

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

# Overview: Securing the web chat
{: #web-chat-security}

If you enable security, you can configure the web chat to authenticate users, protect private data, and restrict access to your assistant.
{: shortdesc}

## When to enable web chat security
{: #web-chat-security-overview}

All messages that are sent between the web chat and the assistant are encrypted using Transport Layer Security (TLS), which protects sensitive data as it travels through the network. However, there are still potential security exposures that you might need to protect against. By enabling the web chat security feature and updating your website code appropriately, you can add the following protections:

- You can prevent unauthorized websites from sending messages to your assistant, even if they copy your web chat embed script.

- You can securely authenticate customers in order to control access to features of your assistant that require authorization.

- You can encrypt sensistive data so that customers cannot see it, while still allowing your assistant to access it.

Web chat security uses JSON Web Tokens (JWTs), which are data objects that are sent with each message from your website to the {{site.data.keyword.conversationshort}} service. Because a JWT is digitally signed using a private encryption key that only you have, it ensures that each message originates with your website. The JWT payload can also be used to securely authenticate users and carry encrypted private data.

For detailed information about JSON Web Tokens, see the [JWT specification](https://tools.ietf.org/html/rfc7519){: external}).
{: tip}

## Steps for enabling web chat security
{: #web-chat-security-steps }

Implementing web chat security requires that a developer make changes to your website code. At a high level, the process of enabling security is as follows:

1. In your web application code, implement a function that generates a JWT signed with your private encryption key.

1. In the web chat embed script on your website, use the web chat API to specify the generated JWT so it is included with all messages sent to the assistant.

1. Enable security in the web chat security settings and specify your public encryption key, which the web chat integration will use to verify that messages it receives were signed with your private key.

    After you enable web chat security, any message received by the web chat integration that is not accompanied by a properly signed JWT will be rejected.
    {: important}

For detailed information about how to complete these steps, see [Enabling web chat security](/docs/watson-assistant?topic=watson-assistant-web-chat-security-enable).

With web chat security enabled, you can optionally implement additional security measures as needed:

- You can use JWTs to securely [authenticate customers](#web-chat-security-authenticate) by user ID, which makes it possible for your assistant to control access to functions that require authorization.

    Without web chat security enabled, each customer who uses your assistant is identified only by the `user_id` property that is part of the message request. This is sufficient for identifying unique users for billing purposes, but it is not secure, because it could be modified.

    By encoding user identity information as part of the JWT payload, you can authenticate users securely. The JWT payload is encrypted and cannot be accessed or modified by the user.

    For more information about using JWTs for secure authentication, see [Authenticating users](/docs/watson-assistant?topic=watson-assistant-web-chat-security-authenticate).

- You can [prevent unauthorized access](#web-chat-security-encrypt) to sensitive customer information by encrypting it and including it as part of the JWT user payload.

    The user payload is a part of the JWT you can use to send information you want your assistant to have access to, but that you do not want customers to see. This information is stored only in private variables, which cannot be seen by customers and are never included in logs.

    For more information about using the user payload to protect sensitive information, see [Encrypting sensitive data](/docs/watson-assistant?topic=watson-assistant-web-chat-security-encrypt).

![development icon](images/development-icon.png) **Tutorial:** For a developer tutorial that shows an example of using web chat security to authenticate users and protect sensitive data, see [Tutorial: Authenticating a user in the middle of a session](/docs/watson-assistant?topic=watson-assistant-web-chat-develop-security).

## Reviewing security
{: #web-chat-security-review}

The web chat integration undergoes tests and scans on a regular basis to find and address potential security issues, such as cross-site scripting (XSS) vulnerabilities.

Be sure to run your own security reviews to see how the web chat fits in with your current website structure and policies. The web chat is hosted on your site and can inherit any vulnerabilities that your site has. Only serve content over HTTPS, use a Content Security Policy (CSP), and implement other basic web security precautions.
