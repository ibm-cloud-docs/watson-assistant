---

copyright:
  years: 2020, 2021
lastupdated: "2021-09-10"

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

# Integrating with phone ![Plus or higher plans only](images/plus.png)
{: #deploy-phone}

By adding the phone integration to your assistant, you can make your assistant available to customers over the phone.
{: shortdesc}

When you add the phone integration to your assistant, you can automatically generate a working phone number that is automatically connected to your assistant. Or, if you prefer, you can connect the assistant to your existing infrastructure by configuring an existing Session Initiation Protocol (SIP) trunk.

A SIP trunk is equivalent to an analog telephone line, except it uses Voice over Internet Protocol (VoIP) to transmit voice data and can support multiple concurrent calls. The trunk can connect to the public switched telephone network (PSTN) or your company's on-premises private branch exchange (PBX). If you choose to generate a free phone number for your assistant, a SIP trunk is automatically provisioned from IntelePeer. You can also choose to use an existing SIP trunk from a provider such as IntelePeer, Genesys, or Twilio.

Generating a free phone number is available only with new phone integrations. If you have an existing phone integration and you want to switch to a free phone number, you must delete the existing integration and create a new one.
{: note}

When your customer makes a phone call using the telephone number connected to your assistant, the phone integration answers. The integration converts output from your assistant into voice audio by using the {{site.data.keyword.texttospeechfull}} service. The audio is sent to the telephone network through the SIP trunk. When the customer replies, the voice input is converted into text by using the {{site.data.keyword.speechtotextfull}} service.

This feature is available only to Plus or Enterprise plan users. <!--Note that {{site.data.keyword.speechtotextshort}} and {{site.data.keyword.texttospeechshort}} charges are included in the cost of a [monthly active user](/docs/assistant?topic=assistant-services-information#services-information-user-based-plans) (MAU). -->

Depending on the architecture of your existing telephony infrastructure, there are multiple ways you might integrate it with Watson Assistant. For more information about common integration patterns, read the blog post [Hey Watson, can I have your number?](https://medium.com/ibm-watson/hey-watson-can-i-have-your-number-7de8fc7621ed) on Medium.
{: tip}

## Set up the integration
{: #deploy-phone-setup}

You must have Manager service level access to the instance. <!-- For more information about access levels, see [Managing access to resources](/docs/assistant?topic=assistant-access-control). -->

<!--To watch a video that walks through the setup process, see [Phone and SMS Integration](https://community.ibm.com/community/user/watsonapps/viewdocument/phone-and-sms-integration?CommunityKey=7a3dc5ba-3018-452d-9a43-a49dc6819633&tab=librarydocuments){: external} in the *IBM Watson Apps Community*.-->

To set up the integration, complete the following steps:

1. In the **Integrations** section on the main page for your assistant, click **Add integration**.

1. On the **Add integration** page, click **Phone**.

1. Click **Create**.

1. Choose whether you want to generate a free phone number for your assistant or connect to an existing SIP trunk:

    - To generate a free phone number for your assistant, click **Generate a free phone number**.

      Generating a free phone number is supported only for {{site.data.keyword.conversationshort}} instances in the Dallas and Washington DC data centers.
      {: note}

    - To use an existing phone number you have already configured with a [SIP trunk provider](#deploy-phone-sip-providers), click **Use an existing phone number with an external provider**.

    Click **Next**.

1. If you are using an existing phone number, follow the instructions to configure the SIP trunk. (If you are generating a free phone number, skip this step).

    1. On the **Bring your own SIP trunk** page, copy the SIP URI and assign it to your SIP trunk. Click **Next**.

    1. On the **Phone number** page, specify the phone number of the SIP trunk. Specify the number by using the international phone number format: `+1 958 555 0123`. Do not surround the area code with parentheses.

      Currently, only one primary phone number can be added during initial setup of the phone integration. You can add more phone numbers in the phone integration settings later.

      Click **Next**.

<!--   You might have only the one phone that you created through your SIP trunk provider in the previous step, or you might have a set of numbers.

    - If you have one phone number, add it to the field.

      Specify the number by using the international phone number format: `+1 958 555 0123`. Do *not* surround the area code with parentheses, such as (958).

    - If you have multiple phone numbers, click **Add**.

      Add a phone number and an optional description, and then click the checkmark icon ![checkmark icon](images/phone-checkmark-save.png) to save the number.

      - To add more phone numbers one by one, click the *add phone number* icon (![Add phone number][images/phone-integ-add-number.png]), and then specify the phone number and an optional description. Repeat to add more numbers.

      {: important}

     The phone numbers must be unique per phone integration. If you use Twilio as the SIP trunk provider, you can use the same phone number for the phone and text messaging integrations.
-->

1. On the **Speech to Text** page, select the instance of the {{site.data.keyword.speechtotextshort}} service you want to use for the phone integration.

    - If you have existing {{site.data.keyword.speechtotextshort}} instances, select the instance you want to use from the list.

    - If you do not have any existing {{site.data.keyword.speechtotextshort}} instances, click **Create new instance** to create a new Plus instance.

1. In the **Choose your Speech to Text language model** field, select the language model you want to use.

    The list of language models is automatically filtered to use the same language as your assistant. To see all language models, toggle the **Filter models based on assistant language** switch to **Off**.

    If you created specialized custom models that you want your assistant to use, choose the {{site.data.keyword.speechtotextshort}} service instance that hosts the custom models now, and you can configure your assistant to use them later. The {{site.data.keyword.speechtotextshort}} service instance must be hosted in the same location as your {{site.data.keyword.conversationshort}} service instance. <!--For more information, see [Using a custom language model](/docs/assistant?topic=assistant-dialog-voice-actions#dialog-voice-actions-custom-language).-->
    {: note}

    For more information about language models, see [Languages and models](https://cloud.ibm.com/docs/speech-to-text?topic=speech-to-text-models){: external} in the {{site.data.keyword.speechtotextshort}} documentation.

    Click **Next**.

1. On the **Text to Speech** page, select the instance of the {{site.data.keyword.texttospeechshort}} service you want to use for the phone integration.

    - If you have existing {{site.data.keyword.texttospeechshort}} instances, select the instance you want to use from the list.

    - If you do not have any existing {{site.data.keyword.texttospeechshort}} instances, click **Create new instance** to create a new Standard instance.

1. In the **Choose your Text to Speech voice** field, select the voice you want to use.

    The list of voices is automatically filtered to use the same language as your assistant. To see all voices, toggle the **Filter voices based on assistant language** switch to **Off**.

    For more information about voice options, and to listen to audio samples, see [Languages and voices](https://cloud.ibm.com/docs/text-to-speech?topic=text-to-speech-voices){: external} in the {{site.data.keyword.texttospeechshort}} documentation.

    Click **Next**.

<!--   Stop and create speech service instances yourself before you finish setting up the integration in the following cases:

    - If you have Lite plan instances of the speech services, the automatic creation process is not started. Consider deleting the lite plan instances or create Plus plan instances of the services.
    - If you want to use instances that are dedicated to handling speech services for your assistant only, and your existing instance is already in use by other applciations.
    - If you want to use a paid plan other than Plus.
    - If you have an Enterprise with Data Isolation {{site.data.keyword.conversationshort}} plan, create Premium plan instances of the speech services so you can select them during the setup process.
    
    Create the speech instances in the same data center location before you set up the integration. Then, you can choose the existing instances from the list.
    
    If you want to use a model that was created in a different service instance, click **More options** to show all service instances that you can access as options. <!--For example, if you created specialized custom models that you want your assistant to use, you can find and select them.



    <!-- - **{{site.data.keyword.speechtotextshort}}**: Optionally choose a different {{site.data.keyword.speechtotextshort}} service language model to use to define the language your assistant will use when it transcribes what customers say.

      For example, indicate whether to use British or American English. The list shows options from {{site.data.keyword.speechtotextshort}} service instances that you can access. 
      

    - **{{site.data.keyword.texttospeechshort}}**: Optionally choose a different {{site.data.keyword.texttospeechshort}} service voice model to use a different voice for your assistant. 

      The list shows options from {{site.data.keyword.texttospeechshort}} service instances that you can access. 
      

-->

<!-- If you want your assistant to be able to switch between voice and text during a customer interaction, enable both the phone and SMS with Twilio integrations. The integrations do not need to use the same third-party service provider. For more information, see [Integrating with *SMS with Twilio*](/docs/assistant?topic=assistant-deploy-sms). -->

Any speech service charges that are incurred by the phone integration are billed with the {{site.data.keyword.conversationshort}} service plan as *voice add-on* charges. After the instances are created, you can access them directly from the IBM Cloud dashboard. Any use of the speech instances that occurs outside of your assistant are charged separately as speech service usage costs.
{: important}

The phone integration setup is now complete. On the **Phone** page, you can click the tabs to view or edit the phone integration.

If you chose to generate a free telephone number, your new number is displayed on the **Phone number** tab immediately. However, provisioning the new number so it is ready to use might take several minutes.
{: note}

## Adding more phone numbers

If you are using existing phone numbers you configured using a SIP trunk provider, you can add multiple numbers to the same phone integration.

If you generated a free phone number, you cannot add more numbers.
{: note}

To add more phone numbers:

1. In the phone integration settings, go to the **Phone number** tab.

1. Use one of the following methods to add phone numbers:

    - To add phone numbers one by one, type each number in the table, along with an optional description. Click the checkmark icon ![checkmark icon](images/phone-checkmark-save.png) to save each number.

    - To import a set of phone numbers that are stored in a comma-separated values (CSV) file, click the *Upload a CSV file* icon (![Add phone number][images/phone-integ-import-number.png]), and then find the CSV file that contains the list of phone numbers.

      The phone numbers you upload will replace any existing numbers in the table.
