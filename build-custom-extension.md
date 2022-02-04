---

copyright:
  years: 2022
lastupdated: "2022-02-04"

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

# Building a custom extension
{: #build-custom-extension}

If you need to integrate your assistant with an external service that has a REST API, you can build a custom extension by importing an OpenAPI document.
{: shortdesc}

By importing an OpenAPI document that describes an external service, you can create an extension that you can then connect to an assistant as an integration. In your actions, you can then define steps that interact with the external service by calling the extension.

## Overview
{: #build-custom-extension-overview}

OpenAPI (formerly known as Swagger) is an open standard for describing and documenting REST APIs. An OpenAPI document defines the resources and operations supported by an API, including request parameters and response data, along with details such as server URLs and authentication methods.

An OpenAPI document describes a REST API in terms of _paths_ and _operations_. A path identifies a particular resource that can be accessed using the API (for example, a hotel reservation or a customer record), while an _operation_ defines a particular action that can be performed on that resource (such as creating, retrieving, updating, or deleting it). The OpenAPI document specifies all of the details for each operation, including the HTTP method used, request parameters, the data included in the request body, and the structure of the response body.

For more information about the OpenAPI specification, see [OpenAPI Specification](https://swagger.io/specification/){: external}.

When you create a custom extension, you import an OpenAPI document that describes the REST API of an external service. {{site.data.keyword.conversationshort}} parses the OpenAPI document to identify the operations supported by the external service, along with information about the input parameters and response for each operation and supported authentication methods.

After this processing has completed, the custom extension becomes available as a new integration that you can connect to the assistant in the Draft or Live environment. Your assistant can then use the extension to send requests to the external service based on conversations with your customers. Values included in the response from the service are then mapped to action variables, which can be accessed by subsequent action steps.

(For more information about connecting a custom extension to an assistant, see [Add a custom extension](/docs/watson-assistant?topic=watson-assistant-add-custom-extension).)

## Preparing the API definition
{: #build-custom-extension-openapi-file}

To create a custom extension, you need access to an OpenAPI document that describes the REST API you want to integrate with. Many third-party services publish OpenAPI documents that describe their APIs, which you can download and import. For an API that your company maintains, you can use standard tools to create an OpenAPI document describing it. (For more information about creating an OpenAPI document, see [OpenAPI 3.0 Tutorial](https://support.smartbear.com/swaggerhub/docs/tutorials/openapi-3-tutorial.html).)

The OpenAPI document must satisfy the following requirements and restrictions:

- The document must conform to the OpenAPI 3.0 specification. If you have an OpenAPI (or Swagger) document that uses an earlier version of the specification, you can use the online [Swagger editor](https://editor.swagger.io/) to convert it to OpenAPI 3.0.
- The document must be in JSON format (YAML is not supported). If you have a YAML document, you can use the online [Swagger editor](https://editor.swagger.io/) to convert it to JSON.
- Each operation must have a clear and concise `summary`. The text of the summary is used in the UI to describe the operations that are available from an action, so it should be short and meaningful to someone who is building an assistant.
- [Relative URLs](https://swagger.io/docs/specification/api-host-and-base-path/#relative-urls){: external} are currently not supported.
- Only `Basic`, `Bearer`, and `API key` authentication are supported.
- References using `$ref` are currently not supported. (All schemas and other definitions must be inline.)
- Schemas defined using `anyOf`, `oneOf`, and `allOf` are currently not supported.
- Arrays are not supported in request bodies. You can import a document that defines requests that take arrays, but the assistant will not be able to pass values for these parameters.
- Arrays in response bodies are included, but individual values in an array are not mapped to separate action variables. These values can be accessed from an assistant only by writing expressions in the JSON editor.

## Building the custom extension

To build a custom extension based on the API definition, follow these steps:

1. On either the **Draft environment** or **Live environment** page, click **Browse catalog** to open the integrations catalog.

1. On the **Integrations** page, scroll to the **Extensions** section and click **Build a custom extension**.

1. Read the **Get started** information and click **Next** to continue.

1. In the **Basic information** step, specify the following information about the extension you are creating:

    - **Extension name**: A short, descriptive name for the extension (for example, `CRM system` or `Weather service`). This is the name that will be displayed on the tile for the extension on the **Integrations** page.
    - **Extension description**: A brief summary of the extension and what it does. The description will also be available from the **Integrations** page.

    Click **Next**.

1. In the **Import OpenAPI** step, click or drag and drop to add the OpenAPI document that describes the REST API you want to integrate with. Click **Next**.

1. If you an encounter an error when you try to import the JSON file, make sure the file satisfies all of the requirements listed in [Preparing the API definition](##build-custom-extension-openapi-file). Edit the file to correct errors or remove unsupported features, and try the import again.

1. In the **Review extension** step, review what has been imported. The **Extension operations** shows the operations that the assistant will be able to call from an action step. (An _operation_ is a request using a particular HTTP method, such as `GET` or `POST`, on a particular resource.)

    The table is organized by categories derived from the `tags` field in the OpenAPI file. Click the ![label](images/twistie.png) icon to see the operations in a category.

    [image of example table]

    For each operation, the table shows the following information:

    - **Operation**: A description of the operation, which is derived from either the `summary` (if present) or `description` in the OpenAPI file.
    - **Method**: The HTTP method used to send the API request for the operation.
    - **Resource**: The path to the resource the operation acts upon.

<!-->
1. To see additional information about an operation, hover the mouse pointer over its row in the table and click the ![menu icon](images/kebab.png) menu icon. Select **Request** or **Response** to see details about the information sent with a request and returned with a response.

    The **Request** table shows the input fields for which the assistant will be able to provide values when sending the request.
    
    [image of example table]
    
    Each row in the table shows the following information:

    - **Name**: The name of the field, which might be a parameter (such as a query parameter or path parameter) or a property in the request body. The name is derived from the `name` field in the OpenAPI definition.
    - **Description**: The description of the parameter or property, taken from the `description` field.
    - **Example**: An example value, taken from the `example` field.

    The **Response** table shows the action variables that will contain the data included in the response from the external service. After the request completes, these action variables will be available to subsequent action steps.
    
    [image of example table]
    
    For each variable, the table shows the following information:

    - **Name**: The name of the action variable.
    - **Description**: A description of the property that is mapped to the action variable. This might be a root property of the response body, or a property of a nested object in the response.
    - **Path**: The path identifying the location of the property in the response body.
    - **Example**: An example value.

    If a response property contains an array, the individual elements in the array are not extracted as separate values. To access an element in an array, you must write an expression. For more information about expressions, see [Writing expressions](/docs/watson-assistant?topic=watson-assistant-expressions.md).
    {: note}
-->
1. If you are satisfied with the extension, click **Finish**.

    If you want to change something, delete the extension, edit the JSON file to make your changes, and repeat the import process.

The new extension is now available from the integrations catalog.
