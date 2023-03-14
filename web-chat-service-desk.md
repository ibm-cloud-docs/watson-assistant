---

copyright:
  years: 2019, 2023
lastupdated: "2023-03-14"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Adding contact center support
{: #deploy-web-chat-haa}

[IBM Cloud]{: tag-ibm-cloud}

You can configure the web chat to transfer a customer to a human customer support agent if the customer asks for help from a person. The following built-in contact center (service desk) integrations are available:

- [Zendesk](/docs/watson-assistant?topic=watson-assistant-deploy-zendesk) {: #deploy-web-chat-zendesk}
- [Salesforce](/docs/watson-assistant?topic=watson-assistant-deploy-salesforce) {: #deploy-web-chat-salesforce}

## Contact center starter kits
{: #deploy-web-chat-haa-starter-kits}

If you are comfortable writing code, you can use the contact center starter kits to integrate with additional contact center platforms, or to develop your own integration with the contact center platform of your choice.

The starter kits are available from a [GitHub repo](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter){: external}. Fully functional reference implementations are provided for the following contact center platforms:

- [Genesys Cloud](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter/tree/main/src/genesys/webChat){: external}
- [NICE inContact](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter/tree/main/src/incontact/webChat){: external}
- [Twilio Flex](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter/tree/main/src/flex/webChat){: external}
- [Kustomer](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter/tree/main/src/kustomer/webChat){: external}
- [eGain Advisor Desktop](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter/tree/main/src/egain/webChat){: external}
- [Enghouse Interactive CCaaS](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter/tree/main/src/enghouse){: external}
- [Bring your own (starter kit)](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter){: external}

The starter kit reference implementations, while functional, are examples only, and have not been vetted for production use. You should perform robust testing before deploying these integrations in production.
{: important}

After you set up a contact center integration, you must update your actions to ensure they understand user requests to speak to someone and can transfer the conversation properly.


