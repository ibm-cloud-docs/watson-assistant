---

copyright:
  years: 2018, 2025
lastupdated: "2025-01-03"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Overview: Editing actions
{: #build-actions-overview}

If you're looking for the AI Assistant Builder documentation, see [Building AI Assistants](https://www.ibm.com/docs/watsonx/watson-orchestrate/current?topic=building-ai-assistants-ai-assistant-builder).{: note}

Like a human personal assistant, the assistant you build helps your customers complete tasks and answer questions. You build your assistant by defining actions.
{: shortdesc}

An _action_ represents a discrete outcome that you want your assistant to be able to accomplish in response to a user's request. An action comprises the interaction between a customer and the assistant about a particular question or request. This interaction begins with the user input that starts the action (for example, `I want to withdraw money`). It might then include more exchanges as the assistant gathers more information, and it ends when the assistant carries out the request or answers the customer's question.

## Creating and editing an action
{: #build-actions-overview-create}

To see how actions work and how you build one, let's go through an example.

When you create a new action from scratch, {{site.data.keyword.conversationshort}} prompts you for an example of the customer input that starts the action. This text is also used as the default name for the action, but you can edit the action name later. Also, each action must have a unique name, so make sure you're not adding an example that duplicates an existing action name.

![New action ](images/new-action-prompt.png){: caption="New action" caption-side="bottom"}

Type `I want to withdraw money` and then click **Save** to create the action.

Initially, you need to specify only one example of typical user input that starts the action. You can add more examples of user input later. For more information, see [Understanding your users' questions or requests](/docs/watson-assistant?topic=watson-assistant-understand-questions).
{: tip}

## Visualizing the flow of the action
{: #build-actions-visual-flow}

After you created an action, you have the option to switch between the **Edit** tab and the **Visualization** tab. By choosing the visualization tab you can view the flow chart of the action.

![Editor](images/editor_tab.png){: caption="Editor" caption-side="bottom"}

While you are viewing the flow chart of the action, you are able to zoom and pan around the canvas.

![Visualization](images/visual_tab.png){: caption="Visualization" caption-side="bottom"} 

## Using the action editor
{: #build-actions-overview-use}

After you create the action, the action editor opens.

![Action editor showing newly created action](images/action-editor-new-action.png){: caption="Action editor" caption-side="bottom"}

The editor window shows the parts of an action:

- The **Customer starts with:** tile shows the customer input that starts the action. You can click this tile to edit the example text or add more examples, but we'll leave it as is for now.

- Under **Conversation steps**, you can see the steps that make up the action. A step is an interaction between the assistant and the customer; steps are executed in order, from first to last. You can reorder the steps in an action by clicking and dragging steps in the list.

- The **Preview** button opens a pane that shows you how the assistant responds to customer input. You can preview the assistant at any time to see the effect of changes you make.

- The **Action notes** icon opens an area where you can add a description, documentation, comments, or any other annotations to help you track your work as you build an action.

The action editor supports basic Markdown syntax.
{: tip}

## Steps
{: #build-actions-overview-steps}

An action consists of one or more _steps_. The steps in an action define the conversation turns that follow the initial customer input that triggered the action. In a simple case, a step might consist of a direct answer to a question from the customer; for example, if the customer asks `What are your business hours?`, a one-step action might reply with `We are open Monday through Friday from 9 AM to 5 PM.`.

More commonly, though, an action requires multiple steps to fully understand the customer's request. For our `I want to withdraw money` example, we need more information:

- Which account should the money come from?
- What is the amount to withdraw?

Each of these follow-up questions represents a step in the action.

### Editing a step
{: #build-actions-overview-edit-step}

Within a step, you define the following things:
- A step title that describes what the step does. The step title is optional.
- Any conditions that determine whether the step is processed at run time. (By default, a step is always processed if the user input matches.)
- What the assistant says to the customer when the step is processed.
- Rules for how the customer can reply to what the assistant says (if any response is expected).
- What to do after the step finishes.

![Action editor showing parts of a step](images/action-editor-step-parts.png){: caption="Step" caption-side="bottom"}

Let's edit step 1 to find out which account the customer wants to withdraw money from:
1. Click the **Edit step title** icon and enter the title **Determine account**.

1. In the **Is taken** field, use the default value of **without conditions**. This step is always required for any withdrawal.

1. In the **Assistant says** field, type `Withdraw from which account?`.

1. Click **Define customer response**.

    ![Defining the customer response for a step](images/action-editor-define-response.png){: caption="Define customer response" caption-side="bottom"}

    Because we are asking the user to select from a list of predefined choices, click **Options**. The Edit Response window opens.

1. In the **Option 1** field, type `Savings`. As soon as you enter a value for option 1, a field appears for option 2.

    ![Editing an Options response](images/action-editor-edit-options-response.png){: caption="Edit response" caption-side="bottom"}

    Click **Option 2** and type `Checking`.

    Click **Apply** to save the customer response.

1. Now we can check that the step works like we expect. Click **Preview** to open the Preview pane, and type `I want to withdraw money`:

    ![Previewing action with one step](images/action-preview-one-step.png){: caption="Preview" caption-side="bottom"}

    As expected, the assistant now prompts you to select the account you want to withdraw money from.

### Duplicating a step
{: #build-actions-overview-duplicate-step}

You can duplicate a step so you don't have to re-create variable settings and customizations. Duplicating a step is helpful when you need to add a step similar to a previous step, but with minor modifications.

Complete the following steps to duplicate a step:

1. Click the **Duplicate** icon on the step that you want to duplicate.

    ![Duplicate button on a step](images/action-editor-duplicate-button.png){: caption="Duplicate icon" caption-side="bottom"}

    A step appears immediately following the step that you duplicated. This step is identical to the duplicated step and displays a blue circle in the upper right to indicate that the step is a duplicate.

    ![Duplicated step](images/action-preview-duplicate-step.png){: caption="Duplicated step" caption-side="bottom"}

1. Edit the information in the new step as necessary.

### Adding conditional steps
{: #build-actions-overview-conditional-steps}

Suppose our bank charges a fee for withdrawals from checking accounts, and we need to confirm that the customer understands. Our action needs to have slightly different behavior depending on which kind of account the customer selects. We can handle this using step conditions.

When a step asks for information from the user, the user's response is stored as an _action variable_. By referring to the action variables stored by previous steps, you can construct step conditions based on your customer's previous responses.

1. Click **New step**.

1. In the **Step 2 is taken** field, select **with conditions**. The **Conditions** section expands.

    ![Action editor: specifying conditions](images/action-editor-conditions.png){: caption="Conditions" caption-side="bottom"}

1. By default, a condition is automatically created based on the action variable that is stored by the previous step (`Withdraw from which account?`). However, by default it is checking for a value of `Savings`, which is not what we want. Click the value field and select `Checking` instead.

    ![Editing a condition to select Checking as the value to check for](images/action-condition-edit.png){: caption="Edit condition" caption-side="bottom"}

1. In the **Assistant says** field, type `Withdrawals from checking accounts might incur a fee. Do you want to continue?`

1. Click **Define customer response** and select **Confirmation**, which has the choices `Yes` and `No`. 

    Click **Apply** to save the customer response.

1. Because we want to make sure the customer always agrees explicitly, click the **Settings** icon to open **Customer response settings**, then select **Always ask for this information, regardless of earlier messages**.

    ![Customer response settings](images/action-editor-customer-response-settings.png){: caption="Customer response settings" caption-side="bottom"}

Now we need another conditional step to handle the situation where the customer decides not to continue.

1. Click **New step**.

1. In the **Step 3 is taken** field, select **with conditions**.

1. Edit the condition so it checks that the customer's response to step 2 was `No`.

    ![Action editor: specifying conditions](images/action-editor-conditions-2.png){: caption="Edit conditions" caption-side="bottom"}

1. In the **Assistant says** field, type `Canceling transaction.`.

1. In the **And then** field, select **End the action**. If this step is executed (meaning that the customer decides not to proceed), no subsequent steps in the action are executed.

We don't need a conditional step to handle a response of `Yes` in step 2 because in that situation processing just continues as normal.
{: note}

### Getting the amount
{: #build-actions-overview-get-amount}

We need one more piece of information before we can complete the customer's request: the amount of money to withdraw.

1. Click **New step**.

1. In the **Assistant says** field, type `How much do you want to withdraw?`.

1. Click **Define customer response**. We need the customer to specify a monetary amount, so select **Currency**. 

### Finishing the action
{: #build-actions-overview-finish-action}

We now have all the information that we need. For our example, we're not going to implement any real logic for making a withdrawal, but we can send a final message to summarize what we're doing.

To do this summary, we need to insert action variables (representing customer responses from previous steps) into our response. At run time, these action variables are replaced with the actual values that are supplied by the customer.

1. Click **New step**.

1. Now we need to build a confirmation message that says "OK, we will withdraw *amount* from your *account_type* account."

    To create this response, type the text of the message in the **Assistant says** field, but in place of the variable values, click the **Insert a variable** ![Action variable icon](images/function-math.svg) icon to insert references to action variables:

    - For *amount*, select **4. How much do you want to withdraw?**.
    - For *account_type*, select **1. Withdraw from which account?**.

    ![Action editor: message including variable references](images/action-editor-message-with-variables.png)

1. Because this is the last step in the action, you don't need to specify any customer response.

If you decide a step is no longer needed, you can delete it from the action. To delete a step, click the **Delete** ![Delete step icon](../../icons/delete.svg) icon on the tile for the step.
{: tip}

## Testing the action
{: #build-actions-overview-test}

We can now test the action to make sure it's working. Click **Preview** to open the Preview pane. (If the text from a previous test is still shown, click the **Refresh** ![Preview refresh icon](../../icons/restart.svg) icon to restart the conversation.)

Start by typing `I want to withdraw money`. Try various permutations of your input to test how the assistant behaves:

- Try selecting both `Savings` and `Checking`. Confirm that if you select `Checking`, the assistant warns you about incurring a fee and asks if you want to continue, but if you select `Savings`, it proceeds without the warning.

- When you select `Checking`, try both responses when the assistant asks if you want to continue. Confirm that if you select `No`, the action ends.

- Try including additional information in your initial message. For example, try typing `I want to withdraw $50 from my savings account`. Confirm that the assistant does not ask you again to specify the information you already provided.

That's it! You built a simple action that includes multiple steps, collects information that it stores as action variables, and conditions its responses based on what your customer chooses. There is a lot more you can do with actions, but all of it is built on this basic pattern.

## Action limits
{: #build-actions-limits}

The number of actions, steps, and variables you can create depends on your {{site.data.keyword.conversationshort}} [plan type](https://www.ibm.com/products/watsonx-assistant/pricing){: external}.

| Plan | Actions | Steps | Variables |
|---|---:|---:|---:|
| Lite | 100 | 1,000 | 2,000 |
| Trial | 100 | 1,000 | 2,000 |
| Plus | 2,000 | 5,000 | 8,000 |
| Enterprise | 2,000 | 5,000 | 8,000 |
| Enterprise with Data Isolation | 2,000 | 5,000 | 8,000 |
{: caption="Plan details" caption-side="top"}
