---

copyright:
  years: 2023, 2024
lastupdated: "2024-04-03"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Google custom search extension setup
{: #search-extension-google}

You can access Google search through an extension to your assistant that uses the [Google Programmable Search Engine](https://developers.google.com/custom-search/docs/overview). It is a configurable search that you can customize based on your use case.

To set up the extension for Google search:

## Get Search Engine ID and API key
{: #search-extension-google-api-key}

Create a Google Programmable Search Engine. Then, get its Search Engine ID and an API key. For detailed instructions, see [Create Programmable Search Engine](https://developers.google.com/custom-search/v1/introduction#create_programmable_search_engine){: external} in the Google Programmable Search Engine documentation.

## Download the OpenAPI specification
{: #search-extension-google-open-api-specification}

Download the OpenAPI specification file: [google-custom-search-openapi.json](https://github.com/watson-developer-cloud/assistant-toolkit/blob/master/integrations/extensions/starter-kits/google-custom-search/basic/google-custom-search-openapi.json){: external}. You use this file to add the extension to your assistant.

The OpenAPI specification defines the following methods:

- `GET /customsearch/v1`: Search for content over the entire web.
- `GET /customsearch/v1/siterestrict`: Search for content over a specific collection of websites.

For more information about the endpoints, see [Custom Search](https://developers.google.com/custom-search/v1/reference/rest/v1/cse/list){: external} or [Custom Search Site Restricted](https://developers.google.com/custom-search/v1/reference/rest/v1/cse.siterestrict/list){: external}.

The endpoints have the same arguments and responses, but with differences:

- *Custom Search Site Restricted* is restricted to searching 10 or fewer websites, each of which can have an unlimited number of pages.
- *Custom Search* can support any number of websites that is indexed by Google, but has a [daily query limit](https://developers.google.com/custom-search/v1/overview#pricing).

For a typical assistant focused on a specific topic, it is usually only necessary to search a single website or a few websites. *Custom Search Site Restricted* is a better fit since it doesn't have a limit on the number of queries that can be run per day. Assistants that need to search more than 10 websites need to use *Custom Search* instead.

## Create and add extension
{: #search-extension-google-add-extension}

1.  In your assistant, on the **Integrations** page, click **Build custom extension** and use the OpenAPI specification file to build a custom extension. For general instructions on building any custom extension, see [Building a custom extension](/docs/watson-assistant?topic=watson-assistant-build-custom-extension).

1. After you build the Google custom search extension and it appears on your **Integrations** page, click **Add** to add it to your assistant. Use your Google programmable search engine API key to authenticate. For general instructions on adding any custom extension, see [Adding an extension to your assistant](/docs/watson-assistant?topic=watson-assistant-add-custom-extension).

## Add the Google custom search starter kit action template
{: #search-extension-google-template}

1. Open the **Actions** page.

1. If you have no actions, choose **Create a new action**. If you already have some actions, choose **New action**.

1. On **Create an action**, choose **Quick start with templates**.

   **Quick start with templates** is available in English-language assistants only.
   {: note}

1. On **Quick start with templates**, add the Google custom search starter kit.

## Edit system actions
{: #search-extension-google-set-by-assistant}

1. Click **Set by assistant** and open the **No matches** action.

1. Delete the two default steps. 

1. Add a step. Set **And then** to **Go to a subaction** and choose the **Google search** action.

1. If you aren't connecting your customers to a live agent, you might want to edit the **Fallback** action in the same way as **No matches**.

## Using your Google custom search extension
{: #search-extension-google-using}

Issue a query to your assistant. If no action that matches that query, then it uses Google to produce search results.

## Limit on search results size
{: #search-extension-google-limits}

{{site.data.keyword.conversationshort}} has a 100 kb limit on the size of information that is stored in context variables, which includes search results. If the results from your extension exceed that limit, the action can fail without any visible warning or error. Typically a long delay occurs and then there is no response. This failure rarely happens with the Google custom search extension, but it might happen if you are searching a site with large volumes of metadata that is returned by Google custom search. If you think that this might be a problem, try running the query in an API testing tool like curl, [Insomnia](https://insomnia.rest/), or [Postman](https://www.postman.com/). Check how many bytes of data you are getting as search results. If the total is at or near 100 kb, you might be able to work around the issue by reducing `num_of_results` and getting fewer results for each query or by excluding sites or pages with large volumes of metadata.

For more information, see [Limit on Size of Search Results](https://github.com/watson-developer-cloud/assistant-toolkit/blob/master/integrations/extensions/starter-kits/watson-discovery/README.md#limit-on-size-of-search-results){: external} in a starter kit for {{site.data.keyword.discoveryfull}}. 
