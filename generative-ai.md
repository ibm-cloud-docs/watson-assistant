---

copyright:
  years: 2015, 2024
lastupdated: "2024-01-29"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Using watsonx.ai for generative AI capabilities
{: using-watsonxai-for-generative-ai-capabilities}

[Beta]{: tag-cyan}

By enabling watsonx.ai, you bring the generative AI capabilities in your assistants to give quick, accurate, and intelligent responses to the customer queries. In addition, the Large Language Models (LLMs) help your assistant to recognize customer conversation and respond to queries by using clear and concise conversation. For more information, see [Conversational search](/docs/watson-assistant?topic=watson-assistant-conversational-search)

This beta feature is available in English for evaluation and testing purposes only. The watsonx generative AI model is currently hosted only in the Dallas and Frankfurt regions. To sign up for the beta access, use the [form here](https://form.asana.com/?k=xflsi8sU1akW_LI3ZXdStA&d=8612789739828).{: beta}

By default, assistants in all regions except `Frankfurt` use the model from the `Dallas` region. {: important}
You can configure and manage the following two capabilities of generative AI in your assistants:

- [Information gathering](#information-gathering)
- [Conversational search](#conversational-search)

## Information gathering
{: #information-gathering}

You can use watsonx.ai in your assistant to intelligently gather information and address a customer query quickly to avoid repetitive questions. The watsonx.ai uses large language models (LLMs) to recognize the information units in a query body and stores each of them in the respective slot, which is linked to a prompt. 

By enabling information gathering, your assistant can analyze a customer's free text response to:
- Gather accurate information
- Complete multiple steps in one step

For more information about collecting information from customer responses, see [Collecting information from your customers](/docs/watson-assistant?topic=watson-assistant-collect-info).

### Enabling information gathering capability
{: #enable-information-gathering}

To enable the information gathering capability, do the following steps:

1. Go to **Home** > **Actions** > **Global settings** > **Generative AI** > **Information gathering**.
1. Set **Use watsonx.ai information gathering** to `On`.

When you enable intelligent information gathering, settings for existing free text customer responses change to `Skip asking if the answer is mentioned in previous messages`. If you later disable information gathering, settings for free text responses revert to `Always ask`. For more information, see [Skipping steps, always asking steps, or never asking steps](/docs/watson-assistant?topic=watson-assistant-collect-info#collect-info-skip-step).{: tip}



## Conversational search
{: #conversational-search}

Use *conversational search* with the {{site.data.keyword.discoveryfull}} or Elasticsearch search integration to help your assistant extract an answer from the highest-ranked query results and return a text response to the user.
{: shortdesc}

When you enable this feature, search results are provided to an IBM watsonx generative AI model that produces a conversational reply to a user's question. For more information, see [Conversational search](/docs/watson-assistant?topic=watson-assistant-conversational-search).

