---

copyright:
  years: 2018, 2022
lastupdated: "2022-00-01"

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
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Using variables to manage conversation information
{: #manage-info}

When customers reply to your assistant, they share information about themselves and what they want. Your assistant remembers this information, and other information about a conversation, as *variables*. Your assistant can use variables to provide a more personalized and customized experience, and to get users quickly to the solutions they need.
{: shortdesc}

Variables are a powerful tool you can use to build a better assistant. Variables make possible all of the following benefits:

- **Personalization.** The best virtual assistant experiences are targeted and personalized for each customer. When an assistant greets a customer by saying "Hello, Frank! Welcome back," it tells Frank that it remembers his name and that it has talked to him before. By storing this kind of information in variables and then referencing them in your assistant's output, you can personalize the conversation and help your assistant seem more human.

- **Acceleration.** Over the course of a conversation, your customers will answer questions and make choices. These customer responses are stored as variables, which your assistant can then use to guide a conversation. By choosing the right steps and not wasting your customers' time, you can get them as quickly as possible to the right solution.

- **Modularity.** Some information might be useful for many different purposes (for example, a customer's current account balance or contact information). Rather than retrieving or recalculating this information in multiple locations, you can do so once, using a variable to store the result and then access it wherever you need it.

A variable is simply a named container for a piece of information; by referencing this container by name, your assistant can store or retrieve the information at run time. For example, a variable called *account_balance* might store your customer's current account balance, a value your assistant can update or retrieve as needed.

The data stored by a variable is characterized by the type of data it contains (such as text, a numeric value, a date, or even a list of multiple values); the operations you can perform with a variable vary depending on its data type. <!-- A complex variable can even contain calculations or calls to external services (for more information, see XXXXX). -->

## Action variables and session variables

{{site.data.keyword.conversationshort}} supports two categories of variables:

- **Action variables**: When a step collects information from the customer, the customer response is automatically stored in an *action variable*. You can think of action variables as short-term memory: they persist only for the duration of the current action.

    The name of an action variable is always the name of the step that defines the customer response. (You cannot change the name of an action variable.) For example, suppose you define a step that asks "When were you born?" and accepts a date value as a response. The customer response is automatically stored as an action variable called `When were you born?`, which you can then access from any subsequent step in the same action.

- **Session variables**: A value that is not necessarily tied to a particular action can be stored as a *session variable*. Session variables are long-term memory: they persist throughout the user's interaction with the assistant, and your assistant can reference them from any action.

    You can create a session variable to store the value from an action variable, if you want to keep the value available for other actions to use. You can also define a session variable based on another session variable, or using a value defined in an expression. In addition to variables you create, {{site.data.keyword.conversationshort}} provides a set of built-in session variables for global values like the current time and date.

    Session variables can help you to modularize your assistant, because you can write a single action that collects information needed in multiple places. For example, you might have a greeting action that collects basic information about the customer and stores the responses in session variables, which any action can then access.

    A session variable you create persists only for the duration of a single session. At the end of the session, the variable's value is cleared. How long a session lasts depends upon how your customers access your assistant, and how your assistant is configured. <!-- For more information about sessions, see XXXXX. -->
    {: note}

### Creating a session variable
{: #create-session-variable}

To add a session variable that can be accessed by any action:

1. From the main actions page, click **Variables > Created by you** in the navigation pane. The list shows all session variables you have created for your assistant.

1. Click **New variable**.

    You can also create a new session variable from the step editor. For more information, see [Storing a value in a session variable](#store-session-variable).
    {: tip}

1. In the **Name** field, type a name for the session variable.

    As you add the name, an ID is generated for you. Any spaces in the name are replaced with underscores (_) in the ID.

1. **Optional**: Add a type. This sets the response type of the variable. (For more information about response types, see [Choosing a response type](/docs/watson-assistant?topic=watson-assistant-collect-info#choosing-a-response-type).)

    From this field, you can also select any of the saved responses that you created. For more information about saved responses, see [Saving and reusing customer responses](/docs/watson-assistant?topic=watson-assistant-collect-info#saved-customer-responses).

    In addition to the listed types, a variable can also be created as an array. To create an array variable, select **Any** as the type, and in the next step, define an initial value using the expression `[]` to represent an empty array.

1. **Optional**: Add an initial value. This sets the starting value for the variable at the beginning of each user session. For example, suppose you have an assistant your customers can use to make purchases; you might initialize a *Payment due* variable with a starting value of 0, and then add to that value as the customer orders items.

    To specify a complex object or an array as the initial value, or to calculate the initial value based on other variables, you can write an expression. For more information about writing expression, see [Writing expressions](/docs/watson-assistant?topic=watson-assistant-expressions).)

1. **Optional**: Add a description.

1. Click **Apply**.

### Built-in variables
{: #built-in-variables }

In addition to the variables you create, {{site.data.keyword.conversationshort}} provides a set of built-in variables you can access from any action. At run time, these variables are automatically set with the appropriate values. For example, the *Current time* session variable always provides the current time in the user's time zone, at the time of the interaction with the customer.

To see these variables, click **Variables** in the navigation pane from the main actions page.

- The **Set by assistant** page shows built-in session variables that are automatically provided for each assistant.

- The **Set by integration** page shows variables that are automatically provided by the integration your customer is using to connect to the assistant. (These variables are not set if no integration is connected.)

**Set by assistant**:

|  Variable name             | Variable ID | Description | Example |
|----------------------------|-------------|-------------|---------|
| *Now*                      | `now`       | The current date and time in the user's time zone. | `2021-08-11T11:28:02` |
| *Current time*             | `current_time` | The current time in the user's time zone.       | `11:28:02`            |
| *Current date*             | `current_date` | The current date in the user's time zone.       | `2021-08-11`          |
| *Last action*              | `last_action`  |                                                 |                       |
| *Fallback reason*          | `fallback_reason` |                                              |                       |
| *Assistant repeats itself* | `assistant_repeats_itself` |                                     |                       |
{: caption="Variables set by assistant" caption-side="top"}

**Set by integration**:

| Variable name | Variable ID | Description | Example |
|---------------|-------------|-------------|---------|
| *Timezone*    | `timezone`  | The user's time zone as specified by the integration or API client. The default time zone (if not specified by the integration) is UTC. | `America/New_York` |
| *Locale*      | `locale`    | The user's locale as set by the integration or API client. The locale can affect understanding and formatting of dates, times and numbers. | `en-gb` |
| *Channel Name* | `channel_name` | The name of the channel that your user is interacting with. | `Web chat` |
{: caption="Variables set by integration" caption-side="top"}

## Storing a value in a session variable
{: #store-session-variable}

Any action can store a value in a session variable so it is available to other actions. To store a value in a session variable:

1. From within a step, choose the **Set variable values** ![Set variable values icon](images/set-variable-values.png) icon.

1. Click **Set new value**.

1. From the drop-down list, select the session variable you want to store the value in. Note that the new value will replace any previous value stored in the variable.

    If you have not yet created the session variable you want to use, select **New variable**. You can then specify the details about the new session variable, which will be added to the list of session variables for the assistant. (For more information, see [Creating a session variable](#create-session-variable).)

    - From the main actions skill page, click to open the *Variables - Created by you* page. Click **New variable**.

1. Select from the list to set the new value for the session variable:

    - Select an action variable to use the value of a customer response. You can choose an action variable created by any previous step in the current action.

    - Select another session variable to use its value. You can choose a session variable you created or one of the built-in variables.

    - Select **Expression** to write an expression to define the value for the session variable. For more information about expressions, see [Writing expressions](/docs/watson-assistant?topic=watson-assistant-expressions).

## Using variables to manage conversation flow

One of the ways you can use variables is to choose the correct path through the conversation, based on customer responses and other values available at run time. You can do this by defining step conditions, which determine whether a specific step in an action is executed based on runtime conditions.

By defining a condition based on an action variable, you can control whether a step is executed based on the customer's response to a previous step. You can also build step conditions based on session variables, which can store information from other actions.

For more information about step conditions, see [Defining step conditions](/docs/watson-assistant?topic=watson-assistant-step-conditions).

## Using variables to customize the conversation
{: #reference-variables}

You can also use variables in what your assistant says, dynamically referencing information that has been collected during the conversation. This is useful for confirming information the customer has provided (for example, `You want to transfer $153.14 to your checking account. Is that correct?`), and for simply personalizing the conversation to make it more human (`Hi, John. How can I help you today?`).

To reference a variable in what your assistant says:

1. In the **Assistant says** field, start typing the text for the response.

1. When you reach a point where you want to insert a reference to a variable, type a dollar sign (`$`) or click the *Insert a variable* icon (![Insert a variable icon](images/action-variable-icon.png)). A list appears showing the variables you can choose from.

1. Click a variable to add a reference to it in the text.

1. **Optional:** Click the variable in the text to add a fallback value. The fallback value is the value the assistant will use if a user-defined session variable does not contain a value.

    ![Fallback value for session variables](images/rn-fallback-value.png)

When you reference a variable, it appears using a default format in your assistant's response. The format of the variable might differ from the way the value is stored; for example, a date value of `2021-08-11` is formatted as `August 11, 2021` by default. <!-- (To learn how to change the format, see **[ADVANCED FORMATTING TOPIC]**.) -->

The default formats are as follows:

| Type | Format | Examples |
| --- | --- | --- |
| Options | As chosen by the user | `Yes` `No` |
| Number | Numerals only | `1000` |
| Date | Mmm DD, YYYY | `Jun 30, 2021` |
| Time | H:MM:SS AM | `5:15:00 PM` |
| Currency | Number only, no currency symbol | `20` |
| Percent | Number only, no percentage symbol | `20` |
| Free text | As entered by the user | `Please check that the apples aren't bruised` |
{: caption="Default formats for variables" caption-side="top"}

When building an assistant response that includes variables, you concatenate multiple parts (text strings and variables). A single response can consist of no more than 30 concatenated parts (for example, 15 variables along with 15 text strings).
{: note}
