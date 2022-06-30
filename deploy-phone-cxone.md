

# Integrating with phone and NICE CXone call center
{: #deploy-phone-nicecxone}

You can use the phone integration to help your customers over the phone and transfer them to live agents in the NICE CXone call center. If in the course of a conversation with your assistant, a customer asks to speak to a person, you can transfer the conversation directly to a NICE CXone live agent.

## Before you begin

To use this integration pattern, make sure you have the following:

- {{site.data.keyword.conversationshort}} Plus or Enterprise Plan (required for phone integration)
- A working assistant you are ready to deploy
- A NICE CXone account and phone numbers were allocated for this integration. 

## Integrating with NICE CXone

First, you need to generate access keys. Access keys consist of two parts: an access key ID and a Secret Access Key. Access keys can be used for authentication in the back-end integration of Watson Assistant to  CXone. 

1. Log into the NICE CXone console.
2. Click the app selector  ![](https://help.nice-incontact.com/content/resources/images/icons/appselectoricon.png)  and select  **Admin**.
3. Click  **Users** and then locate and click the user account you want to use for the integration.
5. Click the  **Access Keys** tab.
6. Click  **Generate New Access Key**.
7. If required, click  **Show Secret Key** and copy the secret key to a secure location.
8. Click  **Save**. Once you click **Save**, you cannot retrieve the secret key again. You will need to generate a new access key if the secret key is lost.

To integrate your assistant with NICE CXone, follow these steps:

 1. In the Watson Assistant user interface, create a new phone integration. Specify the following information:

    - When prompted, select **Use an existing phone number with an external provider**.

    - Specify the phone number you allocated for the NICE CXone integration.
    - On the **Select contact center** tab, select NICE CXone.
    - Click **Next**.
    - On the **Connect to contact center** tab:
	    - Enter the NICE CXone authentication endpoint in the **Authentication URL** field.  
	    - Enter the NICE CXone *Admin* API endpoint in the **API URL** field.  
	    - Enter the SIP header field name that contains the Contact ID in the **Contact ID** field. Optional. The default value is **X-ContactID**.
	    - Enter the access key ID from the previous step in the **Access Key ID** field. 
	    - Enter the access key secret you generated in the previous step in the **Access Key Secret** field. 
    - Complete the phone integration setup process. (For more information, see [Integrating with phone](/docs/watson-assistant?topic=watson-assistant-deploy-phone).)

### Configuring the NICE CXone script

NICE CXone provides a scripting tool that allows workflow developers to define routing flows for their contact centers in CXone.
Ensure that you have the following actions and settings in the workflow for integration to work properly. 

#### Connecting a caller to a Watson Assistant bot

-  Use a [Placecall](https://help.nice-incontact.com/content/studio/actions/placecall/placecall.htm) action to initiate an outbound call to Watson Assistant. In the **PhoneNumber** property enter the phone number you allocated for this integration. 

The phone number must match the number you configured in **Use an existing phone number with an external provider** in the Watson Assistant user interface.
{: note}

-  [Sipputheader](https://help.nice-incontact.com/content/studio/actions/sipputheader/sipputheader.htm) action. In the **headerName** property enter the name of the SIP header field that will contain the Contact ID. This header field will be included in outgoing SIP INVITE messages to Watson Assistant.  

	**headerName** X-Contact-ID
	**headerValue** {ContactId}


The value in **headerName** must match the name you configured in the **Contact ID** field in the Watson Assistant user interface.
{: note}

**Sipputheader** must be executed before **Placecall**.
{: note}

![Image of the outbound call flow](images/cxone-placecall.png)

#### Transferring a caller to a live agent

You can configure your Watson Assistant bot to transfer a caller to a NICE CXone live agent. 
 
- For transferring a call to a live agent, the phone integration uses the [signal](https://developer.niceincontact.com/API/AdminAPI#/Contacts/Signal%20a%20Contact) REST API. The **p1** attribute is preserved for the session history key. The key can be used for fetching the Watson Assistant conversation history and presenting it to a live agent.  Use [Onsignal](https://help.nice-incontact.com/content/studio/actions/onsignal/onsignal.htm)  to process the signal event. Save the value of the **p1** attribute:

```
sessionKey = "{p1}"
```

For example, you can use the [Snippet](https://help.nice-incontact.com/content/studio/actions/snippet/snippet.htm) action:

```
ASSIGN sessionKey = "{p1}"
```

Use [Reqagent](https://help.nice-incontact.com/content/studio/actions/reqagent/reqagent.htm) to transfer a call to a live agent.


![Image of call transfer to a live agent](images/cxone-live-agent.png)

#### Presenting Watson Assistant conversation history to a live agent

You can configure your script to present a transcript of the end user's conversation with Watson Assistant to a live agent. When an agent answers a call, a pop out window can be presented with the conversation history. This will help the agent to better understand the customer's needs.


- Add an [Onanswer](https://help.nice-incontact.com/content/studio/actions/onanswer/onanswer.htm) event to your script. The  **Onanswer** event is triggered when an agent answers the call, 

- Use [Assign](https://help.nice-incontact.com/content/studio/actions/assign/assign.htm) to store the link to the conversation history into a variable. 
**Variable** watson_url
**Value** https://web-chat.global.assistant.watson.appdomain.cloud/loadAgentAppFrame.html?session_history_key={sessionKey}

- Use the [PopURL](https://help.nice-incontact.com/content/studio/actions/popurl/popurl.htm) action to display the conversation transcript to a live agent. 
**URL** {watson_url}

In this example, when the call is answered by a live agent, the **Onanswer** event is triggered and a pop out window with the Watson Assistant conversation transcript is displayed to an agent.

![Image of the conversation history window](images/cxone-pop-url.png)

#### Disconnecting a call

- The phone integration uses the same [signal](https://developer.niceincontact.com/API/AdminAPI#/Contacts/Signal%20a%20Contact) REST API for disconnecting a call.  In this case, the **p1** attribute is set to `hangup`. You need to design your script so it can distinguish between transferring a call to a live agent and disconnecting a call. If **p1** is set to `hangup` when an **Onsignal** event is triggered, use [Hangup](https://help.nice-incontact.com/content/studio/actions/hangup/hangup.htm) to terminate a script. 

![Image of call hangup](images/cxone-hangup.png)

#### Transferring a caller to a live agent when an error occurs

-  If an error occurs during a call, the phone integration disconnects a call by sending a `SIP BYE` request. In this case, a call should be transferred to a live agent. Use [Onrelease](https://help.nice-incontact.com/content/studio/actions/onrelease/onrelease.htm) to process the BYE request and transfer a call to a live agent.  

In this example, when **Onrelease** is triggered, the script verifies whether the call was already transferred. If no, it calls the **Signal** action and sets an indication that the call is being transferred to a live agent. The indication is set using the **Assign** action. 
**Variable** transferred
 **Value** true

![Image of call disconnect on failure](images/cxone-disconnect-on-failure.png)

**Note** If the  **Hangup** action is executed and an  [**Onrelease**](https://help.nice-incontact.com/content/studio/actions/onrelease/onrelease.htm)  event action is present,  CXone will hang up on the caller and the script will jump to the  **OnRelease** action. Design your script so it can distinguish whether the **OnRelease** event is triggered due to a transfer or hangup. 
{: note}



## Adding transfer support to your Watson Assistant 


Make sure your assistant is configured to transfer calls to an agent using the *Connect To Agent* response_type. For more information about how to do this, see [Transferring a call to a human agent](/docs/watson-assistant?topic=watson-assistant-phone-actions#phone-actions-transfer).

Use the following format:

```json
{
  "output": {
    "generic": [
      {
        "response_type": "connect_to_agent",
        "transfer_info": {
          "target": {
            "nice_cxone": {
              "custom_data": {
                "p2": "test"
              }
            }
          }
        },
        "agent_available": {
          "message": "Ok, I'm transferring you to an agent."
        },
        "agent_unavailable": {
          "message": "Agent is unavailable."
        }
      }
    ]
  }
}
```

**Note** parameters listed in the `custom_data` are transferred to the [signal](https://developer.niceincontact.com/API/AdminAPI#/Contacts/Signal%20a%20Contact) REST API. Supported parameters are `p2`, `p3`, ... `p9`.  `p1` is preserved and used by the phone integration for passing the session history key into the NICE CXone script. 
{: note}
