---

copyright:
  years: 2015, 2021
lastupdated: "2021-12-06"

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

# CDR log event reference
{: #cdr-log-reference}

For `cdr_logged` events sent by a log webhook, the `payload` object contains data about a Call Detail Record (CDR) event that was handled by the phone integration. The `payload` object for a call detail record event contains the following keys:

|Key| Type| Description|
|-----|----|---|
|`primary_phone_number`| string| The phone number that was called. |
|`global_session_id`| string |The unique session identifier.|
|`failure_occurred`| boolean|Indicates whether a failure occurred during the call.|
|`failure_details`| string| Details about a failure.|
|`transfer_occurred`| boolean|Indicates whether an attempt was made to transfer a call|
|`active_calls`|  Number|Number of active calls when the call started.|
|`x-global-sip-trunk-call-id`|string| The value of the SIP trunk call ID header extracted from the initial SIP `INVITE` request. The following SIP trunk call ID headers are supported: <br><ul>_X-Twilio-CallSid_</ul><ul>_X-SID_</ul><ul>_X-Global-SIP-Trunk-Call-ID_</ul>  |
|`call`|JSON object| Contains information about the call.|
|`session_initiation_protocol`|JSON object| SIP protocol related details.|
|`max_response_milliseconds`|JSON object| Maximum latency for various services used during the call.|
|`assistant_interaction_summaries`|JSON array| Details about the {{site.data.keyword.conversationshort}} transactions that took place during the call.|
|`injected_custom_data`|JSON object| A JSON object that contains a set of key/value pairs. Extracted from the 	`cdr_custom_data` context variable.|
|`warnings_and_errors`| JSON array| An array of warnings and errors that were logged during the call.|
|`realtime_transport_network_summary`|JSON object| When RTCP is enabled, the `realtime_transport_network_summary` object provides statistics for the inbound stream in the `inbound_stream` object and statistics for the outbound stream in the `outbound_stream` object.|
{: caption="Table 1. Keys for the `payload` object" caption-side="top"}



The `call` object contains the following keys:


|Key| Type| Description|
|-----|----|---|
|`start_timestamp`| string. Time in the ISO format `yyyy-MM-ddTHH:mm:ss.SSSZ`|Time when the call started. |
|`stop_timestamp`| string. Time in the ISO format `yyyy-MM-ddTHH:mm:ss.SSSZ`|Time when the call ended. |
|`milliseconds_elapsed`| number| Length of the call in milliseconds. |
|`end_reason`| string| Call end reason:<br><ul>_assistant_transfer_</ul><ul> _assistant_hangup_</ul><ul>_caller_hangup_</ul><ul>_failed_ |
|`security.media_encrypted`| boolean|Indicates whether the media was encrypted. |
|`security.signaling_encrypted`| boolean|Indicates whether the SIP signaling was encrypted. |
|`security.sip_authenticated`| boolean|Indicates whether SIP authentication was used to challenge the authentication of the caller. |
{: caption="Table 2. Keys for the `call` object" caption-side="top"}


The `session_initiation_protocol` object contains the following keys:

|Key| Type|Description|
|-----|----|---|
|`invite_arrival_timestamp`|string. Time in the ISO format `yyyy-MM-ddTHH:mm:ss.SSSZ`| Time when the `INVITE` request arrived. |
|`setup_milliseconds`| number|Time it took to set up the call in milliseconds. Specifically, the field shows the time between when the initial SIP `INVITE` request was received and when the final SIP `ACK` request was received. |
|`headers.call_id`| string|The SIP `Call-ID` header field pulled from the SIP `INVITE` related to the call. |
|`headers.from_uri`|string| SIP URI from the initial SIP INVITE `From` field |
|`headers.to_uri`| string|SIP URI from the initial SIP INVITE `To` field |
{: caption="Table 3. Keys for the `session_initiation_protocol` object" caption-side="top"}

    
The `assistant_interaction_summaries` object contains the following keys:

|Key| Type|Description|
|-----|----|---|
|`assistant_id`| string|The unique identifier of the assistant. |
|`session_id`| string|The unique identifier of the session. |
|`turns`| JSON array|An array of the {{site.data.keyword.conversationshort}} transactions that took place during the conversation.|
{: caption="Table 4. Keys for the `assistant_interaction_summaries` object" caption-side="top"}

The `turn` object contains the following keys:

|Key| Type|Description|
|-----|----|---|
|`assistant.log_id`| string|A unique identifier for the logged transaction. Can be used to correlate between message logs and CDR events. |
|`assistant.start_timestamp`| string. Time in the ISO format `yyyy-MM-ddTHH:mm:ss.SSSZ`| Time when the request was sent to {{site.data.keyword.conversationshort}}. |
|`assistant.response_milliseconds`| number|Time between when the request was sent and when the response was received from {{site.data.keyword.conversationshort}}. |
|`request`| JSON object|A request sent to {{site.data.keyword.conversationshort}}.  |
|`response`| JSON array|An array of the `response` objects associated with the request.  |
{: caption="Table 5. Keys for the `turn` object" caption-side="top"}

The `request` object contains the following keys:

|Key| Type|Description|
|-----|----|---|
|`type`| string|The request type: <br><ul>_start_ - an initial request to {{site.data.keyword.conversationshort}}</ul><ul> _speech_to_text_ - a request is triggered on speech recognition	</ul><ul>_dtmf_ - a request is triggered when DTMF collection completes</ul><ul>_sms_ - a request is triggered when a SMS message is received from the caller</ul><ul> _post_response_timeout_ - a request is triggered when the post response timer expires </ul><ul> _redirect_ - a request is triggered when a call is redirected </ul><ul> _transfer_  - a request is triggered when a call is transferred </ul><ul> _transfer_failed_  - a request is triggered when a call transfer fails</ul><ul> _final_utterance_timeout_ - a request is triggered when the final utterance timer expires </ul><ul> _no_input_turn_ - a request is triggered when `no inpout turn` is enabled</ul><ul> _sms_failure_ - a request is triggered when a SMS message can't be sent to the caller </ul><ul> _speech_to_text_result_filtered_ - a request is triggered when an utterance is filtered due to low confidence level</ul><ul> _mrcp_recognition_unsuccessful_ - a request is triggered when the MRCP recognition completes without a final utterance</ul><ul> _network_warning_ - a request is triggered when a network error is detected </ul><ul> _media_capability_change_ - a request is triggered when media capabilities change in the middle of a call</ul>|
|`streaming_statistics`|JSON object|Contains information and statistics related to the {{site.data.keyword.speechtotextshort}} recognition.|

The `request.streaming_statistics` object contains the following keys:

|Key| Type| Description|
|-----|----|---|
|`transaction_id`| string|A unique identifier of the transaction.  |
|`start_timestamp`| string. Time in the ISO format `yyyy-MM-ddTHH:mm:ss.SSSZ`| Time when the transaction started.  |
|`stop_timestamp`| string. Time in the ISO format `yyyy-MM-ddTHH:mm:ss.SSSZ`| Time when the transaction ended.  |
|`response_milliseconds`|number|Latency in milliseconds between when silence is detected in the caller's speech and a final result from {{site.data.keyword.speechtotextshort}} is received.  |
|`echo_detected`| boolean|Indicates whether an echo was detected. The value can be `true` or `false`.  |
|`confidence`| number|The confidence score of the final utterance.  |
{: caption="Table 6. Keys for the `request.streaming_statistics` object" caption-side="top"}



The `response` object contains the following keys:

|Key| Type| Description|
|-----|----|---|
|`type`| string| The response type: <br><ul>_text_to_speech_ - a command to play an utterance to the caller </ul><ul>_sms_ - a command to send a SMS to the caller</ul><ul>_url_ - a command to play an audio file to the caller</ul><ul>_transfer_ - a command to transfer a call </ul><ul>_text_to_speech_config_ - a command to change {{site.data.keyword.texttospeechshort}} settings </ul><ul>_speech_to_text_config_ - a command to change the {{site.data.keyword.speechtotextshort}} settings </ul><ul>_pause_speech_to_text_ - a command to stop speech recognition  </ul><ul>_unpause_speech_to_text_ - a command to start speech recognition</ul><ul>_pause_dtmf_ - a command to stop DTMF recognition</ul><ul>_unpause_dtmf_ - a command to start speech recognition</ul><ul>_enable_speech_barge_in_ - a command to enable speech barge-in so that callers can interrupt playback by speaking </ul><ul>_disable_speech_barge_in_ - a command to disable speech barge-in so that playback isn't interrupted when callers speak over top of the played back audio</ul><ul>_enable_dtmf_barge_in_ - a command to enables DTMF barge-in so that callers can interrupt playback from the phone integration by pressing a key. </ul><ul>_disable_dtmf_barge_in_ - a command to disable DTMF barge-in so that playback from the phone integration isn't interrupted when callers press keys. </ul><ul>_dtmf_ - a command to send DTMFs to the caller </ul><ul>_hangup_ - a command to disconnect a call </ul>  |
|`barge_in_occurred`| boolean|Indicates whether barge-in occurred during the turn.  |
|`streaming_statistics`| JSON object|Contains information and statistics related to the {{site.data.keyword.texttospeechshort}} synthesis and playback.  |
{: caption="Table 6. Keys for the `response` object" caption-side="top"}



The `response.streaming_statistics` object contains the following keys:

|Key| Type|Description|
|-----|----|---|
|`transaction_id`| string|A unique identifier of the transaction.  |
|`start_timestamp`| string. Time in the ISO format `yyyy-MM-ddTHH:mm:ss.SSSZ`| Time when the transaction started.  |
|`stop_timestamp`| string. Time in the ISO format `yyyy-MM-ddTHH:mm:ss.SSSZ`| Time when the transaction ended.  |
|`response_milliseconds`|number|Time in milliseconds between when a text utterance is sent to the {{site.data.keyword.texttospeechshort}} service and when the phone integration receives the first packet of synthesized audio.  |
{: caption="Table 7. Keys for the `response.streaming_statistics` object" caption-side="top"}


The `max_response_milliseconds` object contains the following keys:

|Key| Type|Description|
|-----|----|---|
|`assistant`| number|Maximum round-trip latency in milliseconds, calculated from all {{site.data.keyword.conversationshort}} requests related to the call. |
|`text_to_speech`| number|Maximum time in milliseconds between when a text utterance is sent to the {{site.data.keyword.texttospeechshort}} service and when the phone integration receives the first packet of synthesized audio. Calculated from all the {{site.data.keyword.texttospeechshort}} requests related to this call. |
|`speech_to_text`| number|Maximum latency in milliseconds between when silence is detected in the user's speech and a final result from {{site.data.keyword.speechtotextshort}} is received. This value is calculated from all the {{site.data.keyword.speechtotextshort}} recognition results related to this call. |
{: caption="Table 8. Keys for the `max_response_milliseconds` object" caption-side="top"}


#### Mapping between CDR and Watson Assistant response types
{: #webhook-log-cdr-response-type-mapping}

|CDR response type| Watson Assistant response type|
|-----|----|
|`text_to_speech`| `text` |
|`url`| `audio` |
|`dtmf`| `dtmf`, `command_info.type` : `send` |
|`sms`| `user_defined`,  `vgwAction.command` : `vgwActSendSMS`|
|`transfer`| `connect_to_agent` |
|`text_to_speech_config`| `text_to_speech`, `command_info.type` : `configure` |
|`speech_to_text_config`| `speech_to_text`, `command_info.type` : `configure` |
|`unpause_speech_to_text`| `start_activities`, `type`:`speech_to_text_recognition` |
|`pause_speech_to_text`| `stop_activities`, `type`:`speech_to_text_recognition` |
|`unpause_dtmf`| `start_activities`, `type`:`dtmf_collection`|
|`pause_dtmf`| `stop_activities`, `type`:`dtmf_collection` |
|`enable_speech_barge_in`| `text_to_speech`, `command_info.type` : `enable_barge_in` |
|`disable_speech_barge_in`| `text_to_speech`, `command_info.type` : `disable_barge_in` |
|`enable_dtmf_barge_in`| `dtmf`, `command_info.type` : `enable_barge_in` |
|`disable_dtmf_barge_in`| `dtmf`, `command_info.type` : `disable_barge_in` |
|`hangup`| `end_session` |


#### Warning details
{: #webhook-log-cdr-warning-details}

The  `warnings_and_errors`  object contains warnings and errors that were logged during the call, listed in order of occurrence. Warnings for the following conditions are included:

-   Messages when utterances are filtered out by the confidence score threshold.
-  {{site.data.keyword.texttospeechshort}} underflows, which is when {{site.data.keyword.texttospeechshort}} synthesis can't keep up with the phone integration streaming rate and audio might skip.
-   RTP network warnings, such as high packet loss or high average jitter, if RTCP is enabled

```plaintext

  "warnings_and_errors": [
    {
      "message": "CWSMR0032W: A Watson Speech to Text final utterance has a confidence score of 0.1, which does not meet the confidence score threshold of 0.2. The utterance will be ignored.",
      "id": "CWSMR0032W"
    },
    {
      "message": "CWSMR0031W: The synthesis stream from the Watson Text To Speech service can't keep up with the playback rate to the caller, so audio might skip. transaction ID=a1b2c3d4e5",
      "id": "CWSMR0031W"
    }
  ]


```

The object for each warning contains the following keys:

|Key|Type|Description|
|---|----|---|
|`message`|string|The text of the warning message that was logged. |
|`id`| string|The unique message identifier. |
{: caption="Table 9. Keys for the `warnings_and_errors` object" caption-side="top"}



#### RTP network summary details
{: #webhook-log-cdr-rtp-network-summary-details}

When RTCP is enabled, each  `realtime_transport_network_summary`  object provides statistics for the inbound stream in the  `inbound_stream`  object and statistics for the outbound stream in the  `outbound_stream`  object.

```json
"realtime_transport_network_summary": {
  "inbound_stream": {
      "maximum_jitter": 5,
      "average_jitter": 1,
      "packets_lost": 0,
      "packets_transmitted": 1000,
      "canonical_name": "user@example.com",
      "tool_name": "User SIP Phone"
   },
  "outbound_stream": {
      "maximum_jitter": 5,
      "average_jitter": 1,
      "packets_lost": 0,
      "packets_transmitted": 2000,
      "canonical_name": "voice.gateway@127.0.0.1",
      "tool_name": "IBM Voice Gateway/1.0.0.5"
   }
}

```     
{: codeblock}


The objects for each stream contain the following keys:


|Key| Type|Description|
|---|---|---|
|`maximum_jitter`|  Number| Maximum jitter during the call. |
|`average_jitter`|  Number| Average jitter, calculated over the call duration. |
|`packets_lost`|  Number| An estimate of the number of packets that were lost during the call. |
|`packets_transmitted`| Number| An estimate of the total number of packets that were transmitted during the call. |
|`canonical_name`|string|A unique identifier for the sender of the stream, typically in  _@_  format. |
|`tool_name`| string|The name of the application or tool where the stream originated. For Voice Gateway, the default is `IBM Voice Gateway/  `. |
{: caption="Table 10. Keys for RTP network summary details"  caption-side="top"}

