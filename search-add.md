---

copyright:
  years: 2021, 2024
lastupdated: "2024-04-25"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.discoveryfull}} search integration setup 
{: #search-add}

[Plus]{: tag-green}

This feature is currently not available in the AI assistant builder of IBM watsonx Orchestrate.{: note}

The search integration searches for information from a data collection that you create by using the {{site.data.keyword.discoveryshort}} service.

{{site.data.keyword.discoveryshort}} is a service that crawls, converts, and normalizes your unstructured data. The product applies data analysis and cognitive intuition to enrich your data such that you can more easily find and retrieve meaningful information from it later. To read more about {{site.data.keyword.discoveryshort}}, see the [product documentation](/docs/discovery-data?topic=discovery-data-about){: external}.

The search integration requires {{site.data.keyword.discoveryshort}} v2. For more information, see [Getting the most from {{site.data.keyword.discoveryshort}}](/docs/discovery-data?topic=discovery-data-version-choose){: external}.
{: important}

Typically, the type of data collection you add to {{site.data.keyword.discoveryshort}} and access from your assistant contains information that is owned by your company. This proprietary information can include FAQs, sales collateral, technical manuals, or papers written by subject matter experts. Mine this dense collection of proprietary information to find answers to customer questions quickly.

Watch a 4-minute video that provides an overview of the search integration:

![Search Integration: {{site.data.keyword.conversationshort}}](https://video.ibm.com/embed/channel/23952663/video/wa-search){: video output="iframe" data-script="none" id="watsonmediaplayer" width="480" height="270" scrolling="no" allowfullscreen webkitallowfullscreen mozAllowFullScreen frameborder="0" style="border: 0 none transparent;"}

## Before you begin
{: #search-add-prereqs}

Before you begin, you must: 
- Set up a {{site.data.keyword.discoveryshort}} v2 instance on {{site.data.keyword.cloud_notm}} or installed on {{site.data.keyword.icp4dfull_notm}}. 
- Have at least a Plus plan {{site.data.keyword.discoveryshort}} service instance for {{site.data.keyword.cloud_notm}}. Go to the [{{site.data.keyword.discoveryshort}}](/catalog/services/watson-discovery){: external} page in the {{site.data.keyword.cloud_notm}} catalog and create a Plus plan service instance.
- Use public endpoints. Private endpoints are currently not supported for {{site.data.keyword.conversationshort}} or the classic experience.

## Create the search integration or search skill
{: #search-add-task}

To create a search integration:

1.  From the assistant where you want to add search, click **Integrations**.

    You can add search if you are a user with a paid plan.
    {: note}

1.  In the **Extensions** section, locate Search, click **Add**, then click **Confirm**.

If you are using the classic experience, add a search skill:

1.  From the assistant where you want to add the skill, click **Add search skill**.

1.  Take one of the following actions:

    - To create a new search skill, stay on the *Create skill* tab.

    - If you have created a search skill already, the *Add existing skill* tab is displayed, and you can click to add an existing skill.

1.  Specify the details for the new skill:
    - **Name**: A name no more than 64 characters in length. A name is required.
    - **Description**: An optional description no more than 128 characters in length.

## Connect to an existing {{site.data.keyword.discoveryshort}} instance
{: #search-add-connect-discovery}

1.  Choose the {{site.data.keyword.discoveryshort}} service instance that you want to extract information from.
{: #choose-d-instance}

    If you see a warning that some of your {{site.data.keyword.discoveryshort}} service instances do not have credentials set, it means that you can access at least one instance that you never opened from the {{site.data.keyword.cloud_notm}} dashboard. You must access a service instance for credentials to be created for it, and credentials must exist before {{site.data.keyword.conversationshort}} can establish a connection to the {{site.data.keyword.discoveryshort}} service instance on your behalf. If you think a {{site.data.keyword.discoveryshort}} service instance is missing from the list, open the instance from the {{site.data.keyword.cloud}} dashboard directly to generate credentials for it.
    {: note}

1.  Indicate the data collection to use, by doing one of the following things:
{: #pick-data-collection}

    - Choose an existing project.

      You can click the *Open {{site.data.keyword.discoveryshort}}* icon to review the configuration of a project before you decide which one to use.

      Go to [Configure the search](#search-add-configure).

    - If you do not have a project or do not want to use any of the projects that are listed, click **Create a new project** to add one. Follow the steps in [Create a project](#search-add-create-discovery-collection).

      **Create a new project** is not displayed if you reached the limits based on your {{site.data.keyword.discoveryshort}} service plan. See [{{site.data.keyword.discoveryshort}} pricing plans](/docs/discovery-data?topic=discovery-data-pricing-plans){: external} for plan limit details.
      {: note}

## Create a project
{: #search-add-create-discovery-collection}

1.  On the **OK, where is your data?** page, select your data source, then click **Next**. Example choices include Salesforce, SharePoint, Box, IBM Cloud Object Storage, web crawl, and upload data. 

1. On the **Let's create a collection for your data** pages, enter the information on how to connect to your data and configure your collection. The information that you need to enter is different depending on the data source. For example, you need to enter your authentication credentials for services such as Salesforce, Sharepoint, and Box. For web crawl, you specify the website with your existing information.

1. Click **Finish**. Give {{site.data.keyword.discoveryshort}} a few minutes to start creating documents. You can use the **Manage collections** page within the project to see the progress.

1.  Wait for the collection to be fully ingested, then click **Back to {{site.data.keyword.conversationshort}}**.

## Configure the search
{: #search-add-configure}

1.  On the {{site.data.keyword.conversationshort}} search integration page, verify that the {{site.data.keyword.discoveryshort}} instance and project you want to use is selected, then click **Next**.

1.  In the **Configure result content** section, review the {{site.data.keyword.discoveryshort}} fields and examples that are used in the search results shown to your customers. You can accept the defaults, or customize them as you want.

    The appropriate collection fields to extract data from vary depending on your collection's data source and how the data source was enriched. After you choose a data collection type, the collection field values are prepopulated with source fields that are considered most likely to contain useful information given the collection's data source type. However, you know your data better than anyone. You can change the source fields to ones that contain the best information to meet your needs.

     To learn more about the structure of the documents in your collection, including the names of fields that contain information you might want to extract, open the collection in {{site.data.keyword.discoveryshort}}, and then use the **Identity fields** and **Manage fields** tabs.

    Each search result can consist of the following sections:

    - **Title**: Search result title. Use the title, name, or similar type of field from the collection as the search result title.

      You must select something for the title or no search result response is displayed in the Facebook and Slack integrations.

    - **Body**: Search result description. Use an abstract, summary, or highlight field from the collection as the search result body.

       You must select something for the body or no search result response is displayed in the Facebook and Slack integrations.

    - **URL**: This field can be populated with any footer content that you want to include at the end of the search result.

       For example, you might want to include a hypertext link to the original data object in its data source. Most online data sources provide self-referencing public URLs for objects in the store to support direct access. If you add a URL, it must be valid and reachable. If it is not, the Slack integration doesn't include the URL in its response, and the Facebook integration doesn't return any response.

       The Facebook and Slack integrations can successfully display the search result response when the URL field is empty.
  
    You must use a field for at least one of the search results.
    {: important}

    If no options are available from the drop-down fields, give {{site.data.keyword.discoveryshort}} more time to finish creating the collection. If the collection is not created, then your collection might not contain any documents or might have ingestion errors that you need to address first.

    ![Shows that the Title, Shortdesc, and url fields are selected and the preview search card is populated with information from those fields](images/search-configure-fields.png)

    As you add field mappings, a preview of the search result is displayed with information from the corresponding fields of your data collection. This preview shows you what gets included in the search result response that is returned to users.

    To get help with configuring the search, see [Troubleshooting](#search-add-troubleshoot).

1.  Use the **Message**, **No results found** and **Connectivity issue** tabs to customize different messages to share with users based on the successfulness of the search.

    | Tab | Scenario | Example message |
    | --- | --- | --- |
    | Message | Search results are returned | `I found this information that might be helpful:` |
    | No results found | No search results are found | `I searched my knowledge base for information that might address your query, but did not find anything useful to share.` |
    | Connectivity issue | I was unable to complete the search for some reason | `I might have information that could help address your query, but am unable to search my knowledge base at the moment.` |
    {: caption="Search result messages" caption-side="top"}

1.  Choose whether to enable **Emphasize the answer**. 

    This option is available only if your {{site.data.keyword.discoveryshort}} instance uses the v2 {{site.data.keyword.discoveryshort}} API.
    {: note}

    When you enable this feature, the sentence that is determined by {{site.data.keyword.discoveryshort}} to be the exact answer to the customer's question is highlighted in the block of text that is displayed to the customer as the search result.

1.  In the **Adjust result quantity** section, specify the number of results to return.

    The top three results are returned automatically. You can choose to show fewer or more (up to 10) results in the response.

    By default, customers can choose to see more results. If you don't want to give customers this choice, clear the **Include link for customers to view up to 10 results** checkbox.

1.  In the **Set result selectivity** section, decide whether to be more selective with the answers that are returned. By increasing result selectivity, Search returns fewer but more accurate results. In most cases, Search is accurate enough that the default setting (off) is sufficient.

1.  Use **Custom results filter** to add a filter for the custom text strings in the search integration. The **Custom results filter** field helps you define the search results relevant for a topic, product, or text string. For example, if you define the **Custom results filter** field by sing `enriched_text.entities.text:"Boston, MA"`, the search responses for any query in the assistant are filtered to make it relevant to `"Boston, MA"` in the `enriched_text.entities.text` file.

    ![Custom results filter](/images/custom-result-filter-wd.png)

1.  Click **Preview**. Enter a test message to see the results that are returned when your configuration choices are applied to the search. Make adjustments as necessary.

1.  Click **Create**.

## Edit the search integration configuration
{: #search-edit-config}

If you want to change the configuration of the search result card later, open the search integration again, and make edits. You do not need to save changes as you make them; they are automatically applied. When you are happy with the search results, click **Save** to finish configuring the search integration.

If you decide you want to connect to a different {{site.data.keyword.discoveryshort}} service instance or project, open the search integration and click **Edit Discovery Settings**. You can choose either a new project from the same instance, or a new instance and project.

 ## Configure your assistant to use {{site.data.keyword.discoveryshort}} search
 {: #search-assistant-configure}

After you configure {{site.data.keyword.discoveryshort}} search integration, you must configure your assistant to use {{site.data.keyword.discoveryshort}} search when the customer response matches no action. For more information about updating **No matches** to use search, see [Use search when no action matches](/docs/watson-assistant?topic=watson-assistant-search-integration-enhancement#search-no-action-matches). 

## Troubleshooting
{: #search-add-troubleshoot}

Review this information for help with common tasks.

- **Creating a web crawl data collection**: Things to know when you create a web crawl data source:

    - To increase the number of documents that are available to the data collection, click add a URL group where you can list the URLs for pages that you want to crawl but that are not linked to from the initial seed URL.
    - To decrease the number of documents that are available to the data collection, specify a subdomain of the base URL. Or, in the web crawl settings, limit the number of hops from the original page. You can specify subdomains to explicitly exclude from the crawl also.
    - If no documents are listed after a few minutes and a page refresh, then make sure that the content you want to ingest is available from the URL's page source. Some web page content is dynamically generated and therefore cannot be crawled.

- **Configuring search results for uploaded documents**: If you are using a collection of uploaded documents and cannot get the correct search results or the results are not concise enough, consider using *Smart Document Understanding* when you create the data collection.

    You can annotate documents based on text formatting. For example, you can teach {{site.data.keyword.discoveryshort}} that any text in 28-point bold font is a document title. If you apply this information to the collection when you ingest it, you can later use the *title* field as the source for the title section of your search result.

    You can also use Smart Document Understanding to split up large documents into segments that are easier to search. For more information, see the [Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields){: external} topic in the {{site.data.keyword.discoveryshort}} documentation.

- **My response text is surrounded by brackets**: If you notice that your response text is surrounded by brackets and quotation marks (`["My response text"]`) when you test it from the Preview, for example, you might need to change the source field that you're using in the configuration. The unexpected formatting indicates that the value is stored in the source document as an array. Any field that you extract text from must contain a value with a String data type, not an Array data type. When the chat integration shows a response that is extracted from a field that stores the data as an array, it does a straight conversion of the array value into a string, which produces a response that includes the array syntax.

    For example, maybe the field in the source document contains an array with a single text value as its only array element:

    ```json
    "title": ["a single array element"]
    ```
    {: codeblock}

    The array value is converted by the {{site.data.keyword.conversationshort}} into this string value:

    ```json
    "title": "[\"a single array element\"]"
    ```
    {: codeblock}

    As a result, the string is returned in this format in the chat; the surrounding brackets and quotation marks are displayed:

    ```code
    ["a single array element"]
    ```
    {: codeblock}

    If you see this happening, consider choosing a different collection field from which to extract search results.

    The {{site.data.keyword.discoveryshort}} document `highlight` field stores values in an array.
    {: note}

## Next steps
{: #search-add-next-steps}

After you add the search integration for the first time, it appears as a tile on the **Draft environment** page. Click the tile to see or edit the search configuration.

![Search in draft environment](images/search-draft-env.png)

When you're ready, you can repeat the steps to add the search integration to your **Live environment** or to other environments, if you're using [multiple environments](/docs/watson-assistant?topic=watson-assistant-multiple-environments).

![Search in live environment](images/search-live-env.png)

## Test the search integration
{: #search-add-test}

After you configure search, you can send test queries to see the search results that get returned from {{site.data.keyword.discoveryshort}} by using the Preview page.

To test the full experience that customers have when they ask questions that are either answered by the action or trigger a search, use the *Preview* for your assistant.

## Test the search skill in the classic experience
{: #search-skill-add-test}

If you are using a search skill in the classic experience, you can send test queries to see the search results that get returned from {{site.data.keyword.discoveryshort}} by using the Preview pane of the search skill.

To test the full experience that customers will have when they ask questions that are either answered by the dialog or trigger a search, use the *Preview* button for your assistant.

You cannot test the full end-to-end user experience from the dialog "Try it out" pane. The search skill is configured separately and attached to an assistant. The dialog skill has no way of knowing the details of the search, and therefore cannot show search results in its "Try it out" pane.
{: important}

Configure at least one integration channel to test the search skill. In the channel, enter queries that trigger the search. If you initiate any type of search from your dialog, test the dialog to ensure that the search is triggered as expected. If you are not using search response types, test that a search is triggered only when no existing dialog nodes can address the user input. And any time a search is triggered, ensure that it returns meaningful results.

### Sending more requests to the search skill
{: #search-skill-add-increase-flow}

If you want the dialog skill to respond less often and to send more queries to the search skill instead, you can configure the dialog to do so.

You must add both a dialog skill and search skill to your assistant for this approach to work.

Follow this procedure to make it less likely that the dialog will respond by resetting the confidence level threshold from the default setting of 0.2 to 0.5. Changing the confidence level threshold to 0.5 instructs your assistant to not respond with an answer from the dialog unless the assistant is more than 50% confident that the dialog can understand the user's intent and can address it.

1.  From the *Dialog* page of your dialog skill, make sure that the last node in the dialog tree has an `anything_else` condition.

    Whenever this node is processed, the search skill is triggered.

1.  Add a folder to the dialog. Position the folder before the first dialog node that you want to de-emphasize. Add the following condition to the folder:

    `intents[0].confidence > 0.5`

    This condition is applied to all of the nodes in the folder. The condition tells your assistant to process the nodes in the folder only if your assistant is at least 50% confident that it knows the user's intent.

1.  Move any dialog nodes that you do not want your assistant to process often into the folder.

After changing the dialog, test the assistant to make sure the search skill is triggered as often as you want it to be.

An alternative approach is to teach the dialog about topics to ignore. To do so, you can add utterances that you want the assistant to send to the search skill immediately as test utterances in the dialog skill's "Try it out" pane. You can then select the **Mark as irrelevant** option within the "Try it out" pane to teach the dialog not to respond to this utterance or others like it. For more information, see [Teaching your assistant about topics to ignore](/docs/watson-assistant?topic=watson-assistant-logs#logs-mark-irrelevant).

### Disabling the search skill
{: #search-skill-add-disable}

You can disable the search skill from being triggered.

You might want to do so temporarily, while you are setting up the integration. Or you might want to only ever trigger a search for specific user queries that you can identify within the dialog, and use a search skill response type to answer.

To prevent the search skill from being triggered, complete the following steps:

1.  From the **Assistants** page, click the menu for your assistant, and then choose **Settings**.
1.  Open the *Search skill* page, and then set the switch to **Disabled**.
