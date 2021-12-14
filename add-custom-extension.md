---

copyright:
  years: 2021
lastupdated: "2021-12-14"

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
{:preview: .preview}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:table: .aria-labeledby="caption"}
{:video: .video}

{{site.data.content.classiclink}}

# Adding a custom extension
{: #add-custom-extension}

A custom extension is an integration with an external service you have defined. A custom extension can be created for any service with a REST API that is described by an OpenAPI specification.
{: shortdesc}

(more high-level text explaining how custom extensions work, with a link to the [Build a custom extension](/docs/watson-assistant?topic=watson-assistant-build-custom-extension) topic in the "Customizing and developing" section)

## Adding the custom extension to your assistant

To add a custom extension to your assistant, follow these steps:

1. On the **Integrations** page, go to the **Extensions** section and find the tile for the custom extension you want to add.

1. ...

(steps for completing authentication etc.)

## Calling the custom extension from an action

Now that you have added the custom extension to your assistant, you can call it from an action. The custom extension is available as a choice in the **And then** field of any step.

To call a custom extension from an action:

1. In the action editor, open the step you want to call the extension from.

1. ...

(steps for calling the extension. Includes:

- choosing the extension
- choosing the resource/operation
- editing/adding parameters
- viewing extension responses
- how to access response values)
