---

copyright:
  years: 2018, 2021
lastupdated: "2021-08-26"

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

{{site.data.content.classiclink}}

# Defining step conditions
{: #step-conditions}

An action represents a business process that helps customers answer their questions or solve their problems. Such a process must adapt to different specifics, based on information provided by customers or otherwise available at run time. For example, the steps for withdrawing money from a savings account might be slightly different from the steps for withdrawing for a checking account.

A step condition is a boolean test, based on some runtime value; the step executes only if the test evaluates as true. This test can be applied to any variable, such as an action variable containing the customer response from a previous step. By defining step conditions, you can create multiple pathways through an action based on different possible runtime values.

For more information about variables, see [Managing information during the conversation](/docs/watson-assistant?topic=watson-assistant-manage-info).

A basic step condition is expressed in the following form:

  `If` `{variable}` `{operator}` `{value}`

where:

- `{variable}` is the name of a variable or an expression.
- `{operator}` is the type of test to apply to the variable value (for example, `is` or `is not`).
- `{value}` is the value to compare to the variable.

For example, a step condition might read:

  `If` `Withdraw from which account?` `is` `Checking`

  This condition evaluates as true if the customer's response to the previous `Withdraw from which account?` step is `Checking`.

Conditions can be grouped together to construct complex tests.

To add a step condition:

1.  Open the step. Click the condition field at the beginning of the step:

    ![Step editor with condition field highlighted](images/step-condition.png)

1. Select **With conditions** from the drop-down list. The **Conditions** section expands.

1. By default, a single condition group, containing a single condition, is automatically created based on the action variable stored by the most recent customer response.

    ![Editing a condition to select Checking as the value to check for](images/action-condition-edit.png)

    You can click any part of the expression to edit it:

    - Select the variable you want to test. You can select any of the following:

      - An action variable storing the customer response from a previous step in the action.
      - A session variable containing a value stored by any action.
      - A built-in variable set by the assistant or by an integration.

      You can also define a complex condition by writing an expression defining some other value. For more information about expressions, see [Writing expressions](/docs/watson-assistant?topic=watson-assistant-expressions).
      {: note}

    - Select the operator representing the test you want to perform on the variable (for example, `is` or `is not`). The available operators for a particular value depend upon its data type. (For more information, see [Operators](#step-conditions-operators).)

    - Select the value you want to evaluate the test against. Again, the values available depend upon the type of value you are testing. For example, an variable containing an options response can be tested against any of the defined options, and a date value can be tested against any date.

1.  To add more than one condition to a step, after adding a condition, click **Add condition**.

    One use case where using more than one condition is helpful is if you need to capture a value range. For example, maybe a requirement of opening a checking account is that the customer deposit at least $100 into the account at creation time. You might ask the customer if they want to transfer funds to the account, and if so, how much? To continue with the transfer, the transfer amount must be $100 or more, but cannot exceed $1000. You can add a step with the following conditions: 

    - `How much to transfer?` `>` `99`
    - `How much to transfer?` `<` `1001`

    Specify whether all or any of the conditions must be met for the step to be included in the conversational flow.

1.  To add another group of conditions, click **Add new group**.

    You can use groups to build complex step conditions. Each group is evaluated true or false as a whole, and then these results are evaluated together. For example, you might build a step that executes only if all conditions in group 1 are true *or* any condition in group 2 is true. (Groups function like parentheses in the boolean conditions of many programming languages.)

    After you add a group, you can define one or more conditions in the new group. Each conditional group is numbered. Between groups, choose **and** or **or** to indicate whether the conditions in both conditional groups or only one of them must be met for the step to be included in the conversational flow.

## Operators

An operator specifies the kind of test you are performing on a value in a condition. The specific operators available in a condition depend on the customer response type of the value, as shown in the following table.

Currently, the only tests supported for session variables are `is defined` and `is not defined`. Other tests are supported only for action variables.
{: note}

| Response type                        | Operators                           |
|--------------------------------------|-------------------------------------|
| Options<br/>Free text<!--<br/>Regex--> | <ul><li>is</li><li>is not</li></ul> |
| Number<br/>Currency<br/>Percent<br/> | <ul><li>is defined</li><li>is not defined</li><li>is equal to (==)</li><li>is not equal to (≠)</li><li>is less than (&lt;)</li><li>is less than or equal to (&lt;=)</li><li>is greater than (&gt;)</li><li>is greater than or equal to (&gt;=)</li></ul> |
| Date                                 | <ul><li>is defined</li><li>is not defined</li><li>is on</li><li>is not on</li><li>is before</li><li>is after</li><li>is on or before</li><li>is on or after</li></ul> |
| Time                                 | <ul><li>is defined</li><li>is not defined</li><li>is at</li><li>is not at</li><li>is before</li><li>is after</li><li>is at or before</li><li>is at or after</li></ul> |
