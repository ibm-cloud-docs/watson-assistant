---

copyright:
  years: 2021, 2022
lastupdated: "2022-02-15"

subcollection: watson-assistant

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:deprecated: .deprecated}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

{{site.data.content.classiclink}}

# Adding assistant responses
{: #respond}

Once an action is activated, the body of the action is composed of multiple *steps* that make up the conversation between your assistant and your users. One part of each step is what the assistant says to the customer when the step is processed.

To create your assistant's response in a step, you use the **Assistant says** section. This represents the text or speech the assistant delivers to a user at a particular step. Depending on the step, you can add a complete answer to a user's question or ask a follow-up question.

You can enter a simple text response just by entering the text that you want your assistant to display to the user. You can also add formatting and web content, and you can reference user information using *variables*.

## Formatting respsonses
{: #respond-formatting}

Use the text editor tools to apply font styling, such as bold or italic, to the text or to add links.

Behind the scenes, font styling and link syntax are stored in Markdown format. If you are using the web chat integration, standard HTML tagging is supported. Other integrations, such as for Facebook and Slack, don't support HTML.

<!--- Behind the scenes, these three choices are stored using Markdown format.

| Choice | Markdown | Example output |
|------------|--------|---------|
| Bold | `There's **no** crying in baseball.` | There's **no** crying in baseball. |
| Italic | `We're talking about *practice*.` | We're talking about *practice*. |
| Link | `Contact us at [ibm.com](https://www.ibm.com).` | Contact us at [ibm.com](https://www.ibm.com). |
{: caption="Formatting" caption-side="top"} --->

If you're using a custom client application that does not support Markdown, don't apply text styling to your text responses.
{: note}

<!--## Including web content
{: #respond-include-web-content}

Depending on how your assistant is deployed, you can include references to web content. Choices include:

| Type | Examples |
| --- | --- |
| Audio | SoundCloud, Mixcloud, mp3 files |
| iFrame | Google Maps, SurveyMonkey, Calendly |
| Image | Images from any public URL |
| Video | YouTube, Vimeo, mp4 files |
{: caption="Web content" caption-side="top"}-->

<!-- To learn more about which deployment options are compatible see **[COMPATIBILITY CHART TOPIC]**. -->

## Adding and referencing variables
{: #respond-variables}

During the conversation, your assistant stores information as *variables*. Variables are containers for data values that become available at run time; the value of a variable can change over time. Variables include *action variables*, which persist only during a particular action, and *session variables*, which are available to any action. For more information about variables, see [Managing information during the conversation](/docs/watson-assistant?topic=watson-assistant-manage-info).

In your assistant's output, you can reference variables in order to personalize the conversation or include information that is available at run time. For more information about referencing variables in what your assistant says, see [Using variables to customize the conversation](/docs/watson-assistant?topic=watson-assistant-manage-info#reference-variables).

## Testing responses
{: #respond-testing}

To see if the assistant responses are formatted correctly, you can use **Preview**.

1.  Click the **Preview** button.
1.  To start the action, enter your first phrase, for example: `What are your store hours?`.
1.  When the assistant responds, check that the message displays as you intended with formatting, use of variables, and so on.

## Tips for adding responses
{: #respond-tips-responses}

- Keep answers short and useful.
- Reflect the user's intent in the response. Doing so assures users that the bot is understanding them, or if it is not, gives users a chance to correct a misunderstanding immediately.
- Only include links to external sites in responses if the answer depends on data that changes frequently.
- Word your responses carefully. You can change how someone reacts to your system based simply on how you phrase a response. Changing one line of text can prevent you from having to write multiple lines of code to implement a complex programmatic solution.

## Response types
{: #respond-response-types}

In addition to text responses, you can use _response types_ to send responses that include multimedia or interactive elements, or to handle channel-specific interactions. To use most response types, you must use the JSON editor to directly edit the response object that your assistant sends to the channel.

For more information about how to edit responses using the JSON editor, see [Defining responses using the JSON editor](/docs/watson-assistant?topic=watson-assistant-assistant-responses-json).

