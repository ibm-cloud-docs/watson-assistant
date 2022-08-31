---

copyright:
  years: 2022
lastupdated: "2022-09-01"

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

# Adding an extension to your assistant
{: #add-custom-extension}

After you build a custom extension, you must add it to the assistant before it can be accessed by actions.
{: shortdesc}

Adding the extension to the assistant configures the extension for use within a particular environment (draft or live), and it makes the extension available so that it can be called from actions.

You can use different configuration details for each environment. For example, you might want to use the URL for a test server in the draft environment, but a production server in the live environment.

For information about how to create a custom extension, see [Build a custom extension](/docs/watson-assistant?topic=watson-assistant-build-custom-extension).

## Adding the extension to the draft environment

To add a custom extension to the assistant, follow these steps:

1. On the ![Integrations icon](images/integrations-icon.png) **Integrations** page, scroll to the **Extensions** section and find the tile for the custom extension you want to add.

1. Click **Add**. Review the overview of the extension and click **Confirm** to configure it for your assistant.

    When you first add an extension to an assistant, the configuration settings you provide are applied only to the draft environment. You must complete configuration for the draft environment before you can add the extension in the live environment.
    {: important}

1. Read the information in the **Get started** step, and then click **Next**.

1. In the **Authentication** step, specify the authentication and server information you want your assistant to use when calling the service.

    - In the **Authentication type** field, select the type of authentication to use.

        Depending on the authentication type you select, you might also need to specify additional information (for example, **Username** and **Password** for HTTP basic authentication).

    - In the **Servers** field, select the server URL to use.

        If the selected URL contains any variables, also specify the values to use. Depending on how each variable is defined in the OpenAPI document, you can either select from a list of valid values or type the value to use in the field.

        The **Generated URL** message shows the full URL that the assistant will use, including the variable values.

     Click **Next**.

1. In the **Review extension** step, review the operations supported by the extension.

    The **Review operations** table shows the operations that the assistant will be able to call from an action step. An _operation_ is a request using a particular HTTP method, such as `GET` or `POST`, on a particular resource.

    ![Review operations table](images/extension-review-operations.png)

    For each operation, a row in the table shows the following information:

    - **Operation**: A description of the operation, which is derived from either the `summary` (if present) or `description` in the OpenAPI file.
    - **Method**: The HTTP method used to send the API request for the operation.
    - **Resource**: The path to the resource the operation acts upon.

    To see more information about an operation, click the ![label](images/twistie.png) icon next to its row in the table. The following additional details are shown:

    - **Request parameters**: The list of input parameters defined for the operation, along with the type of each parameter and whether the parameter is required or optional.
    - **Response properties**: The properties of the response body that will be mapped to variables the assistant can access.

1. Click **Finish**.

1. Click **Close** to return to the Integrations page.

The extension is now connected to your assistant and available for use by actions in the draft environment.

## Configuring the extension for the live environment

To configure the extension for the live environment, follow these steps:

1. On the ![Integrations icon](images/integrations-icon.png) **Integrations** page, scroll to the **Extensions** section and find the tile for the custom extension you want to add.

1. Click **Open**. The **Open custom extension** window opens.

1. In the **Environment** field, select **Live**. Click **Confirm**.

1. Repeat the configuration process, specifying the values you want to use for the live environment.

The extension is now available in the environments you have configured, and it can be called from the assistant. For more information about how to call an extension from an action, see [Calling a custom extension](/docs/watson-assistant?topic=watson-assistant-call-extension).
