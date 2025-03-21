---

copyright:
  years: 2015, 2024
lastupdated: "2024-12-24"

subcollection: watson-assistant


---

{{site.data.keyword.attribute-definition-list}}

# Starting and ending the dialog
{: #dialog-start}

Learn more about how to use the nodes that are added to your dialog automatically to start and end the conversation.
{: shortdesc}

The following dialog nodes are included automatically:

- **Welcome**: Defines how the assistant greets the user and starts the conversation.
- **Anything else**: What the assistant says when a customer's request cannot be satisfied by any of the defined intents.

## Starting the conversation
{: #dialog-start-welcome}

The Welcome node is defined by using the `welcome` special condition, which is triggered when the assistant, rather than the user, starts the conversation. This happens when the integration or client application starts the session with an empty message and then waits for the assistant to greet the user, as in the following situations:

- *Preview* for the assistant
- "Try it out" pane
- *Web chat* integration with home screen disabled

However, the Welcome node is skipped in situations when the user initiates the conversation by sending a message, such as with the *Slack* and *Facebook* integrations. It is also skipped when the *Web chat* integration is used with the home screen enabled because in this situation the home screen provides the greeting. The home screen is enabled by default.

Unlike the `welcome` special condition, the `conversation_start` special condition is always triggered at the start of a conversation. You can use a combination of nodes with these two special conditions (`welcome` and `conversation_start`) to manage the start of your dialog in a consistent way.

For more information, see [Special conditions](/docs/watson-assistant?topic=watson-assistant-dialog-overview#dialog-overview-special-conditions).

### Setting initial context
{: #dialog-start-set-context}

If you need to set initial context variables at the beginning of each conversation, make sure you do so in a way that works with all of the integrations you plan to use. Do not use the Welcome node to set initial context variables unless you are certain your dialog isaccessed only in situations where the `welcome` special condition is triggered.

A safer and more consistent approach is to always set any initial context in a node that is defined by using the `conversation_start` special condition, which is always triggered. You can use this node in addition to a Welcome node that displays a greeting.

To manage the start of any conversation regardless of integration, follow these steps:

1.  Add a dialog node above the Welcome node that is automatically added to the top of the dialog tree when you create the dialog.

1.  Set the node condition for this newly added node to `conversation_start`. This node is reliably triggered at the beginning of any conversation.

1.  In the `conversation_start` node, define any default values for context variables, and call any webhooks that you need to call at the beginning of every conversation.

1.  Do not define a text response for this node. Instead, configure this node to jump to the `Welcome` node directly below it in the dialog tree (or whichever other node you want to process first), and choose **If assistant recognizes (condition)**.

![Screenshot of the dialog tree with a conversation_start node jumping to a welcome node below it.](images/dialog-start.png){: caption="Dialog tree" caption-side="bottom"}

This design results in a dialog that works like this:

- Whatever the integration type, the `conversation_start` node is processed, which means any context variables that you define in it are initialized.
- In integrations where the assistant starts the dialog flow, the `Welcome` node is triggered and its text response is displayed.
- In integrations where the user starts the dialog flow, the user's first input is evaluated and then processed by the node that can provide the best response.

## Ending the conversation gracefully
{: #dialog-start-anything-else}

The *Anything else* node is designed to recognize the `anything_else` special condition, which understands when user input does not match any of the intents that are used as conditions in a dialog's nodes.

Don't delete the *Anything else* node. 

You might not recognize its value at first, but it serves some important functions. If you do delete it, don't panic. You can add it back as a dialog node at the end of your dialog tree, and add the `anything_else` special condition to its *If assistant recognizes* field.

The *Anything else* node provides the following benefits:

- It prevents your assistant from ever going silent and failing to respond at all to your customers. The *Anything else* node is what enables your assistant to (if nothing else) say, `I'm sorry, I didn't understand.` or `I can't help you with that.`

- Analytics uses this node to learn about the topics that your dialog can't address. The *coverage metric* looks for occurrences of nodes with the `anything_else` condition processed in the user conversation logs. It uses this information to determine the frequency with which your dialog is able to match user requests to intents that can address them. The node is registered by the metric if it conditions on `anything_else` alone or when used in combination with another condition, such as `anything_else && #positive_feedback`.

- If you want your assistant to redirect queries to the search integration when the dialog is unable to address them, this node recognizes when it's time to initiate the search. It's when a customer's message reaches the `anything_else` node that the message is sent to the search integration to find a relevant answer in your configured data collections. For more information, see [Search trigger](https://github.com/ibm-cloud-docs/watson-assistant/blob/master/search-integration-enhancement.md#search-trigger){: external}.

   Messages that trigger search in this way are still registered by the coverage metric as messages that are *not* covered.
   {: note}
