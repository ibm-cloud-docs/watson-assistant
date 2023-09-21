---

copyright:
  years: 2020, 2023
lastupdated: "2023-09-21"

keywords: phone, context variables, input parameters

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}


# Phone integration context variables
{: #phone-context}

You can use context variables to manage the flow of conversations with customers who interact with your assistant over the telephone.
{: shortdesc}

The following tables describe context variables that have special meaning in the context of the phone integration. They need to be used for the purpose documented, and none other.



## Context variables that are set by the phone channel
{: #phone-context-variables-set-by-phone-channel}

| Name | Type | Description |
|------|------|-------------|
| `sip_call_id` | string | The SIP call ID associated with the {{site.data.keyword.conversationshort}} session. |
| `sip_custom_invite_headers` | object | A JSON object with key or value pairs defining SIP headers that are pulled from the initial SIP `INVITE` request and passed to the {{site.data.keyword.conversationshort}} service (for example, `{"Custom-Header1": "123"}`). |
| `private.sip_from_uri` | string | The SIP `From` URI associated with the {{site.data.keyword.conversationshort}} service. |
| `private.sip_request_uri` | string | The SIP request URI that started the conversation session. |
| `private.sip_to_uri` | string | The SIP `To` URI associated with the conversation session. |
| `private.user_phone_number` | string | The phone number that the call was received from. |
| `assistant_phone_number` | string | The phone number associated with the {{site.data.keyword.conversationshort}} side that received the phone call. | 
{: caption="Context variables set by the phone channel" caption-side="top"}

## Input parameters that are set by the phone channel
{: #phone-context-input-parameters-set-by-phone-channel}

The following input parameters are only valid for the current conversation turn.

| Name | Type | Description |
|------|------|-------------|
| `post_response_timeout_occurred` | boolean | Whether the post-response timeout expired. |
| `barge_in_occurred` | boolean | Whether barge-in occurred. |
| `final_utterance_timeout_occurred` | `true` or `false` | Whether the final-utterance timeout expired. |
| `dtmf_collection_succeeded` | boolean | Whether the DTMF collection succeeded or failed. When `true`, a DTMF collection succeeded, and returns the expected number of digits. When `false`, a DTMF collection failed to collect the specified number of digits. Even when `dtmf_collection_succeeded` is `false`, all collected digits are passed to the dialog in the input string of the turn request. |
| `is_dtmf` | boolean | Whether the input to {{site.data.keyword.conversationshort}} is dual-tone multi-frequency signaling (DTMF). |
| `speech_to_text_result` | object | The final response from the {{site.data.keyword.speechtotextshort}} service in JSON format, including the transcript and confidence score for the lead hypothesis and any alternatives. The format matches exactly the format that is received from the {{site.data.keyword.speechtotextshort}} service. (For more information, see the [{{site.data.keyword.speechtotextshort}} API documentation](https://cloud.ibm.com/apidocs/speech-to-text#recognize){: external}.) |
{: caption="Input parameters set by the phone channel" caption-side="top"}
| `sms_message` | string | A SMS message received from the caller. |

### Example

```json
{
  "input": {
    "text": "agent ",
    "integrations": {
      "voice_telephony": {
        "speech_to_text_result": {
          "result_index": 0,
          "stopTimestamp": "2021-09-29T17:43:31.036Z",
          "transaction_ids": {
            "x-global-transaction-id": "43dd6ce0-139a-4d76-95aa-86e03fcfc434",
            "x-dp-watson-tran-id": "6e60695e-fed7-4efe-a376-0888b027d30f"
          },
          "results": [
            {
              "final": true,
              "alternatives": [
                {
                  "transcript": "agent ",
                  "confidence": 0.78
                }
              ]
            }
          ],
          "transactionID": "43dd6ce0-139a-4d76-95aa-86e03fcfc434",
          "startTimestamp": "2021-09-29T17:43:29.436Z"
        },
        "is_dtmf": false,
        "barge_in_occurred": false
      }
    }
  },
  "context": {
    "skills": {
      "main skill": {
        "user_defined": {},
        "system": {}
      }
    },
    "integrations": {
      "voice_telephony": {
        "private": {
          "sip_to_uri": "sip:watson-conversation@10.10.10.10",
          "sip_from_uri": "sip:10.10.10.11",
          "sip_request_uri": "sip:test@10.10.10.10:5064;transport=tcp"
        },
        "sip_call_id": "QjryZsuAS4",
        "assistant_phone_number": "18882346789"
      }
    }
  }
}
```
{: codeblock}


