---

copyright:
  years: 2019, 2022
lastupdated: "2022-09-08"

subcollection: watson-assistant

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:deprecated: .deprecated}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:preview: .preview}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:video: .video}

# Building a custom client using the API
{: #api-client}

If none of the built-in integrations meet your requirements, you can deploy your assistant by developing a custom client application that interacts with your users and communicates with the {{site.data.keyword.conversationfull}} service.
{: shortdesc}

The Watson SDKs help you write code that interacts with {{site.data.keyword.conversationshort}}. For more information about the SDKs, see [Watson SDKs](/docs/assistant?topic=watson-using-sdks).

## Setting up the assistant
{: #api-client-setup}

The example application we will create in this section implements several simple functions to illustrate how a client application interacts with {{site.data.keyword.conversationshort}}. The application code will collect input and send it to an assistant, which sends responses the application will display to the user.

If you want to try this example yourself, first you need to set up the simple example assistant that the client will connect to:

1. Download the actions <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/assistant/assistant-simple-example-v2.json" download="assistant-simple-example-v2.json">JSON file</a>.
1. [Create an assistant](/docs/watson-assistant?topic=watson-assistant-assistant-add).
1. In the new assistant, [open the global action settings](/docs/watson-assistant?topic=watson-assistant-actions-global-settings). Go to the **Upload/Download** tab and import the actions from the file you downloaded.

The example actions include a *Greet customer* action that asks the customer's name, and simple actions for making and canceling appointments.

## Getting service information
{: #api-client-get-info}

To access the {{site.data.keyword.conversationshort}} REST APIs, your application needs to be able to authenticate with {{site.data.keyword.Bluemix}} and connect to the assistant in the environment where it is deployed. You'll need to copy the service credentials and environment ID and paste them into your application code. You'll also need the URL for the location of your service instance (for example, `https://api.us-south.assistant.watson.cloud.ibm.com`).

To access the service credentials and the environment ID from the {{site.data.keyword.conversationshort}} user interface, follow these steps:

1. Go to the **Environments** page and click the tab for the environment you want to connect to.

1. Click the ![Environment settings icon](images/gear-icon-black.png) icon to open the environment settings.

1. Select **API details** to see details for the environment, including the URL, assistant ID, and API key.

The URL shown in the **Environment URL** field is an example URL for the `sessions` endpoint. You must edit this URL to remove everything after the instance ID. For more information about the service instance URL, see the [API reference](https://cloud.ibm.com/apidocs/assistant/assistant-v2#endpoint-cloud){: external}. 
{: note}

## Communicating with the {{site.data.keyword.conversationshort}} service
{: #api-client-communicate}

Interacting with the {{site.data.keyword.conversationshort}} service from your client application is simple. We'll start with an example that connects to the service, sends a single empty message, and prints the output to the console:

```javascript
// Example 1: Creates service object, sends initial message, and
// receives response.

const AssistantV2 = require('ibm-watson/assistant/v2');
const { IamAuthenticator } = require('ibm-watson/auth');

// Create Assistant service object.
const assistant = new AssistantV2({
  version: '2020-09-24',
  authenticator: new IamAuthenticator({
    apikey: '{apikey}', // replace with API key
  }),
  url: '{url}', // replace with URL
});

const assistantId = '{assistant_id}'; // replace with assistant ID

// Start conversation with empty message
messageInput = {
  messageType: 'text',
  text: '',
};
sendMessage(messageInput);

// Send message to assistant.
function sendMessage(messageInput) {
  assistant
    .messageStateless({
      assistantId,
      input: messageInput,
    })
    .then(res => {
      processResponse(res.result);
    })
    .catch(err => {
      console.log(err); // something went wrong
    });
}

// Process the response.
function processResponse(response) {
  // Display the output from assistant, if any. Supports only a single
  // text response.
  if (response.output.generic) {
    if (response.output.generic.length > 0) {
      if (response.output.generic[0].response_type === 'text') {
        console.log(response.output.generic[0].text);
        }
      }
    }
  }
```
{: codeblock}
{: javascript}

```python
# Example 1: Creates service object, sends initial message, and
# receives response.

from ibm_watson import AssistantV2
from ibm_cloud_sdk_core.authenticators import IAMAuthenticator

# Create Assistant service object.
authenticator = IAMAuthenticator('{apikey}') # replace with API key
assistant = AssistantV2(
    version = '2021-11-27',
    authenticator = authenticator
)
assistant.set_service_url('{url}') # replace with service instance URL
assistant_id = '{environment_id}' # replace with environment ID

# Start conversation with empty message.
message_response = assistant.message_stateless(
    assistant_id,
).get_result()

# Print responses from actions, if any. Supports only text responses.
if message_response['output']['generic']:
    for assistant_response in message_response['output']['generic']:
        if assistant_response['response_type'] == 'text':
            print(assistant_response['text'])
```
{: codeblock}
{: python}

```java
/*
 * Example 1: Creates service object, sends initial message, and
 * receives response.
 */

import com.ibm.cloud.sdk.core.security.Authenticator;
import com.ibm.cloud.sdk.core.security.IamAuthenticator;
import com.ibm.watson.assistant.v2.Assistant;
import com.ibm.watson.assistant.v2.model.MessageResponseStateless;
import com.ibm.watson.assistant.v2.model.MessageStatelessOptions;
import com.ibm.watson.assistant.v2.model.RuntimeResponseGeneric;
import java.util.List;
import java.util.logging.LogManager;

public class AssistantSimpleExample {
  public static void main(String[] args) {

    // Suppress log messages in stdout.
    LogManager.getLogManager().reset();

    // Create Assistant service object.
    Authenticator authenticator = new IamAuthenticator("{apikey}"); // replace with API key
    Assistant assistant = new Assistant("2020-09-24", authenticator);
    assistant.setServiceUrl("{url}");
    String assistantId = "{assistant_id}"; // replace with assistant ID

    // Start conversation with empty message.
    MessageStatelessOptions messageOptions = new MessageStatelessOptions.Builder(assistantId)
      .build();
    MessageResponseStateless response = assistant.messageStateless(messageOptions)
      .execute()
      .getResult();

    // Print the output from dialog, if any. Assumes a single text response.
      List<RuntimeResponseGeneric> responseGeneric = response.getOutput().getGeneric();
      if(responseGeneric.size() > 0) {
        if(responseGeneric.get(0).responseType().equals("text")) {
          System.out.println(responseGeneric.get(0).text());
        }
      }
  }
}
```
{: codeblock}
{: java}

The first step is to create a the service object, a sort of wrapper for the {{site.data.keyword.conversationshort}} service.

You use the service object for sending input to, and receiving output from, the service. When you create the service object, you specify the API key for authentication, as well as the version of the {{site.data.keyword.conversationshort}} API you are using.

In this Node.js example, the service object is an instance of `AssistantV2`, stored in the variable `assistant`. The Watson SDKs for other languages provide equivalent mechanisms for instantiating a service object.
{: javascript}

In this Python example, the service object is an instance of `watson_developer_cloud.AssistantV2`, stored in the variable `assistant`. The Watson SDKs for other languages provide equivalent mechanisms for instantiating a service object.
{: python}

In this Java example, the service object is an instance of `Assistant`, stored in the variable `assistant`. The Watson SDKs for other languages provide equivalent mechanisms for instantiating a service object.
{: java}

After creating the service object, we use it to send a message to the assistant, using the stateless `message` method. In this example, the message is empty; we just want to trigger the *Greet customer* action to start the conversation, so we don't need any input text. We then print any text responses returned in the `generic` array in the returned output.

Use the `node <filename.js>` command to run the example application.
{: javascript}

Use the `python3 <filename.py>` command to run the example application.
{: python}

Paste the example code into a file named `AssistantSimpleExample.java`. You can then compile and run it.
{: java}

**Note:** Make sure you have installed the Watson SDK for Node.js using `npm install ibm-watson`.
{: javascript}

**Note:** Make sure you have installed the Watson SDK for Python using `pip install --upgrade ibm-watson` or `easy_install --upgrade ibm-watson`.
{: python}

**Note:** Make sure you have installed the [Watson SDK for Java](https://github.com/watson-developer-cloud/java-sdk/blob/master/README.md){: external}.
{: java}

Assuming everything works as expected, the assistant returns the output from the assistant, which the app then prints to the console:

```
Welcome to the Watson Assistant example. What's your name?
```
{: screen}

This output tells us that we have successfully communicated with the assistant and received the greeting message specified by the *Greet customer* action. But we don't yet have a way of responding to the assistant's question.

## Processing user input
{: #api-client-process-input}

To be able to process user input, we need to add a user interface to our client application. For this example, we'll keep things simple and use standard input and output.
<span class="ph style-scope doc-content" data-hd-programlang="javascript">We can use the Node.js prompt-sync module to do this. (You can install prompt-sync using `npm install prompt-sync`.)</span>
<span class="ph style-scope doc-content" data-hd-programlang="python">We can use the Python 3 `input` function to do this.</span>
<span class="ph style-scope doc-content" data-hd-programlang="java">We can use the Java `Console.readLine()` function to do this.</span>

```javascript
// Example 2: Adds user input.

const prompt = require('prompt-sync')();
const AssistantV2 = require('ibm-watson/assistant/v2');
const { IamAuthenticator } = require('ibm-watson/auth');

// Create Assistant service object.
const assistant = new AssistantV2({
  version: '2020-09-24',
  authenticator: new IamAuthenticator({
    apikey: '{apikey}', // replace with API key
  }),
  url: '{urll}', // replace with URL
});

const assistantId = '{assistant_id}'; // replace with assistant ID

// Start conversation with empty message
messageInput = {
  messageType: 'text',
  text: '',
};
sendMessage(messageInput);

// Send message to assistant.
function sendMessage(messageInput) {
  assistant
    .messageStateless({
      assistantId,
      input: messageInput,
    })
    .then(res => {
      processResponse(res.result);
    })
    .catch(err => {
      console.log(err); // something went wrong
    });
}

// Process the response.
function processResponse(response) {

  // If an intent was detected, log it out to the console.
  if (response.output.intents.length > 0) {
    console.log('Detected intent: #' + response.output.intents[0].intent);
  }

  // Display the output from assistant, if any. Supports only a single
  // text response.
  if (response.output.generic) {
    if (response.output.generic.length > 0) {
      if (response.output.generic[0].response_type === 'text') {
        console.log(response.output.generic[0].text);
      }
    }
  }

  // If we're not done, prompt for the next round of input.
  const newMessageFromUser = prompt('>> ');
  if (newMessageFromUser !== 'quit') {
    newMessageInput = {
      messageType: 'text',
      text: newMessageFromUser,
    }
    sendMessage(newMessageInput);
  }
}
```
{: codeblock}
{: javascript}

```python
# Example 2: Adds user input.

from ibm_watson import AssistantV2
from ibm_cloud_sdk_core.authenticators import IAMAuthenticator

# Create Assistant service object.
authenticator = IAMAuthenticator('{apikey}') # replace with API key
assistant = AssistantV2(
    version = '2021-11-27',
    authenticator = authenticator
)
assistant.set_service_url('{url}') # replace with service instance URL
assistant_id = '{environment_id}' # replace with environment ID

# Initialize with empty value to start the conversation.
message_input = {
    'message_type:': 'text',
    'text': ''
    }

# Main input/output loop
while message_input['text'] != 'quit':

    # Send message to assistant.
    message_response = assistant.message_stateless(
        assistant_id,
        input = message_input
    ).get_result()

    # If an intent was detected, print it to the console.
    if message_response['output']['intents']:
        print('Detected intent: #' + message_response['output']['intents'][0]['intent'])

    # Print responses from actions, if any. Supports only text responses.
    if message_response['output']['generic']:
        for assistant_response in message_response['output']['generic']:
            if assistant_response['response_type'] == 'text':
                print(assistant_response['text'])

    # Prompt for next round of input.
    user_input = input('>> ')
    message_input = {
        'text': user_input
    }
```
{: codeblock }
{: python }

```java
/*
 * Example 2: Adds user input and detects intents.
 */

import com.ibm.cloud.sdk.core.security.Authenticator;
import com.ibm.cloud.sdk.core.security.IamAuthenticator;
import com.ibm.watson.assistant.v2.Assistant;
import com.ibm.watson.assistant.v2.model.MessageInputStateless;
import com.ibm.watson.assistant.v2.model.MessageResponseStateless;
import com.ibm.watson.assistant.v2.model.MessageStatelessOptions;
import com.ibm.watson.assistant.v2.model.RuntimeIntent;
import com.ibm.watson.assistant.v2.model.RuntimeResponseGeneric;
import java.util.List;
import java.util.logging.LogManager;

public class AssistantSimpleExample {
  public static void main(String[] args) {

    // Suppress log messages in stdout.
    LogManager.getLogManager().reset();

    // Create Assistant service object.
    Authenticator authenticator = new IamAuthenticator("{apikey}"); // replace with API key
    Assistant assistant = new Assistant("2020-09-24", authenticator);
    assistant.setServiceUrl("{url}");
    String assistantId = "{assistant_id}"; // replace with assistant ID

    // Initialize with empty message to start the conversation.
    MessageInputStateless input = new MessageInputStateless.Builder()
      .messageType("text")
      .text("")
      .build();

    // Main input/output loop
    do {
      // Send message to assistant.
      MessageStatelessOptions messageOptions = new MessageStatelessOptions.Builder(assistantId)
        .input(input)
        .build();
      MessageResponseStateless response = assistant.messageStateless(messageOptions)
        .execute()
        .getResult();

      // Print the output from dialog, if any. Assumes a single text response.
      List<RuntimeResponseGeneric> responseGeneric = response.getOutput().getGeneric();
      if(responseGeneric.size() > 0) {
        if(responseGeneric.get(0).responseType().equals("text")) {
          System.out.println(responseGeneric.get(0).text());
        }
      }

      // Prompt for next round of input.
      System.out.print(">> ");
      String inputText = System.console().readLine();
      input = new MessageInputStateless.Builder()
        .messageType("text")
        .text(inputText)
        .build();
    } while(!input.text().equals("quit"));
  }
}
```
{: codeblock }
{: java }

This version of the application begins the same way as before: sending an empty message to the assistant to start the conversation.

The `processResponse()` function now displays any intent detected by the dialog skill, along with the output text. It then prompts for the next round of user input.
{: javascript }

It then displays the text of any responses received from the assistant, and it prompts for the next round of user input.
{: python }

It then displays any intent detected by the dialog along with the output text, and then it prompts for the next round of user input.
{: java}

Because we need a way to end the conversation, the client app is also watching for the literal command `quit` to indicate that the program should exit.

But something still isn't right:

```
Welcome to the Watson Assistant example. What's your name?
>> Robert
I'm afraid I don't understand. Please rephrase your question.
>> I want to make an appointment.
What day would you like to come in?
>> Thursday
I'm afraid I don't understand. Please rephrase your question.
>>
```
{: screen}

The assistant is starting out with the correct greeting, but it doesn't understand when you tell it your name. And if you tell it you want to make an appointment, the correct action is triggered; but once again, it doesn't understand when you answer the follow-up question.

This is happening because we are using the stateless `message` method, which means that it is the responsibility of our client application to maintain state information for the conversation. Because we are not yet doing anything to maintain state, the assistant sees every round of user input as the first turn of a new conversation. Because it has no memory of asking a question, it tries to interpret your answer as a new question or request.

## Maintaining state

State information for your conversation is maintained using the *context*. The context is an object that is passed back and forth between your application and the assistant, storing information that can be preserved and updated as the conversation goes on. Because we are using the stateless `message` method, the assistant does not store the context, so it is the responsibility of our client application to maintain it from one turn of the conversation to the next.

The context includes a session ID for each conversation, as well as a counter that is incremented with each turn of the conversation. The assistant updates the context and returns it with each response. But our previous version of the example did not preserve the context, so these updates were lost, and each round of input appeared to be the start of a new conversation. We can fix that by saving the context and sending it back to the assistant each time.

In addition to maintaining our place in the conversation, the context can also contain action variables that store any other data you want to pass back and forth between your application and the assistant. This can include persistent data you want to maintain throughout the conversation (such as a customer's name or account number), or any other data you want to track (such as the contents of a shopping cart or user preferences).

```javascript
// Example 3: Preserves context to maintain state.

const prompt = require('prompt-sync')();
const AssistantV2 = require('ibm-watson/assistant/v2');
const { IamAuthenticator } = require('ibm-watson/auth');

// Create Assistant service object.
const assistant = new AssistantV2({
  version: '2020-09-24',
  authenticator: new IamAuthenticator({
    apikey: '{apikey}', // replace with API key
  }),
  url: '{url}', // replace with URL
});

const assistantId = '{assistant_id}'; // replace with assistant ID

// Start conversation with empty message
messageInput = {
  messageType: 'text',
  text: '',
};
context = {};
sendMessage(messageInput, context);

// Send message to assistant.
function sendMessage(messageInput, context) {
  assistant
    .messageStateless({
      assistantId,
      input: messageInput,
      context: context,
    })
    .then(res => {
      processResponse(res.result);
    })
    .catch(err => {
      console.log(err); // something went wrong
    });
}

// Process the response.
function processResponse(response) {

  let context = response.context;

  // If an intent was detected, log it out to the console.
  if (response.output.intents.length > 0) {
    console.log('Detected intent: #' + response.output.intents[0].intent);
  }

  // Display the output from assistant, if any. Supports only a single
  // text response.
  if (response.output.generic) {
    if (response.output.generic.length > 0) {
      if (response.output.generic[0].response_type === 'text') {
        console.log(response.output.generic[0].text);
      }
    }
  }

  // If we're not done, prompt for the next round of input.
  const newMessageFromUser = prompt('>> ');
  if (newMessageFromUser !== 'quit') {
    newMessageInput = {
      messageType: 'text',
      text: newMessageFromUser,
    }
    sendMessage(newMessageInput, context);
  }
}
```
{: codeblock}
{: javascript }

```python
# Example 3: Preserves context to maintains state.

from ibm_watson import AssistantV2
from ibm_cloud_sdk_core.authenticators import IAMAuthenticator

# Create Assistant service object.
authenticator = IAMAuthenticator('{apikey}') # replace with API key
assistant = AssistantV2(
    version = '2021-11-27',
    authenticator = authenticator
)
assistant.set_service_url('{url}') # replace with service instance URL
assistant_id = '{environment_id}' # replace with environment ID

# Initialize with empty message to start the conversation.
message_input = {
    'message_type:': 'text',
    'text': ''
    }
context = {}

# Initialize with empty message to start the conversation.
message_input = {
    'message_type:': 'text',
    'text': ''
    }
context = {}

# Main input/output loop
while message_input['text'] != 'quit':

    # Send message to assistant.
    message_response = assistant.message_stateless(
        assistant_id,
        input = message_input,
        context = context
    ).get_result()

    context = message_response['context']

    # Print responses from actions, if any. Supports only text responses.
    if message_response['output']['generic']:
        for assistant_response in message_response['output']['generic']:
            if assistant_response['response_type'] == 'text':
                print(assistant_response['text'])

    # Prompt for next round of input.
    user_input = input('>> ')
    message_input = {
        'text': user_input
    }
```
{: codeblock }
{: python }

```java
/*
 * Example 3: Preserves context to maintain state.
 */

import com.ibm.cloud.sdk.core.security.Authenticator;
import com.ibm.cloud.sdk.core.security.IamAuthenticator;
import com.ibm.watson.assistant.v2.Assistant;
import com.ibm.watson.assistant.v2.model.MessageContextStateless;
import com.ibm.watson.assistant.v2.model.MessageInputStateless;
import com.ibm.watson.assistant.v2.model.MessageResponseStateless;
import com.ibm.watson.assistant.v2.model.MessageStatelessOptions;
import com.ibm.watson.assistant.v2.model.RuntimeIntent;
import com.ibm.watson.assistant.v2.model.RuntimeResponseGeneric;
import java.util.List;
import java.util.logging.LogManager;

public class AssistantSimpleExample {
  public static void main(String[] args) {

    // Suppress log messages in stdout.
    LogManager.getLogManager().reset();

    // Create Assistant service object.
    Authenticator authenticator = new IamAuthenticator("{apikey}"); // replace with API key
    Assistant assistant = new Assistant("2020-09-24", authenticator);
    assistant.setServiceUrl("{url}");
    String assistantId = "{assistant_id}"; // replace with assistant ID

    // Initialize with empty message to start the conversation.
    MessageInputStateless input = new MessageInputStateless.Builder()
      .messageType("text")
      .text("")
      .build();
    MessageContextStateless context = new MessageContextStateless.Builder()
      .build();

    // Main input/output loop
    do {
      // Send message to assistant.
      MessageStatelessOptions messageOptions = new MessageStatelessOptions.Builder(assistantId)
        .input(input)
        .context(context)
        .build();
      MessageResponseStateless response = assistant.messageStateless(messageOptions)
        .execute()
        .getResult();

      context = response.getContext();

      // If an intent was detected, print it to the console.
      List<RuntimeIntent> responseIntents = response.getOutput().getIntents();
      if(responseIntents.size() > 0) {
        System.out.println("Detected intent: #" + responseIntents.get(0).intent());
      }

      // Print the output from dialog, if any. Assumes a single text response.
      List<RuntimeResponseGeneric> responseGeneric = response.getOutput().getGeneric();
      if(responseGeneric.size() > 0) {
        if(responseGeneric.get(0).responseType().equals("text")) {
          System.out.println(responseGeneric.get(0).text());
        }
      }

      // Prompt for next round of input.
      System.out.print(">> ");
      String inputText = System.console().readLine();
      input = new MessageInputStateless.Builder()
        .messageType("text")
        .text(inputText)
        .build();
    } while(!input.text().equals("quit"));
  }
}
```
{: codeblock }
{: java }

The only change from the previous example is that we are now storing the context received from the assistant in a variable called `context`, and we're sending it back with the next round of user input:
{: javascript }

The only change from the previous example is that we are now storing the context received from the assistant in a variable called `context`, and we're sending it back with the next round of user input:
{: python }

The only change from the previous example is that we are now storing the context received from the assistant in a variable called `context`, and we're including it as part of the message options along with the next round of user input:
{: java}

```javascript
  assistant
    .messageStateless({
      assistantId,
      input: messageInput,
      context: context,
    })
```
{: codeblock}
{: javascript }

```python
response = assistant.message_stateless(
    assistant_id,
    input = message_input,
    context = context
).get_result()
```
{: codeblock }
{: python }

```java
MessageStatelessOptions messageOptions = new MessageStatelessOptions.Builder(assistantId)
  .input(input)
  .context(context)
  .build();
```
{: codeblock }
{: java }

This ensures that the context is maintained from one turn to the next, so the {{site.data.keyword.conversationshort}} service no longer thinks every turn is the first:

```
Welcome to the Watson Assistant example. What's your name?
>> Robert
Hi, Robert! How can I help you?
>> I want to make an appointment.
What day would you like to come in?
>> Next Monday
What time works for you?
>> 10 AM
OK, Robert. You have an appointment for 10:00 AM on Sep 12. See you then!
```
{: screen}

Success! The application now uses the {{site.data.keyword.conversationshort}} service to understand natural-language input, and it displays the appropriate responses.

This simple example illustrates how you can build a custom client app to communicate with the assistant. Of course, a real-world application would use a more sophisticated user interface, and it might integrate with other applications such as a customer database or other business systems. It would also need to send additional data to the assistant, such as a user ID to identify each unique user. But the basic principles of how the application interacts with the {{site.data.keyword.conversationshort}} service would remain the same.

## Using the v1 runtime API
{: #api-client-v1-api}

Using the v2 API is the recommended way to build a runtime client application that communicates with the {{site.data.keyword.conversationshort}} service. However, some older applications might still be using the v1 runtime API, which includes a similar method for sending messages to the workspace within a dialog skill. Note that if your app uses the v1 runtime API, it communicates directly with the workspace, bypassing the skill orchestration and state-management capabilities of the assistant.

For more information about the v1 `/message` method and context, see the [v1 API Reference](https://{DomainName}/apidocs/assistant/assistant-v1#message){: external}.
