---

copyright:
  years: 2015, 2023
lastupdated: "2023-10-27"

keywords: context, context variable

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Personalizing the dialog with context
{: #dialog-runtime-context}

To personalize the conversation, your assistant can collect information from the customer and then refer to it later in the conversation.
{: shortdesc}

## Retaining information across dialog turns
{: #dialog-runtime-context-dialog}

The dialog is stateless, meaning that it does not retain information from one interaction with the user to the next. When you add a dialog to an assistant and deploy it, the assistant saves the context from one message call, and then resubmits it on the next request throughout the current session. The current session lasts while a user interacts with the assistant plus the designated session inactivity time frame. The maximum session inactivity time allowed ranges from 5 minutes to 7 days, depending on your plan type. If you do not add the dialog to an assistant, it is your responsibility as the custom application developer to maintain any continuing information that the application needs.

The application can pass information to the dialog, and the dialog can update this information and pass it back to the application, or to a subsequent node. The dialog does so by using *context variables*.

## Context variables
{: #dialog-runtime-context-variables}

A context variable is a variable that you define in a node. You can specify a default value for it. Then, other nodes, application logic, or user input can set or change the value of the context variable.

You can condition against context variable values by referencing a context variable from a dialog node condition to determine whether to execute a node. You can also reference a context variable from dialog node response conditions to show different responses depending on a value that is provided by an external service or by the user.

Learn more:

- [Passing context from the application](#dialog-runtime-context-from-app)
- [Passing context from node to node](#dialog-runtime-context-node-to-node)
- [Defining a context variable](#dialog-runtime-context-var-define)
- [Common context variable tasks](#dialog-runtime-context-common-tasks)
- [Deleting a context variable](#dialog-runtime-context-delete)
- [Updating a context variable](#dialog-runtime-context-update)
- [How context variables are processed](#dialog-runtime-context-processing)
- [Order of operation](#dialog-runtime-context-order-of-ops)
- [Adding context variables to a node with slots](#dialog-runtime-context-var-slots)

### Passing context from the application
{: #dialog-runtime-context-from-app}

Pass information from the application to the dialog by setting a context variable and passing the context variable to the dialog.

For example, your application can set a $time_of_day context variable, and pass it to the dialog that can use the information to tailor the greeting it shows to the user.

![Shows a Welcome node that uses response conditions to check for the value of the $time_of_day context variable that is passed to the dialog from the application.](images/set-context.png){: caption="Time of day context" caption-side="bottom"}

In this example, the dialog knows that the application sets the variable to one of these values: *morning*, *afternoon*, or *evening*. It can check for each value, and depending on which value is present, return the appropriate greeting. If the variable is not passed or has a value that does not match one of the expected values, then a more generic greeting is displayed to the user.

### Passing context from node to node
{: #dialog-runtime-context-node-to-node}

The dialog can also add context variables to pass information from one node to another or to update the values of context variables. As the dialog asks for and gets information from the user, it can track the information and reference it later in the conversation.

For example, in one node you might ask users for their name, and in a later node address them by name.

![Shows an introductions node that asks the user for their name, and stores it as a context variable. The next node refers to the user by name by using the $username context variable.](images/set-context-username.png){: caption="Pass context from one node to another" caption-side="bottom"}

In this example, the system entity @name is used to extract the user's name from the input if the user provides one. In the JSON editor, the username context variable is defined and set to the @name value. In a subsequent node, the $username context variable is included in the response to address the user by name.

### Defining a context variable
{: #dialog-runtime-context-var-define}

Define a context variable by adding the variable name to the **Variable** field and adding a default value for it to the **Value** field in the node's edit view.

1.  Click to open the dialog node to which you want to add a context variable.

1.  Go to the *Assistant responds* section and click the menu icon ![Overflow menu icon](images/overflow-menu--vertical.svg).

1.  Click **Open context editor**.

1.  Add the variable name and value pair to the **Variable** and **Value** fields.

    - The `name` can contain any upper- and lowercase alphabet characters, numeric characters (0-9), and underscores.

    - The `value` can be any supported JSON type, such as a simple string variable, a number, a JSON array, or a JSON object.

The following table shows some examples of how to define name and value pairs for different types of values:

| Variable | Value | Value Type |
| --- | --- | --- |
| dessert | "cake" | String |
| age | 18 | Number |
| toppings_array | `["onions","olives"]` | JSON Array |
| full_name | `{"first":"John","last":"Doe"}` | JSON Object |
{: caption="Define name and value pairs" caption-side="bottom"}

Then, to refer to these context variables, use the syntax `$name` where *name* is the name of the context variable that you defined.

For example, you might specify the following expression as the dialog response:

`The customer, $age-year-old <? $full_name.first ?>, wants a pizza with <? $toppings_array.join(' and ') ?>, and then $dessert.`

The resulting output is displayed as follows:

`The customer, 18-year-old John, wants a pizza with onions and olives, and then cake.`

You can use the JSON editor to define context variables also. You might prefer to use the JSON editor if you want to add a complex expression as the variable value. See [Context variables in the JSON editor](#dialog-runtime-context-var-json) for more details.

### Common context variable tasks
{: #dialog-runtime-context-common-tasks}

To store the entire string that was provided by the user as input, use `input.text`:

| Variable | Value |
| --- | --- |
| repeat | `<?input.text?>` |
{: caption="Capturing user input" caption-side="bottom"}

For example, the user input might be, `I want to order a device.` If the node response is, `You said: $repeat`, then the response would be displayed as, `You said: I want to order a device.`

To store the value of an entity in a context variable, use this syntax:

| Variable | Value |
| --- | --- |
| place | `@place` |
{: caption="Capturing an entity mention" caption-side="bottom"}

For example, the user input might be, `I want to go to Paris.` If your `@place` entity recognizes `Paris`, then your assistant saves `Paris` in the `$place` context variable.

To store the value of a string that you extract from the user's input, you can include a SpEL expression that uses the `extract` method to apply a regular expression to the user input. The following expression extracts a number from the user input, and saves it to the `$number` context variable.

| Variable | Value |
| --- | --- |
| number   | `<?input.text.extract('[\d]+',0)?>` |
{: caption="Using a String method" caption-side="bottom"}

To store the value of a pattern entity, append .literal to the entity name. Using this syntax make sure that the exact span of text from user input that matched the specified pattern is stored in the variable.

| Variable | Value |
| --- | --- |
| email | `<? @email.literal ?>` |
{: caption="Capturing a pattern entity value" caption-side="bottom"}

For example, the user input is `Contact me at joe@example.com.` Your entity that is named `@email` recognizes the `name@domain.com` email format. By configuring the context variable to store `@email.literal`, you indicate that you want to store the part of the input that matched the pattern. If you omit the `.literal` property from the value expression, then the entity value name that you specified for the pattern is returned instead of the segment of user input that matched the pattern.

### Deleting a context variable
{: #dialog-runtime-context-delete}

To delete a context variable, set the variable to null.

| Variable | Value |
| --- | --- |
| order_form | `null` |
{: caption="Nulling a context variable" caption-side="bottom"}

### Updating a context variable value
{: #dialog-runtime-context-update}

To update a context variable's value, define a context variable with the same name as the previous context variable, but this time, specify a different value for it.

When more than one node sets the value of the same context variable, the value for the context variable can change over the course of a conversation with a user. The value that is applied depends on which node is being triggered by the user in the course of the conversation. The value specified for the context variable in the last node that is processed overwrites any values that were set for the variable by nodes that were processed previously.

For information about how to update the value of a context variable when the value is a JSON object or JSON array data type, see [Updating a context variable value in JSON](#dialog-runtime-context-update-json)

### How context variables are processed
{: #dialog-runtime-context-processing}

Where you define the context variable matters. The context variable is not created and set to the value that you specify for it until your assistant processes the part of the dialog node where you defined the context variable. In most cases, you define the context variable as part of the node response. When you do so, the context variable is created and given the specified value when your assistant returns the node response.

For a node with conditional responses, the context variable is created and set when the condition for a specific response is met and that response is processed. For example, if you define a context variable for conditional response #1 and your assistant processes response #2, then the variable that you defined for conditional response #1 is not set.

For information about adding context variables that you want your assistant to set as a user interacts with a node with slots, see [Adding context variables to a node with slots](#dialog-runtime-context-var-slots).

### Order of operation
{: #dialog-runtime-context-order-of-ops}

When you define multiple variables to be processed together, the order in which you define them does not determine the order in which they are evaluated by your assistant. Your assistant evaluates the variables in random order. Don't set a value in the first context variable and expect to use it in the second variable because the first context variable might not be executed before the second one. For example, do not use two context variables to implement logic that checks whether the user input contains the word `Yes` in it.

| Variable | Value |
| --- | --- |
| user_input | `<? input.text ?>` |
| contains_yes | `<? $user_input.contains('Yes') ?>` |
{: caption="Using two context variables to check for a value in user input" caption-side="bottom"}

Instead, use a slightly more complex expression to avoid having to rely on the value of the first variable in your list (user_input) being evaluated before the second variable (contains_yes) is evaluated.

| Variable | Value |
| --- | --- |
| contains_yes  | `<? input.text.contains('Yes') ?>` |
{: caption="Using a single context variable" caption-side="bottom"}

### Adding context variables to a node with slots
{: #dialog-runtime-context-var-slots}

For more information about slots, see [Gathering information with slots](/docs/watson-assistant?topic=watson-assistant-dialog-slots).

To add a context variable that is processed after a response condition for a slot is met:

1. Open the node with slots in the edit view.
1.  Click the **Customize slot** icon ![Customize slot](images/slot-icon.svg).
1.  Click the **Options** icon ![Options](images/overflow-menu--vertical.svg), and then select **Enable condition**.
1.  Click the **Customize handler** icon ![Edit slot](images/slot-icon.svg) next to the response with which you want to associate the context variable.
1.  Click the **Options** icon ![Options](images/overflow-menu--vertical.svg) in the Assistant responds section, and then click **Open context editor**.
1.  Add the variable name and value pair to the **Variable** and **Value** fields.

To add a context variable that is set or updated after a slot condition is met, complete the following steps:

1. Open the node with slots in the edit view.
1.  Click the **Customize slot** icon ![Customize slot](images/slot-icon.svg).
1.  Click the **Options** icon ![Options](images/overflow-menu--vertical.svg), and then select **Enable condition**.
1.  Add the variable name and value pair in JSON format.

   ```json
   {
   "time_of_day": "morning"
   }
   ```
   {: codeblock}

   You can't use the context editor to define context variables that are set during this phase of dialog node evaluation. You must use the JSON editor instead. For more information about using the JSON editor, see [Context variables in the JSON editor](#dialog-runtime-context-var-json).
   {: note}

## Context variables in the JSON editor
{: #dialog-runtime-context-var-json}

You can also define a context variable in the JSON editor. Use the JSON editor if you are defining a complex context variable and want to be able to see the full SpEL expression as you add or change it.

The name and value pair must meet these requirements:

- The `name` can contain any upper- and lowercase alphabet characters, numeric characters (0-9), and underscores.

   You can include other characters, such as periods and hyphens, in the name. However, if you do, then you must specify the shorthand syntax `$(variable-name)` every time you reference the variable. See [Expressions for accessing objects](/docs/watson-assistant?topic=watson-assistant-expression-language#expression-language-shorthand-syntax) for more details.
   {: tip}

- The `value` can be any supported JSON type, such as a simple string variable, a number, a JSON array, or a JSON object.

The following JSON sample defines values for the $dessert string, $toppings_array array, $age number, and $full_name object context variables:

```json
{
  "context": {
    "dessert": "cake",
    "toppings_array": [
      "onions",
      "olives"
    ],
    "age": 18,
    "full_name": {
      "first": "Jane",
      "last": "Doe"
    }
  },
  "output":{}
}
```
{: codeblock}

To define a context variable in JSON format, complete the following steps:

1.  Click to open the dialog node to which you want to add the context variable.

    Any existing context variable values that are defined for this node are displayed in a set of corresponding **Variable** and **Value** fields. If you do not want them to be displayed in the edit view of the node, you must close the context editor. You can close the editor from the same menu that is used to open the JSON editor; the following steps describe how to access the menu.
    {: note}

1.  Click the **Options** icon ![Options](images/overflow-menu--vertical.svg) for the assistant response, and then click **Open JSON editor**.

    If the **Multiple conditioned responses** setting is enabled for the node, then you must first click the **Customize response** ![Customize response](images/slot-icon.svg) icon for the response with which you want to associate the context variable.

1.  Add a `"context":{}` block if one is not present.

    ```json
    {
      "context":{},
      "output":{}
    }
    ```
    {: codeblock}

1.  In the context block, add a `"name"` and `"value"` pair for each context variable that you want to define.

    ```json
    {
      "context":{
        "name": "value"
    },
      "output": {}
    }
    ```
    {: codeblock}

    In this example, a variable that is named `new_variable` is added to a context block that already contains a variable.

    ```json
    {
      "context":{
        "existing_variable": "value",
        "new_variable":"value"
      }
    }
    ```
    {: codeblock}

    To reference the context variable, use the syntax `$name` where *name* is the name of the context variable that you defined. For example, `$new_variable`.

Learn more:

- [Deleting a context variable in JSON](#dialog-runtime-context-delete-json)
- [Updating a context variable value in JSON](#dialog-runtime-context-update-json)
- [Setting one context variable equal to another](#dialog-runtime-context-var-equals-var)

### Deleting a context variable in JSON
{: #dialog-runtime-context-delete-json}

To delete a context variable, set the variable to null.

```json
{
  "context": {
    "order_form": null
  }
}
```
{: codeblock}

If you want to remove all trace of the context variable, you can use the JSONObject.remove(string) method to delete it from the context object. However, you must use a variable to perform the removal. Define the new variable in the message output so it isn't saved beyond the current call.

```json
{
  "output": {
    "text" : {},
    "deleted_variable" : "<? context.remove('order_form') ?>"
  }
}
```
{: codeblock}

Alternatively you can delete the context variable in your application logic.

### Updating a context variable value in JSON
{: #dialog-runtime-context-update-json}

In general, if a node sets the value of a context variable that is already set, then the previous value is overwritten by the new value.

#### Updating a complex JSON object
{: #dialog-runtime-context-update-json-complex}

Previous values are overwritten for all JSON types except a JSON object. If the context variable is a complex type such as JSON object, a JSON merge procedure is used to update the variable. The merge operation adds any newly defined properties and overwrites any existing properties of the object.

In this example, a name context variable is defined as a complex object.

```json
{
  "context": {
    "complex_object": {
      "user_firstname" : "Paul",
      "user_lastname" : "Pan",
      "has_card" : false
    }
  }
}
```
{: codeblock}

A dialog node updates the context variable JSON object with the following values:

```json
{
  "complex_object": {
    "user_firstname": "Peter",
    "has_card": true
  }
}
```
{: codeblock}

The result is this context:

```json
{
  "complex_object": {
    "user_firstname": "Peter",
    "user_lastname": "Pan",
    "has_card": true
  }
}
```
{: codeblock}

#### Updating arrays
{: #dialog-runtime-context-update-arrays}

If your dialog context data contains an array of values, you can update the array by appending values, removing a value, or replacing all the values.

Choose one of these actions to update the array. In each case, we see the array before the action, the action, and the array after the action is applied.

- **Append**: To add values to the end of an array, use the `append` method.

    For this dialog runtime context:

    ```json
    {
      "context": {
        "toppings_array": ["onion", "olives"]
      }
    }
    ```
    {: codeblock}

    Make this update:

    ```json
    {
      "context": {
        "toppings_array": "<? $toppings_array.append('ketchup', 'tomatoes') ?>"
      }
    }
    ```
    {: codeblock}

    Result:

    ```json
    {
      "context": {
        "toppings_array": ["onion", "olives", "ketchup", "tomatoes"]
      }
    }
    ```
    {: codeblock}

- **Remove**: To remove an element, use the `remove` method and specify its value or position in the array.

    - **Remove by value** removes an element from an array by its value.

        For this dialog runtime context:

        ```json
        {
          "context": {
            "toppings_array": ["onion", "olives"]
          }
        }
        ```
        {: codeblock}

        Make this update:

        ```json
        {
          "context": {
            "toppings_array": "<? $toppings_array.removeValue('onion') ?>"
          }
        }
        ```
        {: codeblock}

        Result:

        ```json
        {
          "context": {
            "toppings_array": ["olives"]
          }
        }
        ```
        {: codeblock}

    - **Remove by position**: Removing an element from an array by its index position:

        For this dialog runtime context:

        ```json
        {
          "context": {
            "toppings_array": ["onion", "olives"]
          }
        }
        ```
        {: codeblock}

        Make this update:

        ```json
        {
          "context": {
            "toppings_array": "<? $toppings_array.remove(0) ?>"
          }
        }
        ```
        {: codeblock}

        Result:

        ```json
        {
          "context": {
            "toppings_array": ["olives"]
          }
        }
        ```
        {: codeblock}

- **Overwrite**: To overwrite the values in an array, set the array to the new values:

   For this dialog runtime context:

   ```json
   {
     "context": {
       "toppings_array": ["onion", "olives"]
     }
   }
   ```
   {: codeblock}

   Make this update:

   ```json
   {
     "context": {
       "toppings_array": ["ketchup", "tomatoes"]
     }
   }
   ```
   {: codeblock}

   Result:

   ```json
   {
     "context": {
       "toppings_array": ["ketchup", "tomatoes"]
     }
   }
   ```
   {: codeblock}

### Setting one context variable equal to another
{: #dialog-runtime-context-var-equals-var}

When you set one context variable equal to another context variable, you define a pointer from one to the other. Later, if the value of one of the variables changes, then the value of the other variable is changed also.

For example, if you specify a context variable as follows, then when the value of either `$var1` or `$var2` later changes, the value of the other changes too.

| Variable | Value  |
| --- | --- |
| var2 | var1 |
{: caption="Setting one context variable equal to another" caption-side="bottom"}

Do not set one variable equal to another to capture a point in time value. With arrays, if you want to capture an array value that is stored in a context variable and use it later, create a new variable based on the current value of the variable instead.

For example, to create a copy of the values of an array at a certain point, add an array that is populated with the values for the existing array. To do so, you can use the following syntax:

```json
{
"context": {
   "var2": "<? output.var2?:new JsonArray().append($var1) ?>"
 }
 }
 ```
{: codeblock}
