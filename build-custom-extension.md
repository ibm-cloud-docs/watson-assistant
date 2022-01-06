---

copyright:
  years: 2022
lastupdated: "2022-01-06"

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

If you need to integration your assistant with an external service that has a REST API, you can build a custom extension by importing an OpenAPI document.
{: shortdesc}

By importing an OpenAPI document that describes an external service, you can create an extension that you can then connect to an assistant as an integration. You can then define actions that interact with the external service by calling the extension.

## Overview

OpenAPI (formerly known as Swagger) is an open standard for describing and documenting REST APIs. An OpenAPI document defines the resources and operations supported by an API, including input parameters and response data, along with details such as server URLs and authentication methods.

An OpenAPI document describes a REST API in terms of _paths_ and _operations_. A path identifies a particular resource that can be accessed using the API (for example, a hotel reservation), while an _operation_ defines a particular action that can be performed on that resource (such as creating, retrieving, updating, or deleting). The OpenAPI document specifies all of the details for each operation, including the HTTP method used, the required and optional input parameters, and the structure of the response body.

For more information about the OpenAPI specification, see [OpenAPI Specification](https://swagger.io/specification/){: external}.

When you create a custom extension, you import an OpenAPI document that describes the REST API of an external service. {{site.data.keyword.conversationshort}} parses the OpenAPI document to identify the operations supported by the external service, along with information about the input parameters and response for each operation and supported authentication methods.

After this processing has completed, the custom extension becomes available as a new integration that you can connect to the assistant in either the Draft or Live environment. Your assistant can then send requests to the extension based on conversations with your customers, and it can use the returned data it receives. (For more information about connecting a custom extension to an assistant, see [Add a custom extension](/docs/watson-assistant?topic=watson-assistant-add-custom-extension).)

## Preparing the API definition

To create a custom extension, you need access to an OpenAPI document that describes the REST API you want to integrate with. Many third-party services publish OpenAPI documents that describe their APIs, which you can download and import. If you need to connect to an API that your company maintains, you can use standard tools to create an OpenAPI document describing it. (For more information about creating an OpenAPI document, see [OpenAPI 3.0 Tutorial](https://support.smartbear.com/swaggerhub/docs/tutorials/openapi-3-tutorial.html).)

To work with {{site.data.keyword.conversationshort}}, an OpenAPI document must conform to the OpenAPI 3.0 specification. If you have an OpenAPI (or Swagger) document that uses an earlier version of the specification, you can use the online [Swagger editor](https://editor.swagger.io/) or other tools to convert it to OpenAPI 3.0.

In addition, note the following current requirements and restrictions:

- The OpenAPI document must be in JSON format (YAML is not supported). If you have a YAML document, you can use the online [Swagger editor](https://editor.swagger.io/) to convert it to JSON.
- Each operation must have a clear and concise `summary`. The text of the summary is used in the UI to describe the operations that are available from an action, so it should be short and meaningful to someone who is building an assistant.
- [Relative URLs](https://swagger.io/docs/specification/api-host-and-base-path/#relative-urls){: external} are not supported.
- Only `Basic`, `Bearer`, and `API key` authentication are supported.
- References using `$ref` are currently not supported. (All schemas and other definitions must be inline.)
- Schemas defined using `anyOf`, `oneOf`, or `allOf` are not supported.
- Arrays are not supported for request parameters. You can import a document that defines parameters that take arrays, but the assistant will not be able to pass values for these parameters.

If your API document contains some features that {{site.data.keyword.conversationshort}} does not support, you can delete the unsupported sections, as long as it remains a valid OpenAPI document.

## Building the custom extension

To build a custom extension based on the API definition, follow these steps:

1. On the **Integrations** page, go to the **Extensions** section and click the **Build a custom extension** tile.

1. ...

(steps for building an extension. includes:

- specifying name & description
- importing OpenAPI file
- reviewing the imported info
- optionally tweaking the OpenAPI and iterating
)
