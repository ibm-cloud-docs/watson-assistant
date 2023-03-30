---

copyright:
  years: 2023
lastupdated: "2023-03-30"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Uploading or downloading all actions
{: #upload-download-actions}

You can upload or download all your actions as a JSON file. 

## Downloading
{: #upload-download-actions-global-settings-download}

To back up all your actions, download a JSON file and store it. 

1. On the **Actions** page, click **Global settings** ![Gear icon](../../icons/settings.svg).

1. On the **Upload/Download** tab, click the **Download** button.

## Uploading
{: #upload-download-actions-global-settings-upload}

To reinstate a backup copy of actions that you exported from another service instance or environment, import the JSON file of the actions you exported.

If the {{site.data.keyword.conversationshort}} service changes between the time you export the actions and import it, due to functional updates that are regularly applied to instances in cloud-hosted continuous delivery environments, your imported actions might function differently than before.
{: important}

1. On the **Actions** page, click **Global settings** ![Gear icon](../../icons/settings.svg).

1. On the **Upload/Download** tab, drag and drop a JSON file onto the tab or click to select a file from your local system, then click **Upload**.

The imported JSON file must use UTF-8 encoding, without byte order mark (BOM) encoding. The JSON file cannot contain tabs, newlines, or carriage returns.
{: important}

## Uploading intents as actions
{: #upload-download-actions-upload-intents}

If you created intents in the classic {{site.data.keyword.conversationshort}} experience, you can migrate your intents to actions in the new {{site.data.keyword.conversationshort}} experience. When you upload intents, each intent is created as a new action. All phrases corresponding to an intent are created as example phrases for the new action. This can provide a helpful starting point when you are ready to start building actions in the new experience.

1. Download the intents that you want to migrate to actions from the classic {{site.data.keyword.conversationshort}} experience. For more information, see [Downloading intents](/docs/watson-assistant?topic=watson-assistant-migrate-intents-entities#migrate-intents-download). The format for each line in the file is as follows:
    ```text
    <phrase>,<intent>
    ```
    where `<phrase>` is the text of a user example phrase, and `<intent>` is the name of the intent. For example:
    ```text
    Tell me the current weather conditions.,weather_conditions
    Is it raining?,weather_conditions
    What's the temperature?,weather_conditions
    Where is your nearest location?,find_location
    Do you have a store in Raleigh?,find_location
    ```

1. From the main actions page, click the **Upload** icon ![Upload icon](../../icons/upload.svg).

1. Select the intents file that you downloaded.

    The file is validated and uploaded, and the system trains itself on the new data.

    The intents in column 2 are created as new actions, and the phrases in column 1 are created as example phrases for the corresponding action. For example, if you upload the example from step 1, two new actions are created for the `weather_conditions` and `find_location` intents. The underscores (`_`) in the intent names are replaced with spaces, for example, the `weather_conditions` intent becomes the `weather conditions` action.

    In this example, the `weather_conditions` action will have three example phrases: `Tell me the current weather conditions.`, `Is it raining?`, and `What's the temperature?`. The `find_location` action will have two example phrases: `Where is your nearest location?` and `Do you have a store in Raleigh?`.
