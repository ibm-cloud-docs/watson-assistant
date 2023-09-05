---

copyright:
  years: 2023
lastupdated: "2023-09-05"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Coveo search extension setup
{: #search-extension-coveo}

You can use [Coveo](https://www.coveo.com){: external} to create and manage source documents. The [Coveo Search API](https://docs.coveo.com/en/52/build-a-search-ui/use-the-search-api){: external} can issue search queries on an index. It is a configurable search that you can customize based on your use case. You can access Coveo search through an extension to your assistant.

To set up the extension for Coveo search:

## Add an API key
{: #search-extension-coveo-api-key}

In the Coveo Administration Console, add an API key. For detailed instructions, see [Add an API Key](https://docs.coveo.com/en/1718/manage-an-organization/manage-api-keys#add-an-api-key){: external} in the Coveo documentation. Ensure that the API key is set to enable search and to allow `Execute queries`. 

## Download the OpenAPI specification
{: #search-extension-coveo-open-api-specification}

Download the OpenAPI specification file: [coveo.openapi.json](https://github.com/watson-developer-cloud/assistant-toolkit/blob/master/integrations/extensions/starter-kits/coveo/coveo.openapi.json){: external}. Use this file to add the extension to your assistant.

The OpenAPI specification defines the following method:

- `GET /rest/search/v2`: Search for content in a set of sources or documents.

For more information about the endpoints, see [Perform a Query](https://docs.coveo.com/en/1445/build-a-search-ui/perform-a-query){: external} in the Coveo documentation.

## Create and add the extension
{: #search-extension-coveo-add-extension}

1. In your assistant, on the **Integrations** page, click **Build custom extension** and use the OpenAPI specification file to build a custom extension. For general instructions on building any custom extension, see [Building the custom extension](/docs/watson-assistant?topic=watson-assistant-build-custom-extension#building-the-custom-extension).

1. After you build the Coveo extension, and it appears on your **Integrations** page, click **Add** to add it to your assistant. Use your Coveo API key to authenticate. For general instructions on adding any custom extension, see [Adding an extension to your assistant](/docs/watson-assistant?topic=watson-assistant-add-custom-extension).

## Add the Coveo search starter kit action template
{: #search-extension-coveo-template}

1. Open the **Actions** page.

1. If you have no actions, select **Create a new action**. If you already have some actions, select **New action**.

1. On **Create an action**, select **Quick start with templates**.

   **Quick start with templates** is available in English-language assistants only.
   {: note}

1. On **Quick start with templates**, add the Coveo search starter kit.

## Edit system actions
{: #search-extension-coveo-set-by-assistant}

1. Click **Set by assistant** and open the **No action matches** action.

1. Delete the two default steps.  

1. Add a step. Set **And then** to **Go to a subaction**, and select the **Coveo search** action.

1. If you are not connecting your customers to a live agent, you might want to edit the **Fallback** action in the same way as **No action matches**.

## Using your Coveo search extension
{: #search-extension-coveo-using}

Issue a query to your assistant. If no action matches that query, then it uses Coveo to produce search results.
