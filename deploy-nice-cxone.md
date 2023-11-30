---

copyright:
  years: 2023
lastupdated: "2023-11-30"

subcollection: watson-assistant

---
{{site.data.keyword.attribute-definition-list}}


# Integrating with NICE CXone
{: #deploy-nice-cxone}

[IBM Cloud]{: tag-ibm-cloud}



Integrate web chat with a NICE CXone service desk solution and empower your live agents to provide faster solutions and better customer service.
{: shortdesc}

Connect NICE CXone to your AI-powered assistant with a web chat integration, and personalize the experience as necessary. If, in the course of conversation with your assistant, a customer requests contact with someone, you can transfer or escalate directly to a live agent.

NICE CXone allows your team to assist customers in real time, which increases customer satisfaction. And satisfied customers are happier customers. To learn more about this service desk solution, see the [NICE website](https://www.nice.com/solutions/omnichannel-customer-service){: external}.

## Before you begin
{: #deploy-nice-cxone-prereqs}

You need to sign up for a NICE CXone account, or have an existing one, and [contact the NICE CXone team](https://www.nice.com/contact-us) to access and use Digital First Omnichannel (DFO) Live Chat.

An OAuth provider is required, if only allowing [authenticated users](#deploy-nice-cxone-authenticate).

The {{site.data.keyword.conversationshort}} web chat integration only supports NICE CXone DFO Live Chat, not the older NICE CXone chat channel integration. 
{: note} 

## Setting up NICE CXone with your assistant
{: #deploy-nice-cxone-setup}

Web chat has a built-in integration to the NICE CXone DFO live messaging channel and currently only supports client-side configuration. It is not configurable from the {{site.data.keyword.conversationshort}} user interface (UI).

### Configure DFO Live Chat
{: #deploy-nice-cxone-configuration}

To set up one or more live chat channels to integrate with your assistant, see NICE CXone instructions at [Set Up Digital First Omnichannel Live Chat](https://help.nice-incontact.com/content/acd/digital/chat/setuplivechat.htm).

### Enable the integration in web chat 
{: #deploy-nice-cxone-integration}

1. Have ready the **DFO channel ID, brand ID, and environment**, all values found in the embed code provided by NICE CXone.

1. Use the script at [Enabling the integration](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=service-desks-nice#enabling){: external}.

### Enable authenticated users
{: #deploy-nice-cxone-authenticate}

To configure your integration to only allow authenticated users, see [Authenticated users](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=service-desks-nice#authenticated-users){: external}.


