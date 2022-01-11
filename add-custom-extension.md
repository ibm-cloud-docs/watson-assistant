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

After you have built a custom extension, you must add it to the assistant before it can be accessed by actions.
{: shortdesc}

Adding the extension to the assistant configures the extension for use within a particular environment (Draft or Live), and it makes the extension available in the **And next** field in the action editor.

For information about how to create a custom extension, see [Build a custom extension](/docs/watson-assistant?topic=watson-assistant-build-custom-extension).

To add a custom extension to the assistant, follow these steps:

1. From the **Draft environment** or **Live environment** page, click **Browse catalog**.

    When you first add an extension to an assistant, the configuration settings you provide are applied only to the Draft environment. This is true even if you open the catalog from the **Live environment** page.
    {: note}

1. On the **Integrations** page, go to the **Extensions** section and find the tile for the custom extension you want to add. Click the ![menu icon](images/kebab.png) menu icon if you want to see overview information about the extension.

1. Click **Add**. Review the overview of the extension and click **Confirm** to add it to your assistant.

1. Read the information in the **Get started** step, and then click **Next**.

1. In the **Authentication** step, specify the authentication credentials and server URL you want your assistant to use when calling the service. Click **Next**.

1. In the **Choose operations** step, review the operations supported by the extension. The table shows the following information about each operation:

    - **Operation**: The name of the operation, based on the `operationId` in the API definition.
    - **Description**: A brief description of the operation, taken from the `summary` in the API definition.
    - **Method**: The HTTP method used for the request.
    - **Resource**: The path to the resource the request acts upon.

<!-- not sure if this is in MVP
    If you want to limit what the assistant can access, you can remove operations from the table. To remove an operation, hover the mouse pointer over its row in the table and click the ![menu icon](images/kebab.png) menu icon. Select **Remove from assistant** to remove the operation. (If you change your mind later, you can re-add the operation by selecting **Add to assistant**.) -->

1. For each supported operation, you can review the request and response data supported by the extension.

To see additional information about an operation, hover the mouse pointer over its row in the table and click the ![menu icon](images/kebab.png) menu icon. Select **Request** or **Response** to see details about the information sent with a request and returned with a response.

    The **Request** table shows the input fields for which the assistant will be able to provide values when sending the request.
    
    [image of example table]
    
    Each row in the table shows the following information:

    [TBD ... need to understand what this will look like]

    The **Response** table shows the fields that are included in the response data received from the external service.
    
    [image of example table]
    
    For each variable, the table shows the following information:

    [TBD ... need to understand what this will look like]

  <!-- not sure what is in MVP
    If a response property contains an array, the individual elements in the array are not extracted as separate values. To access an element in an array, you must write an expression. For more information about expressions, see [Writing expressions](/docs/watson-assistant?topic=watson-assistant-expressions.md).
    {: note}
    -->

1. Click **Finish**.

The extension is now connected to your assistant and available for use by actions in the Draft environment.

To configure the extension for the Live environment, follow these steps:

1. Go to the **Live environment** page.

1. Under **Resolution Methods**, find the tile for the extension. You should see an indication that setup is incomplete:

    [image of extension with "Finish setup" indicator]

1. Click the tile and repeat the configuration process, specifying the values you want to use for the Live environment.
