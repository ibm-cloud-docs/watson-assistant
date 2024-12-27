---

copyright:
  years: 2023, 2024
lastupdated: "2024-12-27"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# NeuralSeek extension setup
{: #search-extension-neuralseek}

[NeuralSeek](https://neuralseek.com){: external} by [Cerebral Blue](https://cerebralblue.com/){: external} is a combined search and natural-language generation system that is designed to [make conversational AI feel more conversational](https://garrettrowe.medium.com/making-conversational-ai-feel-more-conversational-8748009b3fda){: external}. It requires that you load all your content into [{{site.data.keyword.discoveryfull}}](/catalog/services/watson-discovery){: external}. Then, when a user asks a question, it has {{site.data.keyword.discoveryshort}} search for multiple relevant documents and then it generates a natural-language answer that uses the contents of those documents. In some cases, the answer might be taken directly from a single document, and in others, the answer can include information from multiple sources that are combined into a single coherent statement. For each query, NeuralSeek returns a single answer and a confidence score. In most cases, it also returns a URL of a document that influenced the answer, which might be one of several documents.

To set up the extension for NeuralSeek search:

## Set up {{site.data.keyword.discoveryfull}}
{: #search-extension-neuralseek-discovery}

1. You need an instance of [{{site.data.keyword.discoveryfull}}](/catalog/services/watson-discovery){: external}. Because NeuralSeek can modify your data as needed to make it more effective, make sure it is not an instance with important data that you are using for other purposes.

1. In {{site.data.keyword.discoveryshort}}, create a project and load the documents that you want to use.

## Get the NeuralSeek OpenAPI specification and API Key
{: #search-extension-neuralseek-api-key}

1. You also need an instance of [NeuralSeek on IBM Cloud](/catalog/services/neuralseek){: external}.

1. In NeuralSeek, open the **Configure** page and enter your information in the **Discovery instance details** section.

1. On the **Integrate** page, and click the **OpenAPI file** link to download the `NeuralSeek.json` OpenAPI specification file configured for your instance.

1. Also on the **Integrate** page, copy the API key for NeuralSeek. The API key for NeuralSeek is not the same as the API key for {{site.data.keyword.discoveryshort}} that you used on the **Configure** page. The API key for NeuralSeek is only available on the **Integrate** page.

Simple instructions for setting up NeuralSeek are available on the **Integrate** page. You can also follow those instructions to get NeuralSeek working with {{site.data.keyword.conversationshort}}.
{: note}

## Create and add extension
{: #search-extension-neuralseek-add-extension}

1. In your assistant, on the **Integrations** page, click **Build custom extension** and use the OpenAPI specification file to build a custom extension. For general instructions on building any custom extension, see [Building a custom extension](/docs/watson-assistant?topic=watson-assistant-build-custom-extension).

1. After you build the NeuralSeek extension and it appears on your **Integrations** page, click **Add** to add it to your assistant. Use your NeuralSeek API key to authenticate. For general instructions on adding any custom extension, see [Adding an extension to your assistant](/docs/watson-assistant?topic=watson-assistant-add-custom-extension).

## Add the NeuralSeek starter kit action template
{: #search-extension-neuralseek-template}

1. Open the **Actions** page.

1. If you have no actions, choose **Create a new action**. If you already have some actions, choose **New action**.

1. On **Create an action**, choose **Quick start with templates**.

   **Quick start with templates** is available in English-language assistants only.
   {: note}

1. On **Quick start with templates**, add the NeuralSeek search starter kit.

## Edit system actions
{: #search-extension-neuralseek-set-by-assistant}

1. Click **Set by assistant** and open the **No matches** action.

1. Delete the two default steps.

1. Add a step. Set **And then** to **Go to a subaction** and choose the **NeuralSeek search** action.

1. If you aren't connecting your customers to a live agent, you might want to edit the **Fallback** action in the same way as **No matches**.

## Using your NeuralSeek extension
{: #search-extension-neuralseek-using}

Issue a query to your assistant. If no action that matches that query, then it uses NeuralSeek to produce search results.

For many use cases, NeuralSeek alone is enough to deploy an assistant. If you are happy with your assistant, you might want to deploy it for real-world use right away. Use the **Analyze** page in {{site.data.keyword.conversationshort}} or the **Curate** page in NeuralSeek to see what kinds of questions users are asking and actions for the common user requests. The **Curate** page can automate the creation of new actions and generate new example utterances that trigger those actions. It can also merge any existing actions with the actions that it generates so you can update an existing assistant. For more information, see the [NeuralSeek documentation](https://documentation.neuralseek.com/){: external}
