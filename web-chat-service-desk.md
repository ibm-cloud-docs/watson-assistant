---

copyright:
  years: 2019, 2023
lastupdated: "2023-08-18"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Adding contact center support
{: #deploy-web-chat-haa}

[IBM Cloud]{: tag-ibm-cloud}

You can configure the web chat to transfer a customer to a live agent if the customer asks for help from a person. The following service desk integrations are available for your assistant:

- [Genesys](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-deploy-genesys)
- [NICE CXone](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-deploy-nice-cxone)
- [Salesforce](/docs/watson-assistant?topic=watson-assistant-deploy-salesforce) {: #deploy-web-chat-salesforce}
- [Zendesk](/docs/watson-assistant?topic=watson-assistant-deploy-zendesk) {: #deploy-web-chat-zendesk}


## Contact center starter kits
{: #deploy-web-chat-haa-starter-kits}

If you are comfortable writing code, you can use starter kits to integrate with service desk platforms, or to develop an integration with the service desk platform of your choice.

The starter kits are available from a [GitHub repo](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter){: external}. Fully functional reference implementations are provided for the following contact center platforms:

- [eGain Advisor Desktop](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter/tree/main/src/egain/webChat){: external}
- [Enghouse Interactive CCaaS](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter/tree/main/src/enghouse){: external}
- [Genesys Cloud](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter/tree/main/src/genesys/webChat){: external}
- [Kustomer](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter/tree/main/src/kustomer/webChat){: external}
- [NICE inContact](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter/tree/main/src/incontact/webChat){: external}
- [Oracle Cloud B2C](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter/tree/main/src/oracle/webChat){: external}
- [Twilio Flex](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter/tree/main/src/flex/webChat){: external}
- [Bring your own (starter kit)](https://github.com/watson-developer-cloud/assistant-web-chat-service-desk-starter){: external}

The starter kit reference implementations, while functional, are examples only, and are not vetted for production use. You should perform robust testing before deploying integrations in production.
{: important}

After you set up a service desk integration, you must update your actions to ensure they understand user requests to speak to someone and can transfer the conversation properly.


