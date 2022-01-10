---

copyright:
  years: 2021
lastupdated: "2022-01-10"

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

A custom extension provides access to the operations supported by the external service. After you connect the extension to your assistant, your actions can call the external service, passing in any necessary input data. After the external service responds, any returned response data is available as action variables that subsequent steps can access.

For more information about how to create a custom extension, see [Build a custom extension](/docs/watson-assistant?topic=watson-assistant-build-custom-extension).

## Adding the custom extension to your assistant

To add a custom extension to your assistant, follow these steps:

1. From your assistant, navigate to the page for the environment where you want to configure the webhook (**Draft environment** or **Live environment**).

1. Click **Browse catalog**.

1. On the **Integrations** page, go to the **Extensions** section and find the tile for the custom extension you want to add. Click the ![menu icon](images/kebab.png) menu icon if you want to see overview information about the extension.

1. Click **Add**. Review the overview of the extension and click **Confirm** to add it to your assistant.

1. Read the information in the **Get started** step, and then click **Next**.

1. In the **Authentication** step, specify the authentication credentials and server URL you want your assistant to use when calling the service. Click **Next**.

1. In the **????** table, review the details of the data returned by each operation the extension supports. The table shows the following information:

    - [details of table, once there is a new design]

1. Click **Finish**.

The extension is now connected to your assistant and available for use by actions.

## Calling the custom extension from an action
{: #add-custom-extension-action}

Now that you have added the custom extension to your assistant, you can call it from an action. The custom extension is available as a choice in the **And then** field of any step.

To call a custom extension from an action:

1. In the action editor, create or open the step from which you want to call the extension.

1. In the step editor, click **And then**.

1. Click **Use an extension**.

1. ...

