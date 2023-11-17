---

copyright:
  years: 2021, 2023
lastupdated: "2023-11-17"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Elasticsearch conversational search integration and configuration 
{: #search-add}

[Plus]{: tag-green}

The conversational search requires large language models (LLMs) to search information from a content source and give accurate search results to the users. Elasticsearch with its LLM capabilities enables your assistants to respond faster to any type of searches by using simple conversations. 

You can integrate search in your assistants by using Elasticsearch or {{site.data.keyword.discoveryshort}}. However, when you configure Elasticsearch as the content source, the Watson Discovery settings is erased completely. For more information about integrating {{site.data.keyword.discoveryshort}}, see [{{site.data.keyword.discoveryfull}} search integration setup](/docs/watson-assistant?topic=watson-assistant-search-add).

Refer the following topics to learn more about integrating conversational search by using Elasticsearch:
- Selecting Elasticsearch as the content source





## Setting Up Elasticsearch Search Skill

Working with an Elasticsearch Search Skill involves three main steps. 

1. Providing your Elasticsearch index information so {{site.data.keyword.conversationshort}} can connect to your index. 
2. Configuring the schema mapping between Elasticsearch and Watson Assistant so that a search response can be
   transformed into the correct output for the front end channel.
3. Choosing if you want your Search Skill to be conversational or not.

And that's it! Lets walk through each of those pieces.

### Choosing Elasticsearch

You can start the Elasticsearch setup in the same two places Watson Discovery is historically configured, either on the
Environments page, or the Integrations page. Both can be found in the left hand navigation. From the Environments page
click the "Add +" button in the Search box on the bottom right. From the Integrations page find the Search title by
scrolling down to the extensions section and then click "Add +". After clicking "Add +" in either location you'll see a
modal presenting a choice to either use Elasticsearch or Watson Discovery, choose Elasticsearch to begin configuring
your instance.

<img src="img_search_choice.png" alt="Search choice modal" width="55%"/>

### Elasticsearch Index Setup

Once you've chosen Elasticsearch as the Search Skill type you'll need to provide four pieces of information. The
Elasticsearch url (and optional Elasticsearch port), Elasticsearch index, Elasticsearch username, Elasticsearch
password. With this information Watson Assistant will be able to send queries to your Elasticsearch index in order to
answer your users search related questions, once you've provided it click "Next" in the top right corner.

<img src="img_search_elastic_instance_config.png" alt="Elasticsearch instance config" width="55%"/>

### Elasticsearch Schema Mapping

On the next panel you'll see three input fields, one for Title, Body, and optional URL. In these fields you need to
specify the Elasticsearch field you want used for that part of the Search Skill response. For example, if the
title field in your data is "fileTitle" then you would input that in the Title input field, and so on.

<img src="img_search_schema_mapping.png" alt="Search schema mapping" width="30%"/>

### Elasticsearch with Conversational Search

Below the input fields for Title, Body, and optional URL you will see a Conversational search toggle. Conversational
search uses a LLM to transform the users query and search results into a conversational form instead of the normal title, body,
and optional url format.

<img src="img_search_conversational_search_toggle.png" alt="Conversational search toggle" width="30%"/>  

After you've chosen whether or not to enable Conversational Search, you have the option of changing the default Search
display text. These are the messages that will be shown to the user when a successful Search query is returned, when no
results are found, or when there is a connection issue communicating with the search environment.

<img src="img_search_messages_config.png" alt="Search messages config" width="30%"/>

Once you've finished configuring this panel click "Finish" in the top right and your Search Skill setup will be
complete.


#### Calling your Search Skill in Actions or Dialog

Now that your Search Skill is setup the next thing that needs to be done is to configure actions / intents which are suppose to
search for results in your search skill when triggered by a users query. The steps will be different depending on if
you're using Dialog or Actions.

For Dialog, first create an intent for a query your customer may ask. Then create a dialog node using that intent and
choose "Search Skill" in the "Assistant responds" section. In that section you can also control the Query and Filter for
that specific search request.

<img src="img_search_dialog_setup.png" alt="Search dialog setup" width="55%"/>

For Actions, first create an action for a query your customer may ask. Then, In the "And then" section, choose "Search
for the answer". Here you can also set a "Custom query" or a "Customer filter".

<img src="img_search_actions_setup.png" alt="Search dialog setup" width="55%"/>

Once you've completed setting up your example you can test your Search Skill setup using either the Actions preview, the
Dialog Try it panel, the Assistant preview, or the preview link.

### Tooling Limitations for Elasticsearch Set Up

While you can setup a working Elasticsearch skill with the new Watson Assistant Tooling (UI) there are some limitations
worth mentioning. 

The majority of these limitations are related to customizing the query body for Elasticsearch. The query body is used to
manipulate the users request into a format that is expected by search. It controls the form the query takes, and what
fields the query is searched against, as well as any filter the query should be run through before a search is made. And
lastly, it can be used to specify a "size" which determines how many results should be returned for the query. For more
information on changing the query_body through the API see [customizing the query_body](#custom-query-body--filter).

It's also worth mentioning that Elasticsearch setup in tooling only supports Basic auth at this time.