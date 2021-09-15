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

# Writing expressions
{: #expressions}

You can write _expressions_ to specify values that are independent of, or derived from, values that are collected in steps or stored in session variables. You can use an expression to define a step condition or to define the value of a session variable.

The Watson Assistant expression language is based on the Spring Expression Language (SpEL), but with some important differences in syntax. For detailed background information about SpEL, see [Spring Expression Language (SpEL)](https://docs.spring.io/spring-framework/docs/5.2.13.RELEASE/spring-framework-reference/core.html#expressions).
{: note}

For example, you might use an expression to write simple math equations. Maybe a customer has $200 in a savings account and wants to transfer $150 from it to a new checking account. The funds transfer fee is $3, and the bank charges a fee when a savings account contains less than $50. You could create a step with a step condition that checks for this situation. The step condition would use an expression like this:

```
${savings} - (${Step_232} + ${transfer_fee}) < 50
```
{: codeblock}

where:

- `${savings}` represents a session variable that stores the customer's savings account total.
- `${Step_232}` represents the step that asks for the amount the customer wants to transfer.
- `${transfer_fee}` represents a session variable that specifies the fee for a funds transfer.

If the step condition is met, the step warns the user that the requested transfer will bring the savings account balance below the $50 minimum and incur a fee, and ask to confirm before proceeding.

To use an expression in a step condition:

1.  From the step, click **Add condition**.

    A condition is generated automatically with the most likely choice, which is typically any variables that were set in the previous step.

1.  Click the first segment of the generated condition, and then scroll down and click **Expression**.

1.  Add the expression that you want to use.

To use an expression to define a session variable value:

1.  From the step, choose the **Set variable values** icon, and then choose **Set variable values**. Click **Set new value**.

1.  Choose the session variable that you want to define a value for. 

1.  From the list of sources to derive the value from, click **Expression**.

1.  Add the expression that you want to use.

For a full list of supported expressions, see XXXX.
