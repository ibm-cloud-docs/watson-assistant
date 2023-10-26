---

copyright:
  years: 2020, 2023
lastupdated: "2023-10-26"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# *SMS* integration reference
{: #sms-reference}

Add action commands to the message `context` object to manage the flow of conversations with customers who interact with your assistant by submitting SMS messages over the telephone.
{: shortdesc}

Learn about the supported commands and reserved context variables that are used by the *SMS* integration.

## Supported commands
{: #sms-reference-actions}

Each action consists of a `command` property, followed by an optional `parameter` property to define parameters for commands that require them. The commands that are described in the following table are supported by the *SMS* integration.

| Action command | Description | Parameters |
| ----- | ----- | ----- |
| `terminateSession` | Ends the current SMS session. Use this command to ensure that the subsequent text message starts a new assistant-level session which does not retain any context values from the current session. | None |
| `smsActSendMedia` | Enables MMS messaging.  | `mediaURL`: Specifies a JSON array of publicly accessible media URLs that are sent to the user. |
| `smsActSetDisambiguationConfig` | Configures how to handle the choices that are displayed in a disambiguation list. | `prefixText`: Text to include before each option. For example, `Press %s for` where `%s` represents the number corresponding to a list choice; this is replaced with the actual number at run time. |
| `smsActSetOptionsConfig` | Configures how to handle option response types. | `prefixText`: Text to include before each option. For example, `Press %s for` where `%s` represents the number corresponding to a list choice; this is replaced with the actual number at run time. |
{: caption="Table 1. Actions that you can initiate from the action" caption-side="top"}

## Reserved context variables
{: #sms-reference-context-variables}

The following table describes the context variables that have special meaning in the context of the *SMS* integration. They should not be used for any purpose other than the documented use.

Table 2 describes the context variables that are set by your action. Table 3 describes the context variables that you can set by the *SMS* integration.

### Table 2. Context variables that are set by your action
{: #sms-reference-context-variables-set-by-action}

| Context variable name | Expected value | Description |
| --------------------- | -------------- | ----------- |
| `smsConversationResponseTimeout` | Time in ms | The amount of time in milliseconds that the integration waits to receive a response from the action. If the time limit is exceeded, the integration attempts to contact the action again. If the service still can't be reached, the SMS response fails. |
{: caption="Table 2. SMS context variables set by the action" caption-side="top"}

### Table 3. Context variables that are set by the integration
{: #sms-reference-context-variables-set-by-integration}

| Context variable name | Description |
| --------------------- | ----------- |
| `smsTenantPhoneNumber` | The integration tenant phone number that the user is messaging. |
| `smsUserPhoneNumber` | The phone number of the user that is exchanging messages with the integration. |
| `smsUserData` | Data in JSON format to be passed verbatim to the service orchestration engine or {{site.data.keyword.conversationshort}} service. This variable is sent only if the session is started from the integration tenant and the data is sent through the REST API. |
| `smsSessionTimeoutCount` | The session timeout value. This variable is sent only if the timeout value is defined through the REST API. |
| `smsError` | When the integration fails to send an SMS message, this variable contains details about the error that occurred.  |
| `smsSessionID` | The globally unique identifier (GUID) for the related SMS Gateway session. |
| `smsMedia` | The `arraylist` of `mediaURL` and corresponding `mediaContentType`. This context variable is cleared at the end of each conversation turn. |
{: caption="Table 3. SMS context variables set by the integration" caption-side="top"}
