---

copyright:
  years: 2022, 2024
lastupdated: "2024-06-18"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Building a custom extension
{: #build-custom-extension}

If you need to integrate your assistant with an external service that has a REST API, you can build a custom extension by importing an OpenAPI document.
{: shortdesc}

After you create a custom extension, you can connect it to an assistant as an integration. In your actions, you can then define steps that interact with the external service by calling the extension.

The [{{site.data.keyword.conversationshort}} extension starter kit](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/extensions) repo on GitHub provides files and [Advanced Usage tips](https://github.com/watson-developer-cloud/assistant-toolkit/blob/master/integrations/extensions/docs/ADVANCED_USAGE.md) that you can use to quickly build a working extension. Each starter kit includes a tested OpenAPI definition that you can use to create an extension that accesses a third-party API, along with a downloadable JSON file you can import to create an assistant that accesses the extension.
{: tip}

## Overview
{: #build-custom-extension-overview}

OpenAPI (formerly known as Swagger) is an open standard for describing and documenting REST APIs. An OpenAPI document defines the resources and operations that are supported by an API, including request parameters and response data, along with details such as server URLs and authentication methods.

An OpenAPI document describes a REST API in terms of _paths_ and _operations_. A path identifies a particular resource that can be accessed by using the API (for example, a hotel reservation or a customer record). An _operation_ defines a particular action that can be performed on that resource (such as creating, retrieving, updating, or deleting it). 

The OpenAPI document specifies all of the details for each operation, including the HTTP method that is used, request parameters, the data included in the request body, and the structure of the response body.

For more information about the OpenAPI specification, see [OpenAPI Specification](https://swagger.io/specification/){: external}.

When you create a custom extension, you import an OpenAPI document that describes the REST API of an external service. {{site.data.keyword.conversationfull}} parses the OpenAPI document to identify the operations supported by the external service, along with information about the input parameters and response for each operation and supported authentication methods.

After this processing is complete, the custom extension becomes available as a new integration that you can connect to the assistant. Your assistant can then use the extension to send requests to the external service based on conversations with your customers. Values that are included in the response from the service are then mapped to action variables, which can be accessed by subsequent action steps.

(For more information about connecting a custom extension to an assistant, see [Add a custom extension](/docs/watson-assistant?topic=watson-assistant-add-custom-extension).)

## Preparing the API definition
{: #build-custom-extension-openapi-file}

To create a custom extension, you need access to an OpenAPI document that describes the REST API you want to integrate with. Many third-party services publish OpenAPI documents that describe their APIs, which you can download and import. For an API that your company maintains, you can use standard tools to create an OpenAPI document that describes it.

The [SwaggerHub](https://swagger.io/tools/swaggerhub/){: external} website offers an [OpenAPI 3.0 Tutorial](https://support.smartbear.com/swaggerhub/docs/tutorials/openapi-3-tutorial.html){: external}, and [tools](https://swagger.io/tools/){: external} to help you develop and validate your OpenAPI document. You can use the online [Swagger editor](https://editor.swagger.io/){: external} to convert your OpenAPI document to the correct format and OpenAPI version.
{: tip}

The OpenAPI document must satisfy the following requirements and restrictions:

- The document must conform to the OpenAPI 3.0 specification. If you have an OpenAPI (or Swagger) document that uses an earlier version of the specification, you can use the online [Swagger editor](https://editor.swagger.io/) to convert it to OpenAPI 3.0.
- The document must be in JSON format (YAML is not supported). If you have a YAML document, you can use the online [Swagger editor](https://editor.swagger.io/) to convert it to JSON.
- The request body in the JSON script must be presented as an object. For example: 

    ```json
    {
        name: "Bob",
        hobbies: ["sleeping", "eating", "walking"]
    }
    ```
    {: codeblock}
    
- The size of the document must not be more than `4 MB` if you have a *Plus* or higher plan of {{site.data.keyword.conversationshort}}. However, if you have an *Enteprise* plan with data isolation, the size of the document must not be more than `8 MB`.
- The `content-type` must be `application/json`.
- Each operation must have a clear and concise `summary`. The summary text is used in the UI to describe the operations that are available from an action, so it should be short and meaningful to someone who is building an assistant.
- [Relative URLs](https://swagger.io/docs/specification/api-host-and-base-path/#relative-urls){: external} are currently not supported.
- Only Basic, Bearer, OAuth 2.0, and API key authentication are supported.
- For OAuth 2.0 authentication, Authorization Code, Client Credentials, Password, and custom grant types that starts with `x-` are supported. Note that `x-`<any custom name> is used by the [IBM IAM authentication mechanism](/docs/account?topic=account-iamoverview) and by [watsonx](https://www.ibm.com/watsonx).
- Schemas that are defined by using `anyOf`, `oneOf`, and `allOf` are currently not supported.

## Adhering to the response timeout limit
{: #adhere-response-timeout-limit}

You must adhere to the response timeout limit, which is 30 seconds, while calling an external API. The timeout value for a custom extension is not configurable.

## Building the custom extension
{: #build-custom-extension-building}

To build a custom extension based on the API definition, follow these steps:

1. Go to the ![Integrations icon](images/integrations.svg) **Integrations** page.

1. Scroll to the **Extensions** section and click **Build custom extension**.

1. Read the **Get started** information and click **Next** to continue.

1. In the **Basic information** step, specify the following information about the extension you are creating:

    - **Extension name**: A short, descriptive name for the extension (for example, `CRM system` or `Weather service`). This name that is displayed on the tile for the extension on the **Integrations** page, and in the list of available extensions in the action editor.
    - **Extension description**: A brief summary of the extension and what it does. The description is available from the **Integrations** page.

    Click **Next**.

1. In the **Import OpenAPI** step, click or drag to add the OpenAPI document that describes the REST API you want to integrate with.

    If you encounter an error when you try to import the JSON file, make sure the file satisfies all requirements listed in [Preparing the API definition](#build-custom-extension-openapi-file). Edit the file to correct errors or remove unsupported features. Click the **X** to clear the error message, and try the import again.

    After you import the file successfully, click **Next**.

1. In the **Manage extension** step, you can review the imported OpenAPI document if required. 

1. In the **Authentication** tab, you see information about the authentication methods that are defined in the OpenAPI document. *Table. Fields in Authentication tab* gives details about the fields in the Authentication tab:

    | Field name | Description | Values |
    |---- | ---- | ---- |
    | **Authentication type** | The type of authentication set up in the OpenAPI script. | - `OAuth 2.0` <br> - `Basic Auth` <br> - `API key auth` <br> - `Bearer auth` |
    | **Username** | The username credential in the OpenAPI script. | For example, `user` |
    | **Password** | The password credential set up in the OpenAPI script. | For example, `Password@123` |
    | **Servers** | The link to the server that is defined in the Open API document to connect. to the API extension. | For example, `https://custom-extension-server.xyz` |

1. The **Review operations** table shows the operations that the assistant is able to call from an action step. An _operation_ is a request by using a particular HTTP method, such as `GET` or `POST`, on a particular resource.

    ![Review operations table](images/extension-review-operations.png)

        For each operation, a row in the table shows the following information:

    - **Operation**: A description of the operation, which is derived from either the `summary` (if present) or `description` in the OpenAPI file.
    - **Method**: The HTTP method used to send the API request for the operation.
    - **Resource**: The path to the resource the operation acts upon.

    To see more information about an operation, click the ![label](images/twistie.png) icon next to its row in the table. The following details are shown:

    - **Request parameters**: The list of input parameters defined for the operation, along with the type of each parameter and whether the parameter is required or optional.
    - **Response properties**: The properties of the response body that are mapped to variables the assistant can access.

1. If you are satisfied with the extension, click **Finish**.

    If you want to change something, delete the extension, edit the JSON file to make your changes, and repeat the import process.

The new extension is now available as a tile in the **Extensions** section of the integrations catalog, and you can [add it to your assistant](/docs/watson-assistant?topic=watson-assistant-add-custom-extension).


