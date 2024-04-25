---

copyright:
  years: 2020, 2024
lastupdated: "2024-04-25"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}



# Integrating with *SMS*
{: #deploy-sms}

[IBM Cloud]{: tag-ibm-cloud}

This feature is currently not available in the AI assistant builder of IBM watsonx Orchestrate.{: note}

Add a text messaging integration so your assistant can exchange messages with your customers.
{: shortdesc}

The Short Messaging Service (SMS) supports text-only messages. Typically, SMS restricts the text message length to 160 characters. The Multimedia Messaging Service (MMS) supports sending images and text messages that are over 160 characters in length. When you create a phone number with Twilio, MMS message support is included automatically. IntelePeer MMS message support is not yet available.

Customers send text messages to your hosted phone number. Twilio and IntelePeer use a messaging webhook that you set up to send a POST request with the text message body to your assistant. Each response from the assistant is sent back to Twilio or IntelePeer to be converted to an outbound SMS message that is sent to the customer. The responses are sent to the SMS provider's API for processing. You provide your SMS provider's authentication token information, which serve as your API access credentials.

Refer to the following sections to set up the integration for your SMS provider:

- [Integrating SMS with Twilio](#deploy-sms-twilio)
- [Integrating SMS with IntelePeer](#deploy-sms-intelepeer)

If you want your assistant to be able to switch between voice and text during a customer interaction, enable both the phone and text messaging integrations. The integrations do not need to use the same third-party service provider. For more information, see [Integrating with phone](/docs/watson-assistant?topic=watson-assistant-deploy-phone).

## Integrating *SMS with Twilio*
{: #deploy-sms-twilio}

### Before you begin
{: #deploy-sms-service-setup-twilio}

If you don't have a text messaging phone number, set up an *SMS with Twilio* account and get a phone number.

1.  Go to the [Twilio website](https://www.twilio.com/){: external}.
1.  Create an account. Free trial accounts cannot be used for this integration.
1.  From the **Develop** tab in the sidebar, click **Phone Numbers**. If **Phone Numbers** is not present, go to the Search Bar at the top and search for 'Phone Numbers', then select **Buy a number**.
1.  Follow the instructions to **Buy a number**. If you want to use this number only for testing purposes, buy a toll-free number. Otherwise, follow the [A2P 10DLC registration procedure](https://support.twilio.com/hc/en-us/articles/1260800720410-What-is-A2P-10DLC-). 

    When you get a Twilio phone number, it supports voice, SMS, and MMS automatically. Your new phone number is listed as an active number.

Keep the Twilio web page open in a web browser tab so you can refer to it again later. You can also pin **Phone Numbers** to the sidebar.
{: tip}

### Set up the integration
{: #deploy-sms-setup-twilio}

To set up the integration, complete the following steps:

1. Go to the **Integrations** page by clicking the integrations icon (![Integrations icon](images/integrations-icon.png)) in the left menu.

1. Click **Add** on the *SMS* tile.

1. Click **SMS with Twilio** tile.

1. Click **Confirm**.

1.  From the Twilio site, click on your account name in the upper left menu to go to your account dashboard.

    Copy the following values and store them temporarily, so you can paste them into the *SMS with Twilio* integration setup page in the upcoming steps.

    - Account SID
    - Auth token

1.  Return to the *SMS with Twilio* integration setup page. Click **Next** to go to Step 1 of your *SMS with Twilio* integration setup.

1.  Enter your **Account SID** information. Click **Next** to go to Step 2 of your *SMS with Twilio* integration setup.

1.  Enter your **Auth token** information. Click **Next** to go to Step 3 of your *SMS with Twilio* integration setup.

1.  **Optional**: Enter the phone number that your Twilio account uses for SMS integration. The webhook URI is used to transfer messages, but if you add your phone number in this optional field, you can easily refer to it later. Click **Next** to go to Step 4 of your *SMS with Twilio* integration setup.

1.  Copy the value from the **Webhook URI** field.

    You will add this URI to the webhook configuration in Twilio. If you want to support more than one phone number, you must add the URI to the webhook for each phone number separately.

1.  Go to your Twilio account web page. From the **Develop** tab in the sidebar, click **Phone Numbers > Manage > Active numbers**.

1.  From the **Active Numbers** page, click one of your phone numbers.

1.  Scroll to the **Messaging** section, and then find the **Webhook** field that defines what to do when *A message comes in*.

    Paste the value that you copied from the **Webhook URI** field into it.

1.  If you want to support multiple phone numbers, repeat the previous step for each phone number that you want to use.

1.  Click **Save**.

1.  From the **Develop** tab in the sidebar, click **Messaging > Settings > Geo permissions**. If **Messaging** is not present, go to the Search Bar at the top and search for 'Messaging', then select **SMS Geographic Permissions**.

1.  From the **Messaging Geographic Permissions** page, select the country codes of the phone numbers that can text your Twilio number. By default, no country codes are allowed to text your Twilio number.

1.  Return to the *SMS with Twilio* integration setup page. Click **Finish**.

## Integrating with *SMS with IntelePeer*
{: #deploy-sms-intelepeer}

### Before you begin
{: #deploy-sms-service-setup-intelepeer}

If you don't have a text messaging phone number, set up an *SMS with IntelePeer* account and get a phone number.

1.  Go to the [IntelePeer website](https://www.intelepeer.ai/){: external}.
1.  Create an account or start a free trial.

    When you get an IntelePeer phone number, it supports voice and SMS. If the number is not automatically enabled for SMS, you will need to enable it manually. Your new phone number is listed as an active number. Refer to the [Atmosphere Messaging Quick Start Guide](https://docs.intelepeer.com/atmosphere/Content/Atmosphere-SMS-Messaging/Atmosphere-SMS-Messaging-Quick-Start-Guide.htm){: external}

### Set up the integration
{: #deploy-sms-setup-intelepeer}

To set up the integration, complete the following steps:

1. Go to the **Integrations** page by clicking the integrations icon (![Integrations icon](images/integrations-icon.png)) in the left menu.

1. Click **Add** on the *SMS* tile.

1. Select **SMS with IntelePeer** tile.

1. Click **Confirm**.

1.  From the [IntelePeer Atmosphere](https://atmosphere.intelepeer.com/home/){: external} site, copy the **API Authentication Token** value and store it temporarily, so you can paste it into the *SMS with IntelePeer* integration setup page in the upcoming steps.

1.  From the [IntelePeer Customer Portal](https://customer.intelepeer.com/){: external} site, under the **My Applications** section, select **SMS API Management**. In the **SMS Management** title bar, click the gear icon, here you will set the SMS **Secret Input**. The Secret Input is used to prevent your webserver webhook from processing any inbound-SMS POST request that does not originate from IntelePeer. Set the **Secret Input** value here and remember it as you will need to use the value in the *SMS with IntelePeer* integration setup page in the upcoming steps.

1.  Return to the *SMS with IntelePeer* integration setup page. Click **Next** to go to Step 1 of your *SMS with IntelePeer* integration setup.

1.  Enter your **Account Secret** information. Click **Next** to go to Step 2 of your *SMS with IntelePeer* integration setup.

1.  Enter your **Auth token** information. Click **Next** to go to Step 3 of your *SMS with IntelePeer* integration setup.

1.  **Optional**: Enter the phone number that your Intelepeer account uses for SMS integration. The webhook URI is used to transfer messages, but if you add your phone number in this optional field, you can easily refer to it later. Click **Next** to go to Step 4 of your *SMS with IntelePeer* integration setup.

1.  Copy the value from the **Webhook URI** field.

    You will add this URI to the webhook configuration in IntelePeer. If you want to support more than one phone number, you must add the URI to the webhook for each phone number separately.

1.  Go to your [IntelePeer Customer Portal](https://customer.intelepeer.com/){: external} site, under the **My Applications** section, select **SMS API Management**.

1.  Go to the phone number(s) you want to enable for SMS. Toggle the **Enabled/Disabled** radial button beside the number and set it to *Enabled*. It may take a few minutes for the phone number to become activated for SMS.

1.  Once the phone number has been enabled for SMS, you will see a webhook icon beside the number.

    Paste the value that you copied from the **Webhook URI** field into it.

1.  Click **Save**.

1.  If you want to support multiple phone numbers, repeat the previous step for each phone number that you want to use.


For security reasons, the authentication fields are removed from view after initial setup. If a field required for authentication is changed, then all entries in related fields must be filled and validated again.
{: note}

## SMS Advanced configuration options
{: #deploy-sms-advanced}

The **Advanced options** tab is available after you set up the *SMS* integration. Click the **Advanced options** tab to make any of the following customizations to the messaging behavior:

- **Initiate conversation from inbound messages**: Disable this option if you want to limit messaging support to allow messages that are sent in the context of an ongoing phone integration conversation only, and not allow customers to start a message exchange with the assistant outside of a phone call.
- **Default failure message**: Add a message to send to the customer if the SMS connection fails.
- **Base URL**: This URL is the REST API endpoint for the SMS service you are using.

## Optimize your actions for messaging
{: #deploy-sms-action}

For the best customer experience, design your actions with the capabilities of the *SMS* integration in mind:

- Do not include HTML elements in your text responses.
- The *SMS* integration does not support chat transfers that are initiated with the *connect_to_agent* response type.

- **Image**, **Audio**, **Video** response types allow sending a message containing media. A title and description are sent along with the attachment. Note that depending on the carrier and device of the end user these messages may not be successfully received. For a list of the supported content types for Twilio, see [Twilio: Accepted Content Types for Media](https://www.twilio.com/docs/sms/accepted-mime-types){: external}.

   For more information on these response types, see [Response types reference](/docs/watson-assistant?topic=watson-assistant-response-types-reference).

If you want to use the same action for an assistant that you deploy to many different platforms, add custom responses per integration type. You can add a conditioned response that tells the assistant to show the response only when the *SMS* integration is being used.

For reference documentation, see [*SMS* integration reference](/docs/watson-assistant?topic=watson-assistant-sms-reference).

## Troubleshooting
{: #deploy-sms-troubleshoot}

Find solutions to problems that you might encounter while using the integration.

- If you get a *Forbidden* message, it means the phone number that you specified when you configured the integration cannot be verified. Make sure the number fully matches the SMS phone number.

## Migrating from Voice Agent with Watson
{: #deploy-sms-migrate-from-va}

If you created an {{site.data.keyword.iva_full}} service instance in IBM Cloud to enable customers to exchange text messages with an assistant, use the *SMS* integration instead.

The *SMS* integration provides a more seamless integration with your assistant and supports as many phone numbers as needed. However, the integration currently does not support the following functions:

- Starting an SMS-only interaction with an outgoing text
- Configuring backup locations
- Reviewing the usage summary page. Use IBM Log Analysis instead.

To migrate from {{site.data.keyword.iva_short}} to the {{site.data.keyword.conversationshort}} *SMS* integration, complete the following step:

1.  Do one of the following things:

    - If your {{site.data.keyword.iva_short}} service instance uses an SMS service provider other than Twilio or IntelePeer, you cannot continue to use it. You must create an SMS account with Twilio or IntelePeer first. Complete the [Before you begin - Twilio](#deploy-sms-service-setup-twilio) or [Before you begin - IntelePeer](#deploy-sms-service-setup-intelepeer) steps to create the account. Next, set up the integration.

    - If your {{site.data.keyword.iva_short}} service instance uses Twilio or IntelePeer as its SMS provider, you can go directly to [Set up the integration - Twilio](#deploy-sms-setup-twilio) or [Set up the integration - IntelePeer](#deploy-sms-setup-intelepeer).
