---

copyright:
  years: 2018, 2021
lastupdated: "2021-08-31"

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

# Overview: Managing conversation flow
{: #manage-flow}

A conversation with your assistant might take many different paths, depending on what information your customers provide and what decisions they make. You can build your assistant so it guides each customer along the fastest path to the right solution.
{: shortdesc}

After your assistant's greeting, each conversation begins with a customer question or request. The first step in guiding your customer to the right solution is for the assistant to recognize what the customer is asking for (based on the example input you have specified), triggering the appropriate action.

There are several ways in which the assistant can adapt the conversation to guide the customer down the right path:

- [**Step conditions**](/docs/watson-assistant?topic=watson-assistant-step-conditions): Each step in an action can be configured to execute only under certain conditions. Therefore, one action can handle multiple variations of the same issue, depending on conditions at run time.

- [**Skipping steps**](/docs/watson-assistant?topic=watson-assistant-skip-steps): Each step in an action can be skipped, if the information it asks for has already been provided.

- [**Choosing what to do next**](/docs/watson-assistant?topic=watson-assistant-step-what-next): Instead of executing the steps in an action in sequential order, you can modify the sequence of steps by defining what happens when a step is complete.

- [**Changing the conversation topic**](/docs/watson-assistant?topic=watson-assistant-change-topic): Your customer might change the topic of the conversation in the middle of an action. Your assistant can respond to this when appropriate.

- [**Handling errors**](/docs/watson-assistant?topic=handle-errors): Sometimes customers can run into problems getting the assistant to do what they want. You can configure how the assistant recovers from these situations to get back on track.

By using these mechanisms, you can build an assistant that is flexible and responds dynamically to quickly get your customers to the solutions they need.
