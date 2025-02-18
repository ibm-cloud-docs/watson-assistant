
---

copyright:
  years: 2025
lastupdated: "2025-02-18"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Configuring Base LLM
{: #base-llm-wxa}

 {{site.data.keyword.conversationshort}} includes a range of pre-built AI models and algorithms that can be used to generate text, images, and other types of content. These models can be customized and combined in various ways to create more sophisticated and powerful generative AI applications.

The **Base large language model (LLM)** section in the **Generative AI** page helps you to configure large language models for your assistants. The LLMs enable your customers to interact with the assistants seamlessly without any custom-built conversational steps. You can enable the Base LLM features for the existing actions in your assistants that improve their conversation capability. 

You can do the following actions in the Base LLM configuration:

## Selecting a large language model for your assistant
{: #base-llm-select-model}

To select the LLM that suits your enterprise ecosystem, do the following steps:

1. Go to **Home** > **Generative AI**.

1. In the **Base large language model (LLM)** section, select the large language model from the **Select a model** dropdown. 

{{site.data.content.llm-description-table-reuse}}

## Adding prompt instructions
{: #base-llm-add-prompt-instructions}

You can instruct the LLM in your assistant to give refined responses by adding prompt instructions. The prompt instructions help LLMs to guide the conversations with clarity and specificity to achieve the end goal of an action. Follow these steps to add the prompt instruction:

1. Go to **Home** > **Generative AI**.

1. In the **Add prompt instructions** section, click **Add instructions** to see the **Prompt instruction** field. 

1. Enter the prompt instructions in the **Prompt instruction** field.

   The maximum number of characters that you can enter in the **Prompt instruction** field is 1,000.
   
## Selecting the answering behavior of your assistant
{: #base-llm-select-answer-behavior}

You can configure the answering behavior of your assistant to provide responses that are based on the preloaded content. The answering behavior that you can configure is:

- **Conversational search** 

Only Plus or Enterprise plans support Conversational search. Starting from June 1, 2024, add-on charges are applicable for using the Conversational search feature in addition to your Plus or Enterprise plans. For more information about the pricing plans, see [Pricing plans](https://cloud.ibm.com/catalog/services/watsonx-assistant?catalog_query=aHR0cHM6Ly9jbG91ZC5pYm0uY29tL2NhdGFsb2c%2Fc2VhcmNoPXdhdHNvbnglMjUyMGFzc2lzdGFudCNzZWFyY2hfcmVzdWx0cw%3D%3D&planId=f0a3dd47-b693-4d73-a8df-aa6baf07a933){: external}. For more information about terms, see [Terms](https://www.ibm.com/support/customer/csol/terms/?id=i128-0038&lc=en){: external}.
{: important}
  
In conversational search, the LLM uses content that is preloaded during the [search integration](/docs/watson-assistant?topic=watson-assistant-search-overview) to respond to customer queries. 
  
To use the conversational search, you must configure [search integration](/docs/watson-assistant?topic=watson-assistant-search-overview) and enable [conversational search](/docs/watson-assistant?topic=watson-assistant-conversational-search).{: note}

To use conversational search in any language other than English, you can change from the default model (Granite) to other model. You can test to verify that you are getting reasonable results in your language that can include Spanish, Brazilian Portuguese, French, or German.


