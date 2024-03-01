---

copyright:
  years: 2023, 2024
lastupdated: "2024-02-29"

keywords: information gathering

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Information gathering
{: #information-gathering}

You can use watsonx.ai in your assistant to intelligently gather information and address a customer query quickly to avoid repetitive questions. The watsonx.ai uses large language models (LLMs) to recognize the information units in a query body and stores each of them in the respective slot, which is linked to a prompt. 

This beta feature is available in English for evaluation and testing purposes only. The watsonx generative AI model is currently hosted only in the Dallas and Frankfurt regions. To sign up for the beta access for Information Gathering, use the form [here](https://forms.monday.com/forms/5d57f5429e099cfe24462c277efdd058?r=use1){: external}.{: beta}

By enabling information gathering, your assistant can analyze a customer's free text response to:
- Gather accurate information
- Complete multiple steps in one step

For more information about collecting information from customer responses, see [Collecting information from your customers](/docs/watson-assistant?topic=watson-assistant-collect-info).

## Enabling information gathering capability
{: #enable-information-gathering}

To enable the information gathering capability, do the following steps:

1. Go to **Home** > **Actions** > **Global settings** > **Generative AI** > **Information gathering**.
1. Set **Use watsonx.ai information gathering** to `On`.

When you enable intelligent information gathering, settings for existing free text customer responses change to `Skip asking if the answer is mentioned in previous messages`. If you later disable information gathering, settings for free text responses revert to `Always ask`. For more information, see [Skipping steps, always asking steps, or never asking steps](/docs/watson-assistant?topic=watson-assistant-collect-info#collect-info-skip-step).{: tip}