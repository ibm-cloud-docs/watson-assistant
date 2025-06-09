---

copyright:
  years: 2025
lastupdated: "2025-06-09"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Supported foundation models
{: #supported-foundation-models}

{{site.data.keyword.conversationfull}} supports a diverse range of AI models for the capabilities within the product. For each model listed, you can learn more about their details so you can choose the model that fits your business needs.
{: shortdesc}

Each model contains the reference for its **Model card** where you can get more information about technical specifications of the model.

Find information such as the supported languages, latest updates, and training data for the models available in their model card.

## Foundation model lifecycle
{: #foundation-model-lifecycle}

As new versions of IBM foundation models are introduced, older versions are deprecated. Similarly, as newer and more effective models from other providers become available, less useful models are removed.

For more information on deprecated or withdrawn models, see [Deprecated or withdrawn models](/docs/watson-assistant?topic=watson-assistant-deprecated-llm-models).

## `granite-13b-chat-v2`
{: #granite-13b-chat-v2}

[Withdrawn]{: tag-cool-gray}

The Granite 13 Billion chat V2 (`granite-13b-chat-v2`) model is the chat-focused variant initialized from the pre-trained Granite Base 13 Billion Base V2 (`granite-13b-base-v2`) model. `granite-13b-base-v2` has been trained using over 2.5T tokens. IBM Generative AI Large Language Foundation Models are Enterprise-level English-language models trained with a large volume of data that has been subjected to intensive pre-processing and careful analysis.

**Usage**:
- Question answering
- Summarization
- Retrieval-Augmented Generation
- Classification
- Generation
- Extraction

**Components that use this model**:  
- [Base LLM](/docs/watson-assistant?topic=watson-assistant-base-llm-wxa).

**Model card**: [ibm/granite-13b-chat-v2](https://dataplatform.cloud.ibm.com/wx/samples/models/ibm/granite-13b-chat-v2){: external}



## `granite-13b-instruct-v2`
{: #granite-13b-instruct-v2}

IBM Generative AI Large Language Foundation Models are Enterprise-level English-language models trained with a large volume of data that has been subjected to intensive pre-processing and careful analysis. The Granite 13 Billion Instruct V2.0 (granite.13b.instruct.v2) model is the instruction-tuned variant initialized from the pre-trained Granite Base 13 Billion Base V2.0 (granite.13b.base.v2) model. granite.13b.base.v2 is trained using over 2.5T tokens. The Granite family of models support all 5 language tasks (Q&A, Generate, Extract, Summarize, and Classify).

**Usage**:
- Question answering
- Summarization
- Retrieval-Augmented Generation
- Classification
- Generation
- Extraction

**Components that use this model**:  
- [Base LLM](/docs/watson-assistant?topic=watson-assistant-base-llm-wxa)

**Model card**: [ibm/granite-13b-instruct-v2](https://dataplatform.cloud.ibm.com/wx/samples/models/ibm/granite-13b-instruct-v2){: external}

## `granite-3-8b-instruct`
{: #granite-3-8b-instruct}

Granite-3.0-8B-Instruct is a 8B parameter model finetuned from Granite-3.0-8B-Base using a combination of open source instruction datasets with permissive license and internally collected synthetic datasets. The model is designed to respond to general instructions and can be used to build assistants for multiple domains, including business applications.

**Usage**:
- Question answering
- Summarization
- Classification
- Generation
- Extraction
- Function calling

**Components that use this model**:  

- [Base LLM](/docs/watson-assistant?topic=watson-assistant-base-llm-wxa)

**Model card**: [ibm/granite-3-8b-instruct](https://dataplatform.cloud.ibm.com/wx/samples/models/ibm/granite-3-8b-instruct){: external}

## `granite-3-2b-instruct`
{: #granite-3-2b-instruct}

Granite-3.0-2B-Instruct is a lightweight and open-source 2B parameter model fine tuned from Granite-3.0-2B-Base on a combination of open-source and proprietary instruction data with permissive license. The model is designed to respond to general instructions and can be used to build assistants for multiple domains, including business applications.

**Usage**:
- Question answering
- Summarization
- Classification
- Generation
- Extraction
- Function calling

**Components that use this model**:  

- [Base LLM](/docs/watson-assistant?topic=watson-assistant-base-llm-wxa)

**Model card**: [ibm/granite-3-2b-instruct](https://dataplatform.cloud.ibm.com/wx/samples/models/ibm/granite-3-2b-instruct){: external}
