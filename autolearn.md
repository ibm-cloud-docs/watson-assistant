---

copyright:
  years: 2020, 2023
lastupdated: "2023-06-21"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Using autolearning to improve assistant responses
{: #autolearn}

[IBM Cloud]{: tag-ibm-cloud}

Use *autolearning* to enable your assistant to learn from interactions with your customers and improve responses.
{: shortdesc}

This is a beta feature that is available for evaluation and testing purposes on IBM Cloud in English-language assistants only.
{: beta}

When customers interact with your assistant, they often make choices. Your assistant can learn from these user decisions.

For example, a customer might ask a question that the assistant isn't sure it understands. The assistant asks a clarifying question so the customer can choose the right action from a list. If customers most often click the same action (option #2, for example), your assistant can learn that option #2 is the best answer. 

Next time, the assistant can list option #2 as the first choice, so customers can get to it more quickly. If the pattern persists over time, it can change its behavior even more. Your assistant can return option #2 immediately, rather than asking a clarifying question.

As your assistant learns over time, your customers get the best answer more often and in fewer clicks.

## How autolearning works
{: #autolearn-how-it-works}

Before your assistant can learn from customer behavior, it must observe a significant amount of real conversation data. The conversations take place in a channel such as the web chat, or in a custom application. 

Logs of conversations and user decisions from your live environment are the data source for observation. Your assistant analyzes the logs to gain insights. (It doesn't watch real-time clicks during a conversation.)

When the assistant observes enough real conversation data from the live environment, it gains insights to help improve your assistant, providing a better customer experience.

When you publish your assistant to the live environment, autolearning starts training the assistant. To apply the autolearning improvements to your assistant's responses, [enable autolearning](#autolearn-task).

## Enabling autolearning
{: #autolearn-task}

You can enable autolearning when the following conditions are met:

- **Ask clarifying question** is enabled in **Global settings**. For more information, see [Global settings for actions](/docs/watson-assistant?topic=watson-assistant-actions-global-settings).

- You publish a version of your assistant to the live environment. For more information, see [Publishing your content](/docs/watson-assistant?topic=watson-assistant-publish).

- Your customers are interacting with a channel or custom application that is connected to the live environment. 

To apply autolearning improvements to your assistant responses:

1. On the **Actions** page, click **Global settings** ![Gear icon](../../icons/settings.svg).

1. Click the **Autolearning** tab.

1. Set the **Use autolearning to modify responses with training from live environment** switch to **On**.

1. In the draft environment, you can preview your actions or your assistant. With autolearning set to **On**, preview in the draft environment uses the autolearning training from the live environment. For more information, see [Using Preview to test your action](/docs/watson-assistant?topic=watson-assistant-review#review-test) or [Previewing your assistant](/docs/watson-assistant?topic=watson-assistant-preview-share).

1. If you are happy with the results from testing the autolearning improvements in the draft environment, publish a new version of your assistant to the live environment to apply the improvements. For more information, see [Publishing your content](/docs/watson-assistant?topic=watson-assistant-publish).


## Learning from your data
{: #autolearn-data}

Observations are made of only your customers' choices to improve only your assistant. These observations are not reused by IBM or shared in any way.

This observed user choices data is separate from the log data for which metrics are displayed on the Analyze page. The observation data is also separate from the information that is collected in all but Enterprise plan service instances and used by IBM for general service improvements. You can opt out of such use by specifying an opt-out header in your `/message` API requests. For more information, see [Opting out of log data use](/docs/watson-assistant?topic=watson-assistant-admin-securing#securing-log-opt-out).

To prevent your own assistant from applying what it learns by observing user choices to your assistant, disable autolearning:

1. In **Global settings**, click the **Autolearning** tab.

1. Set the **Use autolearning to modify responses with training from live environment** switch to **Off**. This immediately disables the modifying of responses in the draft environment.

1. Publish a new version of your assistant to the live environment to completely disable the modifying of responses by autolearning.


