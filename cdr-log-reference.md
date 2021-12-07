---

copyright:
  years: 2015, 2021
lastupdated: "2021-12-07"

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

For `cdr_logged` events sent by a log webhook, the `payload` object contains data about a Call Detail Record (CDR) event that was handled by the phone integration. The `payload` object for a call detail record event contains the following properties:

| Property               | Type    | Description |
|------------------------|---------|-------------|
| `primary_phone_number` | string  | The phone number that was called. |
| `global_session_id`    | string  | The unique session identifier.    |
| `failure_occurred`     | boolean | Whether a failure occurred during the call. |
| `failure_details`      | string  | Details about any failure that occurred. |
| `transfer_occurred`    | boolean | Whether an attempt was made to transfer a call. |
| `active_calls`         | Number  | The number of active calls when the call started. |
| `x-global-sip-trunk-call-id` | string | The value of the SIP trunk call ID header extracted from the initial SIP `INVITE` request. The following SIP trunk call ID headers are supported: \n - `X-Twilio-CallSid` \n - `X-SID` \n - `X-Global-SIP-Trunk-Call-ID` |
| `call`                 | Object  | Information about the call. See [`call`](#cdr-log-reference-call). |
| `session_initiation_protocol` | Object | SIP protocol related details. See [`session_initiation_protocol`](#cdr-log-reference-session_initiation_protocol). |
| `max_response_milliseconds`| Object | Maximum latency for services used during the call. |
| `assistant_interaction_summaries` | Array | Details about the {{site.data.keyword.conversationshort}} interactions that took place during the call. See [`assistant_interaction_summaries`](#cdr-log-reference-assistant_interaction_summaries). |
| `injected_custom_data` | Object  | A set of key/value pairs extracted from the `cdr_custom_data` context variable. |
| `warnings_and_errors`  | Array   | Any warnings or errors that were logged during the call. See [`warnings_and_errors`](#cdr-log-reference-warnings_and_errors). |
| `realtime_transport_network_summary` | Object | Statistics for the inbound stream in the `inbound_stream` object and statistics for the outbound stream in the `outbound_stream` object. Included only if RTCP is enabled. See [`realtime_transport_network_summary`](#cdr-log-reference-realtime_transport_network_summary). |
{: caption="Properties of the CDR webhook `payload` object" caption-side="top"}

## `call`
{: #cdr-log-reference-call}

The `call` object contains the following properties:

| Property         | Type | Description |
|------------------|------|-------------|
| `start_timestamp`| String | The time when the call started, in ISO format (`yyyy-MM-ddTHH:mm:ss.SSSZ`). |
| `stop_timestamp` | String | The time when the call ended, in ISO format (`yyyy-MM-ddTHH:mm:ss.SSSZ`). |
| `milliseconds_elapsed` | Number| The duration of the call, in milliseconds. |
| `end_reason`     | string | The reason the call ended. The possible reasons are as follows: \n - assistant_transfer \n - assistant_hangup \n - caller_hangup \n -failed |
| `security.media_encrypted` | Boolean | Whether the media was encrypted. |
| `security.signaling_encrypted` | Boolean| Whether the SIP signaling was encrypted. |
| `security.sip_authenticated` | Boolean | Whether SIP authentication was used to authenticate the caller. |
{: caption="Properties of the `call` object" caption-side="top"}

## `session_initiation_protocol`
{: #cdr-log-reference-session_initiation_protocol}

The `session_initiation_protocol` object contains the following properties:

| Property             | Type  | Description |
|----------------------|-------|-------------|
| `invite_arrival_timestamp` | String | The time when the `INVITE` request arrived, in ISO format (`yyyy-MM-ddTHH:mm:ss.SSSZ`). |
| `setup_milliseconds` | Number | The time it took to set up the call, in milliseconds. This is the time between when the initial SIP `INVITE` request was received and when the final SIP `ACK` request was received. |
| `headers.call_id`    | String | The SIP `Call-ID` header field pulled from the SIP `INVITE` related to the call. |
| `headers.from_uri`   | String | The SIP URI from the initial SIP INVITE `From` header. |
| `headers.to_uri`     | String | The SIP URI from the initial SIP INVITE `To` header. |
{: caption="Properties of the `session_initiation_protocol` object" caption-side="top"}

## `assistant_interaction_summaries`
{: #cdr-log-reference-assistant_interaction_summaries}

The `assistant_interaction_summaries` object contains the following properties:

| Property       | Type   | Description |
|----------------|--------|-------------|
| `assistant_id` | String | The unique identifier of the assistant. |
| `session_id`   | String | The unique identifier of the session. |
| `turns`        | Array  | An array of objects describing the {{site.data.keyword.conversationshort}} interactions that took place during the conversation. See [`assistant_interaction_summaries.turns[]`](#cdr-log-reference-turns). |
{: caption="Properties of the `assistant_interaction_summaries` object" caption-side="top"}

### `assistant_interaction_summaries.turns[]`
{: #cdr-log-reference-turns}

The objects in the `assistant_interaction_summaries.turns` array contain the following properties:

| Prpoerty           | Type   | Description |
|--------------------|--------|-------------|
| `assistant.log_id` | String | A unique identifier for the logged event. This can be used to correlate between message logs and CDR events. |
| `assistant.start_timestamp` | String | The time when the request was sent to the assistant, in ISO format (`yyyy-MM-ddTHH:mm:ss.SSSZ`). |
| `assistant.response_milliseconds` | Number | The time (in milliseconds) between when the request was sent and when the response was received from the assistant. |
| `request`          | Object | A request sent to the assistant. See [`assistant_interaction_summaries.turns[].request`](#cdr-log-reference-request). |
| `response`         | Array  | An array of the `response` objects associated with the request. |
{: caption="Properties of the objects in the `assistant_interaction_summaries.turns[]` array" caption-side="top"}

#### `assistant_interaction_summaries.turns[].request`
{: #cdr-log-reference-request}

The `assistant_interaction_summaries.turns[].request` object contains the following properties:

| Property | Type   | Description |
|----------|--------|-------------|
| `type`   | String | The request type: \n - `start`: an initial request to the assistant is received \n - `speech_to_text`: a request for the {{site.data.keyword.speechtotextshort}} service is received \n - `dtmf`: DTMF collection completes \n - `sms`: an SMS message is received from the caller \n - `post_response_timeout`: the post-response timer expires \n - `redirect`: a call is redirected  \n - `transfer`: a call is transferred \n - `transfer_failed`: a call transfer fails \n - `final_utterance_timeout`: the final utterance timer expires \n - `no_input_turn`: `no inpout turn` is enabled \n - `sms_failure`: an SMS message cannot be sent to the caller \n - `speech_to_text_result_filtered`: an utterance is filtered due to low confidence level \n - `mrcp_recognition_unsuccessful`: the MRCP recognition completes without a final utterance \n - `network_warning`: a network error is detected \n - `media_capability_change`: media capabilities change during a call |
| `streaming_statistics` | Object| Information and statistics related to the {{site.data.keyword.speechtotextshort}} recognition. See [`assistant_interaction_summaries.turns[].request.streaming_statistics`](#cdr-log-reference-request-streaming_statistics). |
{: caption="Properties of the `assistant_interaction_summaries.turns[].request` object" caption-side="top"}

##### `assistant_interaction_summaries.turns[].request.streaming_statistics`
{: #cdr-log-reference-request-streaming_statistics}

The `assistant_interaction_summaries.turns[].request.streaming_statistics` object contains the following properties:

| Property         | Type    | Description |
|------------------|---------|-------------|
| `transaction_id` | String  | A unique identifier of the transaction. |
| `start_timestamp`| String  | The time when the transaction started, in ISO format (`yyyy-MM-ddTHH:mm:ss.SSSZ`). |
| `stop_timestamp` | String  | The time when the transaction ended, in ISO format (`yyyy-MM-ddTHH:mm:ss.SSSZ`).   |
| `response_milliseconds` | Number | The latency (in milliseconds) between when silence is detected in the caller's speech and a final result from the assistant is received. |
| `echo_detected`  | Boolean | Whether an echo was detected. |
| `confidence`     | Number  | The confidence score of the final utterance. |
{: caption="Properties of the `assistant_interaction_summaries.turns[].streaming_statistics` object" caption-side="top"}

#### `assistant_interaction_summaries.turns[].response`
{: #cdr-log-reference-response}

The `assistant_interaction_summaries.turns[].response` object contains the following properties:

| Property           | Type    | Description |
|--------------------|---------|-------------|
| `type`             | String  | The response type: \n - `text_to_speech`: a command to play an utterance to the caller \n - `sms`: a command to send an SMS message to the caller \n - `url`: a command to play an audio file to the caller \n - `transfer`: a command to transfer a call \n - `text_to_speech_config`: a command to change the {{site.data.keyword.texttospeechshort}} settings \n - `speech_to_text_config`: a command to change the {{site.data.keyword.speechtotextshort}} settings \n - `pause_speech_to_text`: a command to stop speech recognition \n - `unpause_speech_to_text`: a command to start speech recognition \n - `pause_dtmf`: a command to stop DTMF recognition \n - `unpause_dtmf`: a command to start speech recognition \n - `enable_speech_barge_in`: a command to enable speech barge-in so that callers can interrupt playback by speaking \n - `disable_speech_barge_in`: a command to disable speech barge-in so that playback isn't interrupted when callers speak during audio playback \n - `enable_dtmf_barge_in`: a command to enable DTMF barge-in so that callers can interrupt playback from the phone integration by pressing a key \n - `disable_dtmf_barge_in`: a command to disable DTMF barge-in so that playback from the phone integration isn't interrupted when the caller presses a key \n - `dtmf`: a command to send DTMF signals to the caller \n - `hangup`: a command to disconnect the call \n See [Mapping between CDR and {{site.data.keyword.conversationshort}} response types](#cdr-log-reference-response-type-mapping). |
| `barge_in_occurred`| Boolean | Whether barge-in occurred during the turn. |
| `streaming_statistics`| Object | Information and statistics related to {{site.data.keyword.texttospeechshort}} synthesis and playback. See [`assistant_interaction_summaries.turns[].response.streaming_statistics`](#cdr-log-reference-response-streaming_statistics). |
{: caption="Properties of the `assistant_interaction_summaries.turns[].response` object" caption-side="top"}

##### Mapping between CDR and {{site.data.keyword.conversationshort}} response types
{: #cdr-log-reference-response-type-mapping}

The values of the `type` property map to {{site.data.keyword.conversationshort}} response types as follows:

| CDR response type | {{site.data.keyword.conversationshort}} response type |
|-------------------|-------------------------------------------------------|
| `text_to_speech`  | `text` |
| `url`             | `audio` |
| `dtmf`            | `dtmf`, `command_info.type` : `send` |
| `sms`             | `user_defined`,  `vgwAction.command` : `vgwActSendSMS` |
| `transfer`        | `connect_to_agent` |
| `text_to_speech_config` | `text_to_speech`, `command_info.type` : `configure` |
| `speech_to_text_config` | `speech_to_text`, `command_info.type` : `configure` |
| `unpause_speech_to_text` | `start_activities`, `type`:`speech_to_text_recognition` |
| `pause_speech_to_text` | `stop_activities`, `type`:`speech_to_text_recognition` |
| `unpause_dtmf`    | `start_activities`, `type`:`dtmf_collection` |
| `pause_dtmf`      | `stop_activities`, `type`:`dtmf_collection` |
| `enable_speech_barge_in` | `text_to_speech`, `command_info.type` : `enable_barge_in` |
| `disable_speech_barge_in` | `text_to_speech`, `command_info.type` : `disable_barge_in` |
| `enable_dtmf_barge_in` | `dtmf`, `command_info.type` : `enable_barge_in` |
| `disable_dtmf_barge_in` | `dtmf`, `command_info.type` : `disable_barge_in` |
| `hangup`          | `end_session` |

##### `assistant_interaction_summaries.turns[].response.streaming_statistics`
{: #cdr-log-reference-response-streaming_statistics}

The `assistant_interaction_summaries.turns[].response.streaming_statistics` object contains the following properties:

| Property         | Type   | Description |
|------------------|--------|---|
| `transaction_id` | String | A unique identifier of the transaction. |
| `start_timestamp`| String | The time when the transaction started, in ISO format (`yyyy-MM-ddTHH:mm:ss.SSSZ`). |
| `stop_timestamp` | String | The time when the transaction ended, in ISO format (`yyyy-MM-ddTHH:mm:ss.SSSZ`). |
| `response_milliseconds` | Number | The time (in milliseconds) between when a text utterance is sent to the assistant and when the phone integration receives the first packet of synthesized audio. |
{: caption="Properties of the `assistant_interaction_summaries.turns[].response.streaming_statistics` object" caption-side="top"}

## `warnings_and_errors`
{: #cdr-log-reference-warnings_and_errors}

The `warnings_and_errors` object contains warnings and errors that were logged during the call, listed in order of occurrence. Warnings for the following conditions are included:

- Messages when utterances are filtered out by the confidence score threshold.
- {{site.data.keyword.texttospeechshort}} underflows, which is when {{site.data.keyword.texttospeechshort}} synthesis can't keep up with the phone integration streaming rate and audio might skip.
-  RTP network warnings, such as high packet loss or high average jitter, if RTCP is enabled.

The following example shows the structure of the `warnings_and_errors` object:

```json
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

The object for each warning contains the following properties:

| Property  | Type   | Description |
|-----------|--------|-------------|
| `message` | String | The text of the warning message. |
| `id`      | String | The unique message identifier.   |
{: caption="Properties of the `warnings_and_errors` object" caption-side="top"}

## `max_response_milliseconds`
{: #cdr-log-reference-max_response_milliseconds}

The `max_response_milliseconds` object contains the following properties:

| Property         | Type   | Description |
|------------------|--------|-------------|
| `assistant`      | Number | The maximum round-trip latency (in milliseconds), calculated from all {{site.data.keyword.conversationshort}} requests related to the call. |
| `text_to_speech` | Number | The maximum time (in milliseconds) between when a text utterance is sent to the assistant and when the phone integration receives the first packet of synthesized audio. This value is calculated from all {{site.data.keyword.texttospeechshort}} requests related to the call. |
| `speech_to_text` | Number | The maximum latency (in milliseconds) between when silence is detected in the caller's speech and when a final result from the {{site.data.keyword.speechtotextshort}} service is received. This value is calculated from all {{site.data.keyword.speechtotextshort}} recognition results related to the call. |
{: caption="Properties of the `max_response_milliseconds` object" caption-side="top"}

## `realtime_transport_network_summary`
{: #cdr-log-reference-realtime_transport_network_summary}

When RTCP is enabled, the `realtime_transport_network_summary` object provides statistics for the inbound stream in the `inbound_stream` object and statistics for the outbound stream in the `outbound_stream` object.

The following example shows the structure of the `realtime_transport_network_summary` object:

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

The object for each stream contains the following properties:

| Properties       | Type   | Description |
|------------------|--------|-------------|
| `maximum_jitter` | Number | The maximum jitter during the call. |
| `average_jitter` | Number | The average jitter, calculated over the duration of the call. |
| `packets_lost`   | Number | An estimate of the number of packets that were lost during the call. |
| `packets_transmitted` | Number | An estimate of the total number of packets that were transmitted during the call. |
| `canonical_name` | String | A unique identifier for the sender of the stream, typically in `@` format. |
| `tool_name`      | String | The name of the application or tool where the stream originated. For IBM Voice Gateway, the default is `IBM Voice Gateway/  `. |
{: caption="Properties of the `realtime_transport_network_summary` object"  caption-side="top"}

