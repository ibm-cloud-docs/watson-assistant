---

copyright:
  years: 2019, 2023
lastupdated: "2023-10-27"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Connecting customers with support
{: #dialog-support}

No matter where you deploy your assistant, give your customers a way to get more support when they need it.
{: shortdesc}

Build your dialog to recognize when customers need help that cannot be provided by the assistant. Add logic that can connect your customers to whatever type of professional support you offer. Your solutions might include:

- A toll-free phone number to a call center that is staffed by live agents
- An online support ticket form that customers complete and submit
- A service desk solution that is configured to work with your web chat integration or a custom client application

Design your dialog to recognize customer requests for help and address them. Add an intent that understands the customer request, and then add a dialog branch that handles the request.

For example, you might add an intent and use it in a dialog node like these intents:

| Intent name | Intent user example 1 | Intent user example 2 | Response from dialog node that conditions on intent |
| --- | --- | --- | --- |
| `#call_support` | *How do I reach support?* | *What's your toll-free number?* | *`Call 1-800-555-0123 to reach a call center agent at any time.`* |
| `#support_ticket` | *How do I get help?* | *Who can help me with an issue I'm having?* |  *`Go to [Support Center](https://example.com/support) and open a support ticket.`* |
{: caption="Alternative support request intent examples" caption-side="bottom"}

If you deploy your assistant with an integration that has built-in service desk support, you can initiate a transfer by using the special *Connect to human agent* response type in your dialog response.

## Adding chat transfer support
{: #dialog-support-transfers}

Design your dialog so that it can transfer customers to live agents. Consider adding support for initiating a transfer in the following scenarios:

- Anytime a user asks to speak to a person. 

   Create an intent that can recognize when a customer asks to speak to someone. After you define the intent, you can add a root-level dialog node that conditions on the intent. As the dialog node response, add a *Connect to human agent* response type. At run time, if the user asks to speak to someone, this node is triggered and a transfer is initiated on the user's behalf.

- When the conversation broaches a topic that is sensitive in nature, you can start a transfer. 

   For example, an insurance company might want questions about bereavement benefits always to be handled by a person. Or, if a customer wants to close an account, you might want to transfer the conversation to a representative who is authorized to offer incentives to keep the customer's business.

- When the assistant repeatedly fails to understand a customer's request. Instead of asking the customer to retry or rephrase the question over and over, your assistant can offer to transfer the customer to a live agent.

To design a dialog that can transfer the conversation, complete the following steps:

1.  Add an intent that can recognize a user's request to speak to a live agent.

    You can create your own intent or add the prebuilt intent `#General_Connect_to_Agent` that is provided with the **General** content catalog.

1.  Add a root node to your dialog that conditions on the intent you created in the previous step. Choose **Connect to human agent** as the response type.

    For more information, see [Adding a *Connect to human agent* response type](/docs/watson-assistant?topic=watson-assistant-dialog-overview#dialog-overview-add-connect-to-human-agent).

1.  Add meaningful names to the dialog nodes in your dialog.

    When a conversation is transferred to an agent, the name of the most-recently processed dialog node is sent with it. To ensure that a useful summary is provided to service desk agents when a conversation is transferred to them, add short dialog node names that reflect the node's purpose. For example, *Find a store*.

    Every dialog branch can be processed by the assistant while it chats with a customer, including branches with root nodes in folders.
    {: note}

1.  If a child node in any dialog branch conditions on a request or question that you do not want the assistant to handle, add a **Connect to human agent** response type to the child node.

    At run time, if the conversation reaches this child node, the dialog is passed to a live agent at that point.

Your dialog is now ready to support transfers from your assistant to a service desk agent.

## Measuring containment
{: #dialog-support-containment}

From the Analytics page, you can measure conversation containment. Containment is the rate at which your assistant is able to satisfy a customer's request without live agent intervention per conversation.

To measure containment accurately, the metric must be able to identify when a live agent intervention occurs. The metric primarily uses the *Connect to human agent* response type as an indicator. If a user conversation log includes a call to a *Connect to human agent* response type, then the conversation is considered to be *not contained*.

However, not all live agent interventions are transacted by using a *Connect to human agent* response type. If you use an alternative method to deliver more support, you must take extra steps to register the fact that the customer's need was not fulfilled by the assistant. For example, you might direct customers to your call center phone number or to an online support ticket form URL. If so, you need to flag these types of redirects so the containment metric is able to pick them up.

To enable the containment metric, complete the following steps:

1.  For any dialog nodes that transfer the chat to a service desk agent, add a *Connect to human agent* response type.

    For more information, see [Adding a *Connect to human agent* response type](/docs/watson-assistant?topic=watson-assistant-dialog-overview#dialog-overview-add-connect-to-human-agent).

1.  For any dialog nodes that redirect customers to alternative forms of customer support, add a context variable that is named `context_connect_to_agent` and set it to `true`.

    The process that calculates the containment metric looks for instances of this context variable, and registers any occurrences that it finds as interventions.

    - From the dialog node, go to the *Assistant responds* section and click the menu icon ![overflow menu icon](images/overflow-menu--vertical.svg).

      If you're using multiple conditioned responses, you must click **Customize response** to see the menu that is associated with the response.
      {: tip}

    - Click **Open context editor**.

    - Add the following variable name and value to define the context variable:

      | Variable | Value |
      | --- | --- |
      | `context_connect_to_agent` | `true` |
      {: caption="Special containment context variable" caption-side="bottom"}

    - Click **X** to close the dialog node. Your change is saved automatically.

      If you're using multiple conditioned responses, you must click **Save** first.
      {: tip}
