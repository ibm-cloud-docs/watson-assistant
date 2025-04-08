---

copyright:
  years: 2019, 2025
lastupdated: "2025-04-07"

---

{{site.data.keyword.attribute-definition-list}}

# Recording a caller's utterance
{: #record-caller-utterance}

This feature is currently supported only with the Genesys Audio Connector of the Phone Integration.{: note}

The **Record** feature captures the caller's utterance to verify their identity, provide consent, or authorize actions. You can then play it back to the caller for confirmation to proceed with the action.

## Before you begin

Go to [**Defining an audio webhook**](/docs/watson-assistant?topic=watson-assistant-define-webhook-audio) to collect and save audio from the user.

## Adding a recording

Add a record response to collect the user's voice and play it back to confirm a transaction. 

To add the record response type, do the following steps:

1. Go to **Home** > **Actions**.

1. Select your **Action** name or create a **New action +** > **Conversation steps**.

1. In the **Assistant says** field, click the **Add recording** icon ![Recording icon](images/recording-icon.png).

1. In the **Customer prompt** field, type the message that you want the caller to hear before the recording starts. 
For example, "Please state your name to authorize the payment. Press pound to capture the recording."

1. You can choose to play a tone before the recording starts. In the **Input method** field, select **Beep** to play the tone, otherwise select **Silent (pause)**.

1. Select the keypad **End recording key** that the caller needs to press to end the recording. The default value is **#**.

1. In the **Playback confirmation** field, type the message that the caller hears after the recording completes to confirm the recording. The placeholder variable **[recording]** is used where the caller listens to the audio recording.

1. Click **Apply**.
