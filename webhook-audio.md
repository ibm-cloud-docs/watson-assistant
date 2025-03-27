---

copyright:
  years: 2019, 2025
lastupdated: "2025-03-27"

---

{{site.data.keyword.attribute-definition-list}}

# Audio webhook
{: #webhook-audio}

This feature is currently supported only with the Genesys Audio Connector of the Phone Integration.{: note}

An Audio webhook calls an external service or application whenever a record response type is used to collect audio. The external service processes the audio, and if an error occurs, it disconnects the call. A common use for this Audio webhook is to store the audio for compliance reasons, as {{site.data.keyword.conversationshort}} does not store the audio.

## Before you begin

The programmatic call to the external service must meet these requirements:

 - The call must be a POST HTTP request.

 - The request body must be a JSON object (Content-Type: multipart/form-data).

 - The call must return within 30 seconds or less.

For more information on recording audio, See [Recording a caller's utterance](webhook-attestation.md).

## Procedure

To add the webhook details, complete the following steps:

1. Go to **Home** > **Environments**.

1. Click **Settings** ![Gear icon](images/gear-icon-black.png) from either the **Draft** tab > **Draft environment** or the **Live** tab > **Live environment**.

1. Click **Audio webhook**.

1. Set the **Audio webhook** switch to `Enabled`.

1. In the **URL** field, add the URL for the external application to which you want to send the HTTP POST request. Ensure that the URL uses the SSL protocol (for example, starting with https).

1. In the **Secret** field, add a private key to pass with the request to authenticate with the external service. The key must be specified as a text string (for example, purple unicorn), with a maximum length of 1,024 characters. 

    You cannot specify a context variable. If the external service does not require a token, specify any string that you want. You cannot leave this field empty. To view the secret as you enter it, click **Show password** before typing. After saving the secret, asterisks replace the string, and you cannot view it again. For more information about how this field is used, see [Webhook security](webhook-pre.md#webhook-pre-security).{: note}

1. In the **Timeout** field, specify the duration (in seconds) that you want the assistant to wait for a response from the webhook before returning an error. The timeout duration must be between 1 and 30 seconds.

1.  In the Headers section, add any headers that you want to pass to the service one at a time by clicking **Add header**.

    For example, if the external application that you call returns a response, it might be able to send a response in multiple formats. The webhook requires that the response is formatted in JSON. The following table illustrates how to add a header to ensure that the resulting value to be returned is in JSON format.

    | Header name    | Header value       |
    |----------------|--------------------|
    | `Content-Type` | `application/json` |
    {: caption="Header example" caption-side="bottom"}

After you save the header value, the string is replaced by asterisks and can't be viewed again. 

Your webhook details are saved automatically.

For more examples, see [Audio webhook examples](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/phone/examples/audio-webhook). {: external}

## Testing the webhook
{: #webhook-audio-test}

Do extensive testing of your webhook before you enable it for an assistant that is being used in a production environment.
{: important}

The webhook is triggered when a recording response type is used during a phone call. If the request to the webhook fails, the call disconnects. You can look at the phone integration logs for more details as to why the webhook failed. For more information, see [Phone integration troubleshooting](phone-troubleshooting.md).

## Request body
{: #webhook-audio-request-body}

It is useful to know the format of the request body of the Audio webhook so that your external code can process it.

The payload contains the audio and metadata as Content-Type: multipart/form-data. An example of the request is:

    POST /audio-webhook HTTP/1.1
    Content-Type: multipart/form-data; boundary=----------3676416B-9AD6-440C-B3C8-FC66DDC7DB45
    ----------3676416B-9AD6-440C-B3C8-FC66DDC7DB45
    Content-Disposition: form-data; name="metadata"
    Content-Type: application/json
    {
        "assistant_id": "dadf4b56-3b67-411a-b48d-079806b626d3",
        "environment_id": "6205aead-fe91-44af-bfe1-b4435015ba23",
        "session_id": "50989a59-9976-4b3f-9a98-af42adcad69a",
        "recording_id": "3daeb5d2-f52b-4c3e-a869-328b6fc6327c",
        "start_timestamp": "2024-10-21T17:22:07.789Z",
        "stop_timestamp": "2024-10-21T17:22:37.789Z"
    }
    ----------3676416B-9AD6-440C-B3C8-FC66DDC7DB45
    Content-Disposition: form-data; name="audio_recording"
    Content-Type: audio/mulaw;rate=8000

    <binary data>

    {: codeblock}
