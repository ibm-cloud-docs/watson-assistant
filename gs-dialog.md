---

copyright:
  years: 2015, 2023
lastupdated: "2023-08-23"

subcollection: watson-assistant
content-type: tutorial
account-plan: lite
completion-time: 10m

---

{{site.data.keyword.attribute-definition-list}}
 
# Getting started with dialog
{: #gs-dialog}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

In this short tutorial, we help you use a dialog to build your first conversation.
{: shortdesc}

A *dialog* uses natural language processing and machine learning technologies to understand user questions and requests, and respond to them with answers that are authored by you.

## Add intents from a content catalog
{: #gs-dialog-add-catalog}
{: step}

The Intents page is where you start to train your assistant. In this tutorial, you will add training data that was built by IBM to your skill. Prebuilt intents are available from the content catalog. You will give your assistant access to the **General** content catalog so your dialog can greet users, and end conversations with them.

1.  Click **Content Catalog**.

1.  Find **General** in the list, and then click **Add content**.

    ![Shows the Content Catalog and highlights the Add to skill button for the General catalog.](images/gs-add-content-catalog.png){: caption="Content Catalog" caption-side="bottom"}

1.  Open the **Intents** tab to review the intents and associated example utterances that were added to your training data. You can recognize them because each intent name begins with the prefix `#General_`. You will add the `#General_Greetings` and `#General_Ending` intents to your dialog in the next step.

    ![Shows the intents that are displayed in the Intents tab after the General catalog is added.](images/gs-general-content-added.png){: caption="Intents" caption-side="bottom"}

You successfully started to build your training data by adding prebuilt content from {{site.data.keyword.IBM_notm}}.

## Build a dialog
{: #gs-dialog-build-dialog}
{: step}

A *dialog* defines the flow of your conversation in the form of a logic tree. It matches intents (what users say) to responses (what your virtual assistant says back). Each node of the tree has a condition that triggers it, based on user input.

We'll create a simple dialog that handles greeting and ending intents, each with a single node.

### Adding a start node
{: #gs-adding-a-start-node}

1. Click **Dialog**.

    The following two dialog nodes are created for you automatically:

    - **Welcome**: Contains a greeting that is displayed to your users when they first engage with the assistant.
    - **Anything else**: Contains phrases that are used to reply to users when their input is not recognized.

    ![A new dialog with two built-in nodes](images/gs-new-dialog.png){: caption="New dialog with built-in nodes" caption-side="bottom"}

1.  Click the **Welcome** node to open it in the edit view.

1.  Replace the default response with the text, `Welcome to the Watson Assistant tutorial!`.

    ![Editing the welcome node response](images/gs-edit-welcome-node.png){: caption="Welcome node" caption-side="bottom"}

1.  Click ![Close](images/close.png) to close the edit view.

You created a dialog node that is triggered by the `welcome` condition. (`welcome` is a special condition that functions like an intent, but does not begin with a `#`.) It is triggered when a new conversation starts. Your node specifies that when a new conversation starts, the system should respond with the welcome message that you add to the response section of this first node.

### Testing the start node
{: #gs-testing-the-start-node}

You can test your dialog at any time to verify the dialog. Let's test it now.

- Click the ![Try it](images/try-it.png) button to open the *Try it out* pane. You should see your welcome message.

### Adding nodes to handle intents
{: #gs-adding-nodes-to-handle-intents}

Now let's add nodes between the `Welcome` node and the `Anything else` node that handle our intents.

1.  Click **Add node**.

1.  In the node name field, type `Greet customers`.

1.  In the **If assistant recognizes** field of this node, start to type `#General_Greetings`. Then, select the **`#General_Greetings`** option.

1.  Add the response text, `Good day to you!`

    ![Editing the general greeting node.](images/gs-add-greeting-node.png){: caption="Greeting node" caption-side="bottom"}

1.  Click ![Close](images/close.png) to close the edit view.

1.  Click **Add node** to create a peer node. 

1.  Name the peer node `Say goodbye` and specify `#General_Ending` in the **If assistant recognizes** field. 

1.  Add `OK. See you later.` as the response text.

    ![Editing the general ending node.](images/gs-add-ending-node.png){: caption="Ending node" caption-side="bottom"}

1.  Click ![Close](images/close.png) to close the edit view.

### Testing intent recognition
{: #gs-testing-intent-recognition}

You built a simple dialog to recognize and respond to both greeting and ending inputs. Let's see how well it works.

1.  Click the ![Try it](images/try-it.png) button to open the "Try it out" pane.

1.  In the text field, type `Hello` and then press Enter. The output indicates that the `#General_Greetings` intent was recognized, and the appropriate response (`Good day to you.`) is displayed.

1.  Try the following input:
    - `bye`
    - `howdy`
    - `see ya`
    - `good morning`
    - `sayonara`

    ![Testing the dialog in the Try it out pane](images/gs-try-it.mp4){: video controls loop}

    {{site.data.keyword.conversationshort}} can recognize your intents even when your input doesn't exactly match the examples that you included. The dialog uses intents to identify the purpose of the user's input regardless of the precise wording used, and then responds in the way you specify.

### Result of building a dialog
{: #gs-result-of-building-a-dialog}

That's it. You created a simple conversation with two intents and a dialog to recognize them.

## Next steps
{: #gs-dialog-next-steps}

This tutorial is built around a simple example. For a real application, you need to define some more interesting intents, some entities, and a more complex dialog that uses them both. When you have a polished version of the assistant, you can integrate it with web sites or channels, such as Slack, that your customers already use. As traffic increases between the assistant and your customers, you can use the tools that are provided in the **Analytics** page to analyze real conversations, and identify areas for improvement.

