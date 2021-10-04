---

copyright:
  years: 2021
lastupdated: "2021-10-04"

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

# Preview runtime errors
{: #preview-runtime-errors}

You may see these system errors when testing your assistant in [Preview](/docs/watson-assistant?topic=watson-assistant-review).

Some of these errors correspond to advanced development tasks.
{: note}

| Message | Description |
| ---- | ---- | 
| `No actions to interpret` | Assistant has no content. |
| `No action triggered` | Error when an action is not found, for example, when one action specifies another action that isn't defined yet. |
| `Conversation ended. Maximum of %d actions visited.` | Limit is 20 per conversation. |
| `Maximum number of step iterations for a single action` | When a particular step is reached more than 50 times within an action. |
| `Error when updating output in [%s]. The output is [%s]` | When there was an error in updating the output, for example, when using a  SpEL expression. | 
| `Error in context update` | Error when setting a variable to an invalid ASEL expression. | 
| `Error when updating context with context of step %s. Step context is [%s].` | Error when a runtime exception occurs while setting a context, for example, division by zero. |
| `Multiple actions have the same title: %s` | Actions need to have unique names. |
| `Action %s is invalid because step order includes a cycle. Evaluation could result in an infinite loop. Check \"next_step\" property of each step in the action.` | Step could get caught in an infinite loop and not end. |
| `Expression evaluation error inside condition of %s. The syntax is valid, but cannot be evaluated. Condition defaulted to false. Check that objects in expression are not null or out of bounds. Error: %s` | When an unexpected error occurs while checking a condition, for example, division by 0. |
| `Provided expression [%s] cannot be evaluated as a number` | ASEL error message | 
| `Provided expression [%s] cannot be evaluated as Boolean` | ASEL error message | 
| `Provided expression [%s] cannot be evaluated as a string` | ASEL error message | 
| `Provided expression [%s] cannot be evaluated` | ASEL error message | 
| `Actions array contains an element that is not a JsonObject. Cannot build an internal representation.` | Advanced programming message | 
| `Actions array contains elements with the same id (attribute 'action'). Cannot build an internal representation.` | Advanced programming message | 
| `No target step %s found for jump-to resolver` | Advanced programming message | 
| `For resolver of type jump_to the target step cannot be the same as the source step.` | Advanced programming message | 
 
	









































