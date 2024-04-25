---

copyright:
  years: 2018, 2024
lastupdated: "2024-04-25"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}



# Calling actions from a dialog
{: #dialog-call-action}

This feature is currently not available in the AI assistant builder of IBM watsonx Orchestrate.{: note}

In {{site.data.keyword.conversationshort}}, you can use actions with your primary dialog conversation. A dialog feature takes precedence over actions. You can use actions to supplement a dialog-based conversation, but the dialog drives the conversation with users to match their requests.

A dialog node calls an action to perform a task and then return to the dialog. From a single dialog node, you can make a call to either a webhook or an action, not both. Choose the approach that best suits your needs:

- Call an action if you want to perform a discrete and self-contained task, and then return to the dialog to be ready to address any new user requests. Data collected from the user during action processing must be stored as a session variable for it to be passed to the dialog.

- Call a webhook if you want to send a request to a web service to complete a task and return a response that can be used later by this dialog. For more information, see [Extending your assistant with webhooks](/docs/watson-assistant?topic=watson-assistant-webhook-overview). 

## When to call an action from a dialog
{: #dialog-call-action-when}

You might want to call an action from a dialog in the following scenarios:

- You want to perform an action from multiple dialog threads. 

    For example, you want to ask customers how satisfied they are with your service. You can define a single action to check customer satisfaction and call it from multiple branch-ending dialog nodes.

    In this scenario, you don't need to define an intent, such as `#check_satisfaction`. The action is called automatically, replacing a jump to another dialog node's response.

- You want to see how actions works. 

    In this scenario, you can pick an intent for the action to handle. If you plan for the action to be called from the dialog only, you can spend your time defining the user examples for the intent that triggers the dialog node. When you define the action, you can add one customer example only, reducing the time you need to spend building the action.

## Adding a call to an action
{: #dialog-call-action-add}

Before you start, open the **Actions** page and check the following:

- The name of the action you want to call. 

- If the action you want to call uses a session variable, and you want to pass a value to the action by setting the session variable value, make a note of the session variable's ID.

    In the Variables section, click to open the session variable. You can see the syntax that is used for the variable name in the **ID** field. Copy the variable ID to the clipboard. 
  
    You also need to understand the type of value to assign to the session variable. If you don't know, check how the session variable is used by the action.

To call an action from a dialog node:

1.  From the dialog node, click **Customize**.

1.  Set **Call out to webhooks / actions** to **On**.

1.  Select **Call an action**.

    When you add a call to an action, multiple conditional responses are enabled for the dialog node automatically.

1.  Click **Apply**. 

1. In the dialog node, choose the action you want to call.

1.  **Optional**: If the action you want to call uses a session variable, you can set the value of the session variable when the action is started.

    In the **Parameters** section, add a key and value pair to pass with the call to the action.

    Add the variable ID (that you copied to the clipboard earlier) to the **Key** field, and in the **Value** field, specify the value that you want to set the variable to.
    
    For example, let's say the action has a session variable named `given name`. You can pass the current user's given name (which you asked for and saved to a `$name` context variable) to the action as follows:

    | Key | Value |
    | --- | --- |
    | `given_name` | `"$name"` |
    {: caption="Action call key and value pair example}

1.  If you call actions from more than one dialog node, change the name of the return variable to make it unique across all of your dialog nodes. For example, you might already call an action and its return variable is called `$action_result_1`, so you can name the new one `$action_result_2`.

    The return variable is a context variable that is automatically created. It stores any session variable values that are created or have their values changed while the called action is processed.

1.  In the **Assistant responds** section, the condition for the first conditional response is populated automatically with the return variable from the action call.

    The return variable is named `$action_result_1` unless you change the name. 
    
    If any session variables are created or have their values changed by the called action, then they are returned and stored in the result variable as a JSON object. 

    For example, if the action changes the value of the `given name` and `membership status` session variables, the following JSON object is returned:

    ```json
    {"given_name":"Sally","membership_status":"true"}
    ```
    {: codeblock}

1.  If you don't send or change any session variables, you can delete the first conditional response. Otherwise, consider adding a response to show when a return variable is sent from the called action.

    You might want to specify a custom response to show in case the exchange that took place when the action was processed resulted in a change to the value of the session variable that you passed to the action.
    
    For example, let's say that the dialog asks for the person's given name and stores it in the `$name` context variable. The dialog then passes the name to the action as a `given_name` session variable. Then, the action that is called asks if the customer prefers that the assistant use a nickname. The action then replaces the value that was stored in the `given_name` session variable with the nickname that the customer submitted.

    To continue with this example, you might want to address the user by the preferred nickname, now that you know it. You can add a response that says, `Thanks for your business, <? $action_result_1.given_name ?>!` The `<? $action_result_1.given_name ?>` expression extracts the value of the `given_name` session variable that is returned from the called action.

1.  Add a response to show when no return variable is provided as the second conditional response.

    The second response that is added automatically for you has an `anything_else` condition. This response is shown if none of the other conditional responses are displayed. 

    You can delete or edit the conditional responses that are added automatically. You can add more conditional responses and reorder them.

1.  Click **X** to close the dialog node. Your changes are saved automatically.

1. Use the **Preview** page to test the interaction between the dialog and the action.



