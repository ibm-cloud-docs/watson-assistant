---

copyright:
  years: 2020, 2022
lastupdated: "2022-12-12"

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
{:tag-ibm-cloud: .tag data-tag-color="blue"}
{:tag-cp4d: .tag data-tag-color="magenta"}

{{site.data.content.classiclink}}

# Phone integration configuration
{: #deploy-phone-config}

[IBM Cloud]{: tag-ibm-cloud}

After you have set up the phone integration for your assistant, you can modify the phone integration settings to customize the call behavior.
{: shortdesc}

## Handling call and transfer failures
{: #deploy-phone-config-failure}

You can configure the phone integration to transfer the caller to a human agent if the phone connection fails for any reason. To transfer the caller to a human agent automatically, go to the **Advanced** tab in the phone integration settings, and make the following configuration selections:

- **SIP target when a call fails**: Add the SIP endpoint for your support agent service. Specify a SIP or telephone URI for a general call queue that can redirect requests to other queues. For more information, see [Configuring backup call center support](#deploy-phone-config-transfer-service).

- **Call failure message**: Add the message you want the assistant to say to a caller before it transfers the call to a human agent.

If, after you transfer the call to a human, the connection to a live agent fails for any reason, you can configure what to do.

- **Transfer failure message**: Add the message you want the assistant to say to a caller if transfer to a live agent fails. The message can be up to 150 characters in length.

- **Disconnect call on transfer failure**: Choose whether to disconnect the call after the failure message. This option is enabled by default. If this option is disabled, when a call transfer fails, your assistant can disconnect or process a different action.

  If you choose to leave a call connected despite a transfer failure, Watson Assistant will initiate a new turn to determine the next step. It's important that the Assistant be configured with an Action or webhook that can handle this scenario.

The phone integration supports disaster recovery by providing the ability to do a fast failover to another region instead of routing the call to a live agent when a service outage occurs. This is accomplished by sending a SIP 503 response to the upstream SIP trunking provider, instead of auto referring the call to a live agent when failures happen during the setup of a call. This 503 response can then be used by the SIP trunking provider to reroute the call to another region. If you want to take advantage of this capability, open a service ticket against the {{site.data.keyword.conversationshort}} service instance that requires disaster recovery.
{: note}

## Secure the phone connection
{: #deploy-phone-config-security}

You can add security to the phone connection by going to the **Advanced options** tab in the phone integration settings, and selecting one or both of the following options:

- **Force secure trunking**: Select this option to use Secure Real-Time Transfer Protocol (SRTP) to secure the audio that is transmitted over the phone. For more information about RTP, see [Call routing details](#deploy-phone-config-route).

- **Enable SIP authentication**: Select this option if you want to require SIP digest authentication. 

    When SIP authentication is required, all inbound traffic (meaning requests from the SIP provider to your assistant) is authenticated using SIP digest authentication, and must be sent using Transport Layer Security (TLS). If this option is selected, the SIP digest user name and password must be configured, and the SIP trunk being used to connect to Assistant must be configured to use only TLS.

    If you use Twilio as your SIP trunk provider, you cannot enable SIP authentication for outbound SIP trunks to Watson Assistant.
    {: important}

## Applying advanced SIP trunk configuration settings
{: #deploy-phone-config-sip-trunk}

To configure how your assistant interacts with a SIP trunk from an external provider, go to the **SIP trunk** tab in the phone integration settings, and update the following options in the **SIP trunking integration** section:

- **SIP INVITE headers to extract**: List the headers that you want your assistant to use.

    The SIP INVITE request can include metadata about the call in headers that can be extracted and sent to your assistant using context variables. For example, many companies use Interactive Voice Response (IVR) systems that pass information about an incoming call by using SIP headers. If you want to make use of any of these headers, list the header names here.
  
    The specified headers, if present in the request, are stored in the context variable `sip_custom_invite_headers`, along with other related metadata that is automatically extracted from the SIP INVITE. This variable is an array in which each key/value pair represents a header from the request, as in this example:

    ```json
    {
      "input": {
        "text": "",
          ...
      },
      "context" : {
        "global" : {...},
        "skills" : {...},
        "integrations" : {
          "voice_telephony": {
            "private":{
              "user_phone_number":"+18594213456",
            },  
            "sip_call_id": "Aob2-2743-5678-1234",
            "assistant_phone_number":"+18882346789",
            "sip_custom_invite_headers": {
              "X-customer-name": "my_name",
              "X-account-number": "12345"
            }
          }
        }
      }
    }
    ```

    You can then reference these headers in your assistant. For example, you might check the header value in a step condition to determine the next step. You can also use these headers when searching the assistant logs; for example, you might search for a custom header to find all the messages associated with particular account.

- **Disable the ring that callers will hear while the assistant is contacted**: Choose whether you want the caller to hear a signal that indicates that the assistant is being contacted. 

    A `180 Ringing` response is sent from the assistant back to the SIP trunk provider while your assistant processes the incoming call invitation. The ringing response is sent by default.

- **Don't place callers on hold while transferring to a live agent**: Choose whether the phone integration puts the caller on hold. 

    If your SIP trunk provider manages holds, disable this feature. For example, some SIP trunk providers prefer to have the assistant send a SIP REFER request, so they can put the call on hold themselves.

For more information about the SIP protocol, see [RFC 3261](https://tools.ietf.org/html/rfc3261){: external} and about the RTP protocol, see [RFC 3550](https://tools.ietf.org/html/rfc3550){: external}.

## Configuring backup call center support
{: #deploy-phone-config-transfer-service}

When you use the phone integration as the first line of assistance for customers, it's a good idea to have a live agent backup available. You can design your assistant to transfer a call to a human in case the phone connection fails, or if a user asks to speak to someone.

Your company might already have one or more phone numbers that connect to an automatic call dispatcher (ACD) that can queue callers until an appropriate agent is available. If not, choose a call center service to use as your backup.

A conversation cannot be transferred from one integration type to another. For example, if you use the web chat integration with service desk support, you cannot transfer a phone call to the service desk that is set up for the web chat.

You must provide the call center SIP URI for the call center service you use. You must specify this information in your assistant when you enable a call transfer from a dialog node or action step. For more information, see [Transferring a call to a live agent](/docs/watson-assistant?topic=watson-assistant-phone-actions#phone-actions-transfer).

## Optimize your actions for phone interaction
{: #deploy-phone-config-actions}

For the best customer experience, design your dialog with the capabilities of the phone integration in mind:

- Do not include HTML elements in your action responses. To add formatting, use Markdown. For more information, see [Formatting responses](/docs/watson-assistant?topic=watson-assistant-respond#respond-formatting).

- You can use a search extension to include search results in actions that the phone integration will read. When search results are returned, the phone integration reads the introductory message (for example, `I found this information that might be helpful`), and then the body of only the first search result.

    The entire search response (meaning the introductory message plus the body of the first search result) must be less than 5,000 characters long or the response will not be read at all. Be sure to test the search results that are returned and curate the data collection that you use as necessary.

For more information about using the search integration, see [Leveraging existing help content](/docs/watson-assistant?topic=watson-assistant-search-add).

For more information about how to implement common actions from your dialog, see [Handling phone interactions](/docs/watson-assistant?topic=watson-assistant-phone-actions).



## Setting up a SIP trunk
{: #deploy-phone-config-sip-providers}

If you do not use the option to generate a free phone number, you are responsible for setting up the SIP trunk that will be used by the phone integration. Find a provider and create a SIP trunk account. Your account will be charged for the phone integration's use of the SIP trunk.

You can set up a SIP trunk in the following ways:

- [Creating a Twilio SIP trunk](#deploy-phone-config-twilio-setup)
- [Use other third-party providers](#deploy-phone-config-request-setup)
- [Bring your own SIP trunk](#deploy-phone-config-byost)
- [Migrate from Voice Agent with Watson](#deploy-phone-config-migrate-from-va)

### Creating a Twilio SIP trunk
{: #deploy-phone-config-twilio-setup}

To set up a Twilio SIP trunk, complete the following steps: 

1.  Create a Twilio account on the [Twilio website](https://www.twilio.com/sip-trunking){: external}.

1.  From the Twilio website, go to the *Elastic SIP Trunking* dashboard. If you do not see it on the sidebar, go to the Search Bar at the top and search for 'Elastic SIP Trunking', then select **Elastic SIP Trunks**.


1.  On the **Elastic SIP Trunks** page, click the *Create new SIP Trunk* button to create a SIP trunk. Enter a name for your SIP trunk and click *Create*. If you already have a SIP trunk, go to the next step.

1.  From the Elastic SIP Trunks page, select your SIP trunk.

1.  Select *Origination* from the navigation bar for your SIP trunk and configure the origination SIP URI.

    You can get the SIP URI for your phone integration from the phone integration configuration page.

1.  If you plan to support call transfers, enable Call Transfer (SIP REFER) in your SIP trunk. If you expect to transfer calls to the public switched telephone network (PSTN), also enable PSTN Transfer on your trunk.

1.  Select *Numbers* from the navigation bar for your SIP trunk, and then do one of the following things:
  
    - Click *Add a number* and then *Buy a Number*.
    - If you already have a number, you can click *Add a number* and then *Add an Existing Number*.
  
If you use a Lite or Trial Twilio account for testing purposes, then be sure to verify the transfer target. For more information, see the [Twilio documentation](https://support.twilio.com/hc/en-us/articles/223136107-How-does-Twilio-s-Free-Trial-work-){: external}.

You cannot enable SIP authentication if you choose Twilio as your SIP trunk provider. Twilio doesn't support SIPS for originating calls.

### Using other third-party providers
{: #deploy-phone-config-request-setup}

You can ask for help setting up an account with another SIP trunk provider by opening a support request.

IBM has established relationships with the following SIP trunk providers:

- [Five9](https://www.five9.com/products/capabilities/contact-center-software){: external}
- [Genesys](https://www.genesys.com/en-sg/definitions/what-is-a-trunk){: external}
- [Vonage](https://www.vonage.com/communications-apis/sip-trunking/){: external}
- [Voximplant](https://voximplant.com/){: external}

The SIP trunk provider sets up a SIP trunk for your voice traffic, and manages access from allowed IP addresses. Most of the major SIP trunk providers have existing relationships with IBM. Therefore, the network configuration that is required to support the SIP trunk connection typically can be handled for you with minimal effort.

1. Create a [{{site.data.keyword.Bluemix_notm}} case](https://cloud.ibm.com/unifiedsupport/cases/form){: external}.

1. Click **Customer success** as the case type.

1. For **Subject**, enter `SIP trunk provider setup for Watson Assistant`.

1. Include the following information in the description:

   - Company Name
   - Your {{site.data.keyword.Bluemix_notm}} account ID
   - Your {{site.data.keyword.conversationshort}} service name
   - Network diagram with IP address or SIP trunk provider information

### Bring your own SIP trunk
{: #deploy-phone-config-byost}

If you choose to use a SIP trunk carrier that IBM does not have an established relationship with, you can do so.

The following table lists the fully qualified domain names and IP addresses that are used for SIP connections.

| Location  | Domain names | IP addresses |
|-----------|--------------|--------------|
| Dallas    | public.0001.voip.us-south.assistant.watson.cloud.ibm.com  \npublic.0002.voip.us-south.assistant.watson.cloud.ibm.com  \npublic.0003.voip.us-south.assistant.watson.cloud.ibm.com | 67.228.108.82  \n169.63.5.162  \n150.239.30.146 |
| Frankfurt | public.0001.voip.eu-de.assistant.watson.cloud.ibm.com  \npublic.0002.voip.eu-de.assistant.watson.cloud.ibm.com  \npublic.0003.voip.eu-de.assistant.watson.cloud.ibm.com  | 161.156.178.162  \n169.50.56.146  \n149.81.86.82 |
| London    | public.0001.voip.eu-gb.assistant.watson.cloud.ibm.com  \npublic.0002.voip.eu-gb.assistant.watson.cloud.ibm.com  \npublic.0003.voip.eu-gb.assistant.watson.cloud.ibm.com  | 158.176.120.162  \n141.125.102.34  \n158.175.99.34 |
| Seoul     | public.0001.voip.kr-seo.assistant.watson.cloud.ibm.com | |
| Sydney | public.0001.voip.au-syd.assistant.watson.cloud.ibm.com  \npublic.0002.voip.au-syd.assistant.watson.cloud.ibm.com  \npublic.0003.voip.au-syd.assistant.watson.cloud.ibm.com | 168.1.47.2  \n135.90.86.50  \n168.1.106.130 |
| Tokyo | public.0001.voip.jp-tok.assistant.watson.cloud.ibm.com  \npublic.0002.voip.jp-tok.assistant.watson.cloud.ibm.com  \npublic.0003.voip.jp-tok.assistant.watson.cloud.ibm.com | 165.192.69.82  \n128.168.105.178  \n161.202.149.162 |
| Washington, DC | public.0001.voip.us-east.assistant.watson.cloud.ibm.com  \npublic.0002.voip.us-east.assistant.watson.cloud.ibm.com  \npublic.0003.voip.us-east.assistant.watson.cloud.ibm.com | 52.116.100.158  \n169.61.70.162  \n169.59.136.194 |
{: caption="SIP network information" caption-side="top"}

### Migrating from Voice Agent with Watson
{: #deploy-phone-config-migrate-from-va}

If you created an {{site.data.keyword.iva_full}} service instance in IBM Cloud to enable customers to connect to an assistant over the phone, consider using the phone integration instead. You can use the same SIP account and phone number that you configured for use with {{site.data.keyword.iva_short}} in the phone integration.

The phone integration provides a more seamless integration with your assistant. However, the integration currently does not support the following functions:

- Outbound calling
- Configuring backup locations
- Event forwarding to save call detail reports in the IBM Cloudant for IBM Cloud database service 
- Reviewing the usage summary page. Use IBM Log Analysis instead. For more information, see [Viewing logs](/docs/watson-assistant?topic=watson-assistant-phone-troubleshooting#phone-troubleshooting-logs).

To migrate from {{site.data.keyword.iva_short}} to the {{site.data.keyword.conversationshort}} phone integration, complete the following steps:

1.  From the {{site.data.keyword.iva_short}} page, copy the phone number or numbers that you used for your SIP account.
1.  When you set up the {{site.data.keyword.conversationshort}} phone integration, add the phone number or set of numbers that you copied in the previous step.
1.  From the phone integration setup page, copy the SIP uniform resource identifier (URI). 
1.  In your SIP trunk account, replace the {{site.data.keyword.iva_short}} URI that you specified previously with the URI that you copied from the phone integration setup page in the previous step. 

    For example, if you use a Twilio SIP trunk, you would add the assistant's SIP uniform resource identifier (URI) to the Twilio **Origination SIP URI** field.

1. If your SIP trunk provider is not already allowlisted with the {{site.data.keyword.conversationshort}} region you are migrating to, follow these [instructions](#deploy-phone-config-request-setup) to get access to your SIP trunk.

### Call routing details
{: #deploy-phone-config-route}

Incoming calls to your assistant follow this path: 

1.  A customer calls the customer support phone number that is managed by your Session Initiation Protocol (SIP) trunk provider.
1.  The SIP trunk service sends a SIP `INVITE` HTTP request to your assistant's phone integration to establish a connection. 
1.  The phone integration connects to the speech services that are required to support the interaction.
1.  After the services are ready, the connection is established, and audio is sent over the Real-time Transport Protocol (RTP). 

    RTP is a network protocol for delivering audio and video over IP networks.
1.  The greeting action of the assistant is processed. The response text is sent to the {{site.data.keyword.texttospeechshort}} service to be converted to audio and the audio is sent to the caller.
1.  When the customer says something, the audio is converted to text by the {{site.data.keyword.speechtotextshort}} service and is sent to your assistant for evaluation.
1.  The assistant processes the input and calculates the best response. The response text from the assistant is sent to the {{site.data.keyword.texttospeechshort}} service to be converted to audio and the audio is sent back to the caller over the existing connection.
1.  If the caller asks to speak to a person, the assistant can transfer the person to a call center. A SIP `REFER` request is sent to the SIP trunk provider so it can transfer the call to the call center SIP URI that is specified in the dialog node where the transfer action is configured.
1.  When one of the participants of the call hangs up, a SIP `BYE` HTTP request is sent to the other participant.
