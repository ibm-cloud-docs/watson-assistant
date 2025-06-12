---

copyright:
  years: 2018, 2025
lastupdated: "2025-06-09"

keywords: IBM,activity tracker,event,security, assistant event tracker

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Activity tracking events {{site.data.keyword.conversationshort}}
{: #at-events}


[IBM Cloud]{: tag-ibm-cloud} [Enterprise]{: tag-purple} [Premium]{: tag-teal}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.conversationshort}}, generate activity tracking events. This applies to both the classic and new experiences of {{site.data.keyword.conversationshort}}.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.



As of 28 March 2024, the {{site.data.keyword.at_full_notm}} service is deprecated and will no longer be supported as of 30 March 2025. Customers will need to migrate to {{site.data.keyword.logs_full_notm}} before 30 March 2025. During the migration period, customers can use {{site.data.keyword.at_full_notm}} along with {{site.data.keyword.logs_full_notm}}. Activity tracking events are the same for both services.

{: important}
-->





## Locations where activity tracking events are sent to {{site.data.keyword.logs_full_notm}} hosted event search
{: #at-legacy-locations}



{{site.data.keyword.conversationshort}} sends activity tracking events to {{site.data.keyword.logs_full_notm}} hosted event search in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #at-table-1}
{: tab-title="Americas"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #at-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #at-table-3}
{: tab-title="Europe"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

## Locations where activity tracking events are sent by {{site.data.keyword.atracker_full_notm}}
{: #atracker-locations}



{{site.data.keyword.conversationshort}} sends activity tracking events by {{site.data.keyword.atracker_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #atracker-table-1}
{: tab-title="Americas"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #atracker-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #atracker-table-3}
{: tab-title="Europe"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}







## Viewing activity tracking events for {{site.data.keyword.conversationshort}} 
{: #at-viewing}



You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

Events that are generated by an instance of the {{site.data.keyword.conversationshort}} service are automatically forwarded to the {{site.data.keyword.logs_full_notm}} service instance that is available in the same location. However, if your service instance is hosted in the **Washington DC** location, create the {{site.data.keyword.logs_full_notm}} service instance in the **Dallas** region.

{{site.data.keyword.logs_full_notm}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.logs_full_notm}} service in the same location where your service instance is available. For more information, see [Navigating to the UI](/docs/activity-tracker?topic=activity-tracker-launch){: external}.

![{{site.data.keyword.conversationshort}} events in {{site.data.keyword.logs_full_notm}}](images/activity-tracker.png)




### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}



For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

## List of events
{: #at_auditing_events}



| Action                           | Description                        |
|----------------------------------|------------------------------------|     
| `conversation.action.create` | creates an action |
| `conversation.action.delete` | deletes an action |
| `conversation.action.update` | updates an action |
| `conversation.action_handler.create` | creates an action handler |
| `conversation.action_handler.delete` | deletes an action handler |
| `conversation.action_handler.update` | updates an action handler |
| `conversation.action_variable.create` | creates an action variable |
| `conversation.action_variable.delete` | deletes an action variable |
| `conversation.action_variable.update` | updates an action variable |
| `conversation.actions.copy` | copies an action from one assistant to another |
| `conversation.assistant.create` | creates an assistant |
| `conversation.assistant.delete` | deletes an assistant |
| `conversation.assistant.update` | updates an assistant, for example, updates the settings |
| `conversation.catalog_integration.create` | creates a custom extension |
| `conversation.catalog_integration.delete` | deletes a custom extension |
| `conversation.catalog_integration.update` | updates a custom extension |
| `conversation.counterexample.create` | marks test user input in "Try it out" as being irrelevant or corrects the categorization of a user input that was incorrectly assigned to an intent by marking it as irrelevant |
| `conversation.counterexample.delete` | deletes a counterexample |
| `conversation.counterexample.update` | edits a counterexample |
| `conversation.data.delete` | deletes multiple training data items, such as multiple entities or intents |
| `conversation.data.update` | does a bulk action, such as importing a CSV file of intents or entities to the skill |
| `conversation.data_type.create` | creates a saved response |
| `conversation.data_type.delete` | deletes a saved response |
| `conversation.data_type.update` | updates a saved response |
| `conversation.entity.create` | creates an entity |
| `conversation.entity.delete` | deletes an entity |
| `conversation.entity.update` | edits an entity |
| `conversation.environment.create` | adds an environment |
| `conversation.environment.delete` | deletes an environment |
| `conversation.environment.updates` | updates an environment |
| `conversation.example.create` | adds a user input example to an intent |
| `conversation.example.delete` | deletes a user example from an intent |
| `conversation.example.update` | edits a user example that is associated with an intent |
| `conversation.integration_defintion.create` | creates an integration |
| `conversation.integration_defintion.delete` | deletes an integration |
| `conversation.integration_defintion.update` | updates an integration |
| `conversation.intent.create` | creates an intent |
| `conversation.intent.delete` | deletes an intent |
| `conversation.intent.update` | edits an intent |
| `conversation.log.create` | corrects an intent that was inaccurately categorized by the skill from the Analytics>User conversations page |
| `conversation.node.create` | creates a dialog node |
| `conversation.node.delete` | deletes a dialog node |
| `conversation.node.update` | edits a dialog node |
| `conversation.notifier.create` | creates a notifier |
| `conversation.notifier.delete` | deletes a notifier |
| `conversation.notifier.update` | updates a notifier |
| `conversation.processor.create` | creates a processor |
| `conversation.processor.delete` | deletes a processor |
| `conversation.processor.update` | updates a processor |
| `conversation.release.create` | create a version from content in the draft environment |
| `conversation.release.delete` | delete a version |
| `conversation.release.deploy` | publish a version to an environment |
| `conversation.skill.create` | creates a skill |
| `conversation.skill.delete` | deletes a skill |
| `conversation.skill.update` | updates a skill |
| `conversation.skill_reference.create` | adds a specific skill to an assistant |
| `conversation.skill_reference.delete` | removes a specific skill from an assistant |
| `conversation.skill_reference.update` | updates a specific skill that is associated with an assistant |
| `conversation.skill_variable.create` | create a skill variable |
| `conversation.skill_variable.delete` | delete a skill variable |
| `conversation.skill_variable.update` | update a skill variable |
| `conversation.skills.export` | export a skill |
| `conversation.skills.import` | import a skill |
| `conversation.snapshot.create` | creates a version of a dialog skill |
| `conversation.snapshot.delete` | deletes a version of a dialog skill |
| `conversation.snapshot.update` | updates a version of a dialog skill |
| `conversation.step.create` | adds a step to an action |
| `conversation.step.delete` | deletes a step from an action |
| `conversation.step.update` | updates a step in an action |
| `conversation.step_handler.create` | create a step handler |
| `conversation.step_handler.delete` | delete a step handler |
| `conversation.step_handler.update` | update a step handler |
| `conversation.synonym.create` | creates a synonym for an entity value |
| `conversation.synonym.delete` | deletes a synonym that is associated with an entity value |
| `conversation.synonym.update` | edits a synonym that is associated with an entity value |
| `conversation.userdata.delete` | deletes data that was created by a specified customer |
| `conversation.value.create` | creates an entity value |
| `conversation.value.delete` | deletes an entity value |
| `conversation.value.update` | edits an entity value |
| `conversation.workspace.create` | creates a workspace |
| `conversation.workspace.delete` | deletes a workspace |
| `conversation.workspace.update` | edits a workspace |                              |
{: caption="Actions that generates events" caption-side="bottom"}


## Additional information for update events
{: #at_events_additional_updates}

Any of the update events include this additional information in a `requestData.update` object:

- Name changed
- Title changed
- Metadata changed
- Training data changed

This example from an `assistant.update` event shows a name change:

```code
"update":[{"updateType":"Name changed","nameAttribute":"name","newValue”:”Banking Bot 2},{“updateType":"Metadata changed","attributesUpdated":["description","language"]}],{"environment":"draft"},
```
