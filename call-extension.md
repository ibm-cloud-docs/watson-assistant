---

copyright:
  years: 2021
lastupdated: "2022-01-13"

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

# Calling an extension
{: #call-extension}

An extension is an integration with an external service. By calling an extension from an action, your assistant can send requests to the external service and receive response data it can use in the conversation.
{: shortdesc}

For example, you might use an extension to interact with a ticketing or customer relationship management (CRM) system, or to retrieve real-time data such as mortgage rates or weather conditions. Response data from the extension is then available as action variables, which your assistant can use in the conversation.

For information about how to build a custom extension, see [Build a custom extension](/docs/watson-assistant?topic=watson-assistant-build-custom-extension).

To call a custom extension from an action:

1. In the action editor, create or open the step from which you want to call the extension.

1. In the step editor, click **And then**.

1. Click **Use an extension**.

1. In the **Extension setup** window, specify the following information:

    - In the **Extension** field, select the extension you want to call.

    - In the **Operation** field, select the operation you want to perform.

1. Specify values for each of the required input parameters. To assign a value to a parameter, click the input field for the value:

    [image showing UI for setting parameter values]

    Select from the list to set the new value for the session variable:

    - Select an action variable to use the value of a customer response. You can choose an action variable created by any previous step in the current action.

    - Select a session variable or assistant variable to use its value.

    <!-- not supported yet
    - Select **Expression** to write an expression to define the value for the session variable. For more information about expressions, see [Writing expressions](/docs/watson-assistant?topic=watson-assistant-expressions).-->

    You cannot currently use an expression to specify a parameter value. If you need to use an expression, insert a step before you call the extension, and use that step to assign the expression to an action variable. You can then use the variable as the parameter value.
    {: note}

1. If you want to specify values for an optional parameter, click **Optional parameters** and select the parameter you want to specify. Repeat this process for each optional parameter you want to use.

1. Click **Apply**.

The **And then** section of the step editor now shows an overview of the call to the extension:

[screen shot of step editor showing call to extension]

In subsequent steps, you can access the response variables and use them just as you would any other variable. For example, you might use a response variable as a step condition, or reference one in the output sent to your customer.
