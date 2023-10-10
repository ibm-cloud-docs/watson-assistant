---

copyright:
  years: 2015, 2023
lastupdated: "2023-10-10"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Glossary
{: #glossary}

| Term | Definition |
| --- | --- |
| Action | Actions represent the tasks or questions that your assistant can help customers with. Each action has a beginning and an end, making up a conversation between the assistant and a customer.  [Learn more](/docs/watson-assistant?topic=watson-assistant-build-actions-overview). |
| Ask clarifying question | A feature that enables the assistant to ask customers to clarify (disambiguate) their meaning when the assistant isn't sure what a user wants to do next. [Learn more](/docs/watson-assistant?topic=watson-assistant-understand-questions#understand-questions-ask-clarifying-question). |
| Assistant | Container for your actions, channels, and integrations. You add actions and at least one channel to an assistant, and then deploy the assistant when you are ready to start helping your customers. [Learn more](/docs/watson-assistant?topic=watson-assistant-publish-overview). |
| Change conversation topic | A feature that gives the user the power to direct the conversation. It allows digressions and prevents customers from getting stuck in a dialog thread; they can switch topics whenever they choose. [Learn more](/docs/watson-assistant?topic=watson-assistant-change-topic). |
| Channel | The location where your assistant interacts with your users, for example, over the phone, on a website, or in Slack. At least one channel is required for every assistant. [Learn more](/docs/watson-assistant?topic=watson-assistant-deploy-assistant). |
| Completion | Measures how often within a given time period users reach the end step of an action. [Learn more](/docs/watson-assistant?topic=watson-assistant-analytics-action-completion#complete-reasons). |
| Content | The conversation logic and words that are used to respond to your customer. Content is required for every assistant. [Learn more](/docs/watson-assistant?topic=watson-assistant-build-actions-overview). |
| Environment | You can group your work in separate containers that are called _environments_. Each environment contains its own content, channels, and extensions. Environments also have their own IDs, URLs, and service credentials that can be referenced by external services. Each new assistant comes with two environments: the draft environment and the live environment. Your customers interact with assistants on the live environment and cannot interact with assistants on the draft environment. The separation of these two environments allows you to build and iterate on your content separately from what your customers see. You do not want customers to stumble upon an incomplete action that leads them to a dead end. For Enterprise plans, you can add up to three environments as a staging area to test your assistant before deployment. You can build content in the draft environment and test versions of your content in the extra environments. [Learn more](/docs/watson-assistant?topic=watson-assistant-publish-overview#environments). |
| Escalation | If your assistant is integrated with one of the supported service desk systems, you can build in logic that transfers, or escalates, the conversation to a human when necessary. [Learn more](/docs/watson-assistant?topic=watson-assistant-human-agent). |
| Incompletion | Reasons why an action is not completed by a user, including `escalated to agent`, `started a new action`, `stuck on a step`, or `abandoned or ongoing`. [Learn more](/docs/watson-assistant?topic=watson-assistant-analytics-action-completion#reasons-for-incompletion) |
| Integrations | Add-ons to the end experience that help solve specific user problems, for example, connecting to a human agent or searching existing help content. Integrations are not required for an assistant, but they are recommended. [Learn more](/docs/watson-assistant?topic=watson-assistant-deploy-assistant). |
| Message | A single turn within a conversation that includes a single call to the `/message` API endpoint and its corresponding response. |
| Monthly active user (MAU) | A single unique user who interacts with an assistant one or many times in a given month. [Learn more](/docs/watson-assistant?topic=watson-assistant-admin-managing-plan#admin-managing-plan-user-based). |
| Preview | Embeds your assistant in a chat window that is displayed on an IBM-branded web page. From the preview, you can test how a conversation flows through your assistant, from end to end. [Learn more](/docs/watson-assistant?topic=watson-assistant-preview-share). |
| Recognition | Measurement of how many requests are being recognized by the assistant and routed into starting an action. [Learn more](/docs/watson-assistant?topic=watson-assistant-analytics-overview#recognition). |
| Response | To create your assistant's response in an action step, you use the *Assistant says* section. This represents the text or speech the assistant delivers to a user at a particular step. Depending on the step, you can add a complete answer to a user's question or ask a follow-up question. [Learn more](/docs/watson-assistant?topic=watson-assistant-respond). |
| Step | A step that you add to an action represents a single interaction or exchange of information with a customer, a turn in the conversation. [Learn more](/docs/watson-assistant?topic=watson-assistant-build-actions-overview#steps). |
| Subaction | An action that is called from another action is referred to as a _subaction_. [Learn more](/docs/watson-assistant?topic=watson-assistant-step-what-next#go-to-another-action). |
| Training |  To set up an instance with components that enable the system to function in a particular domain (for example: corpus content, training data that generates machine learning models, programmatic algorithms, annotators, or other ground truth components) and then making improvements and updates to these components based on accuracy analysis. |
| Variable | A variable is data that a customer shares with the assistant, which is collected and saved so it can be referenced later. In actions, you can collect *action* and *session* variables. [Learn more](/docs/watson-assistant?topic=watson-assistant-manage-info#action-variables-and-session-variables). |
| Web chat | A channel that you can use to embed your assistant in your company website. [Learn more](/docs/watson-assistant?topic=watson-assistant-deploy-web-chat). |
| Webhook | A mechanism for calling out to an external program during a conversation. For example, your assistant can call an external service to translate a string from English to French and back again in the course of the conversation. [Learn more](/docs/watson-assistant?topic=watson-assistant-webhook-overview). |
{: caption="Glossary" caption-side="top"}
