---

copyright:
  years: 2015, 2024
lastupdated: "2024-12-20"

subcollection: watson-assistant


---

{{site.data.keyword.attribute-definition-list}}

# Migrating to the v2 API
{: #api-migration}

The {{site.data.keyword.conversationshort}} v2 runtime API, which supports the use of assistants and skills, was introduced in November 2018. This API offers significant advantages over the v1 runtime API, including automatic state management, ease of deployment, skill versioning, and the availability of new features such as the search skill.

The v2 API is available for all users, regardless of service plan, at no additional cost.

The v2 API currently supports only runtime interaction with an existing assistant. Authoring applications that create or modify workspaces should continue to use the v1 API.
{: note}

## Overview
{: #api-migration-overview}

With the v2 API, your client app communicates with an assistant, which is an orchestration layer that offers several capabilities, including automatic state management, skill versioning, and easier deployment.

All communication with an assistant takes place within the context of a _session_, which maintains conversation state throughout the duration of the conversation. State data, including any context variables that are defined by your dialog or client application, are automatically stored by {{site.data.keyword.conversationshort}}, without any action required on the part of your application.

State data persists until you explicitly delete the session, or until the session times out because of inactivity.

If you prefer to manage state yourself, the v2 API also provides a stateless `message` method that functions more like the v1 API. If you use the stateless `message` method, you do not need to explicitly create or delete sessions, and your app is responsible for maintaining context. For more information about the stateless `message` method, see the [API Reference](/apidocs/assistant-v2#messagestateless){: external}.
{: note}

If you have an existing application that uses the v1 API to send user input directly to a workspace, migrating your app to use the v2 API is a straightforward process.

## Assistant ID
{: #api-migration-setup}

The v2 runtime API sends messages to an assistant. On the **Assistant Settings** page, find the assistant ID. Your application uses this ID to communicate with the assistant. The service credentials are the same for both the v1 and v2 APIs.

Currently, there is no API support for retrieving an assistant ID. To find the assistant ID, you must use the {{site.data.keyword.conversationshort}} user interface.
{: note}

## Call the v2 runtime API
{: #api-migration-call}

After you create an assistant, you can update your client application to use the v2 runtime API instead of the v1 runtime API.

1. Before sending the first message in a conversation, use the v2 [**Create a session**](/apidocs/assistant-v2#createsession){: external} method to create a session. Save the returned session ID:

   ```javascript
   service
   .createSession({
    assistant_id: assistantId,
   })
   .then(res => {
    sessionId = res.session_id;
   })
   ```
   {: codeblock}
   {: javascript}

   ```python
   session_id = service.create_session(
      assistant_id = assistant_id
   ).get_result()['session_id']
   ```
    {: codeblock }
    {: python}

   ```java
   CreateSessionOptions createSessionOptions = new CreateSessionOptions.Builder(assistantId).build();
   SessionResponse session = service.createSession(createSessionOptions).execute().getResult();
   String sessionId = session.getSessionId();
   ```
   {: codeblock}
   {: java}

1. Use the v2 [**Send user input to assistant**](/apidocs/assistant-v2#message){: external} method to send user input to the assistant. Instead of specifying the workspace ID as you did with the v1 API, you specify the assistant ID and the session ID:

   ```javascript
   service
     .message({
       assistant_id: assistantId,
       session_id: sessionId,
       input: messageInput
     })
   ```
   {: codeblock}
   {: javascript}

   ```python
    response = service.message(
       assistant_id,
       session_id,
       input = message_input
    ).get_result()
    ```
    {: codeblock}
    {: python}

   ```java
    MessageInput input = new MessageInput.Builder().text(inputText).build();
    MessageOptions messageOptions = new MessageOptions.Builder(assistantId, sessionId)
      .input(input)
      .build();
    MessageResponse response = service.message(messageOptions)
      .execute()
      .getResult();
   ```
   {: codeblock}
   {: java}

   The basic message structure has not changed; in particular, the user input is still sent as `input.text`.

1. After a conversation ends, use the v2 [**Delete session**](/apidocs/assistant-v2#deletesession){: external} method to delete the session.

   ```javascript
   service
     .deleteSession({
       assistant_id: assistantId,
       session_id: sessionId,
     })
   ```
   {: codeblock}
   {: javascript}

   ```python
   service.delete_session(
       assistant_id = assistant_id,
       session_id = session_id
   )
   ```
   {: codeblock}
   {: python}

   ```java
   DeleteSessionOptions deleteSessionOptions = new DeleteSessionOptions.Builder(assistantId, sessionId
     .build();
   service.deleteSession(deleteSessionOptions).execute();
   ```
   {: codeblock}
   {: java}

   If you do not explicitly delete the session, it will be automatically deleted after the configured timeout interval. The timeout duration depends on your plan.

To see examples of the v2 APIs in the context of a simple client application, see [Building a custom client using the API](/docs/watson-assistant?topic=watson-assistant-api-client).

## Handle the v2 response format
{: #api-migration-handle-response-format}

Your application might need to be updated to handle the v2 runtime response format, depending on which parts of the response your application needs to access:

- Output for all response types (such as `text` and `option`) are still returned in the `output.generic` object. Application code for handling these responses should work without modification.

- Detected intents and entities are now returned as part of the `output` object, rather than at the root of the response JSON.

- The conversation context is now organized into two objects:

   - The **global context** contains system-level context data that is shared by all skills in the assistant.

   - The **skill context** contains any user-defined context variables that are used by your dialog skill.

   However, keep in mind that state data, including conversation context, is now maintained by the assistant, so your application might not need to access the context at all (see [Let the assistant maintain state](#api-migration-state)).

Refer to the v2 [API Reference ](/apidocs/assistant-v2#message){: external} for complete documentation of the v2 response format.

## Let the assistant maintain state
{: #api-migration-state}

For most applications, you can now remove any code included for maintaining state. It is no longer necessary to save the context and send it back to {{site.data.keyword.conversationshort}} with each turn of the conversation. The context is automatically maintained by {{site.data.keyword.conversationshort}} and can be accessed by your dialog as before.

Note that with the v2 API, the context is by default not included in responses to the client application. However, your code can still access context variables if necessary:

- You can still send a `context` object as part of the message input. Any context variables that you include are stored as part of the context maintained by {{site.data.keyword.conversationshort}}. (If the context variable you send already exists in the context, the new value overwrites the previously stored value.)

   Make sure the context object that you send conforms to the v2 format. All user-defined context variables that are sent by your application should be part of the skill context; typically, the only global context variable you might need to set is `system.user_id`, which is used by Plus and Premium plans for billing purposes.

- You can still retrieve context variables from either the global or skill context. To have the `context` object included with message responses, use the **return_context** property in the message input options. For more information, see [Accessing context data in dialog](/docs/watson-assistant?topic=watson-assistant-api-client-get-context).
