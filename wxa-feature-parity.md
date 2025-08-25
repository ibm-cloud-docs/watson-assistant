---

copyright:
  years: 2015, 2025
lastupdated: "2025-08-25"

keywords: feature parity

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Feature parity for {{site.data.keyword.conversationfull}}
{: #wxa-feature-parity}

{{site.data.keyword.conversationfull}} can be deployed as a managed software as a service (SaaS) or installed on premises. New features are continuously added to each deployment's release cycle. To make informed decisions that align with your business needs, it is important to stay informed about the features available in each deployment.

Stay up to date with the latest features through the [Release notes of {{site.data.keyword.conversationshort}}](/docs/watson-assistant?topic=watson-assistant-watson-assistant-release-notes).

The feature parity covers the following deployments:

- IBM Cloud: for the IBM-managed instances that are provisioned as a service on IBM Cloud.

- IBM Software Hub : for client-managed instances that are provisioned on the IBM Software Hub. It is an on-premises deployment and uses a stationary version of the continuous-delivered and continuous-integrated SaaS deployment for each of its releases into IBM Software Hub. 

IBM Software Hub refers to the latest released version on on-premises. For more information about the latest version of Software Hub, refer to [Latest version](/docs/watson-assistant?topic=watson-assistant-release-notes-hub).
 
## Parity by features' capabilities

Features can have their own capabilities, which might have limitations on what deployments support them. In the following sections, you can view the capabilities of each feature and if the deployments support these capabilities.

In the tables, you can find the following indications:
- The green check icon ![Green check icon](images/green-check.svg) indicates that the deployment supports the capability.
- The green check with a warning icon ![Green check with warning icon](images/green-check-warning.svg) indicates that the deployment supports the capability, but the capability might have specific implementations that differ from other deployments.
- The red cross icon ![Red cross icon](images/red-cross.svg) indicates that the deployment does not support the capability.

### Generative AI
{: #wxa-feature-parity-gen-ai}

| Feature | IBM Cloud | IBM Software Hub |
| ---- | ---- | ---- | 
| Select a base model | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) |
| Add prompt instructions | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Enable or disable conversational search for the base LLM | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
{: caption="The support of the Generative AI capabilities on each deployment." caption-side="top"}

### Actions
{: #wxa-feature-parity-actions}

| Feature | IBM Cloud | IBM Software Hub |
| ---- | ---- | ---- | 
| Add Skill-based action | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) |
| Add Custom-built action | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) |
{: caption="Table. The support of the Actions capabilities on each deployment." caption-side="top"}

### Global settings
{: #wxa-feature-parity-global-settings}

| Feature | IBM Cloud | IBM Software Hub |
| ---- | ---- | ---- | 
| Ask clarifying questions | ![Green check icon](images/green-check.svg) | ![Green check with warning icon](images/green-check-warning.svg) [**¹**](#response-modes) 
| Change conversation topic and as confirmation questions | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Use watsonx.ai for information gathering | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Detect mentions of hate, abuse and profanity (HAP) in the content | ![Green check icon](images/green-check.svg) |  ![Red cross icon](images/red-cross.svg) |
| Autocorrection for spelling mistakes | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Customize formats for local and date and time | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Set an algorithm version for the assistant training | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Upload and download the assistant's actions | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
{: caption="The support of the Global settings capabilities on each deployment." caption-side="top"}

**¹ IBM Software Hub :** Customizing response modes for new actions is not available.  
{: #response-modes}

### Evaluate
{: #wxa-feature-parity-evaluate}

| Feature  | IBM Cloud | IBM Software Hub |
| ---- | ---- | ---- | 
| Evaluate response settings | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
{: caption="The support of the Evaluate capabilities on each deployment." caption-side="top"}

### Preview
{: #wxa-feature-parity-preview}

| Feature | IBM Cloud | IBM Software Hub  |
| ---- | ---- | ---- | 
| Preview assistant| ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
{: caption="The support of the Preview capabilities on each deployment." caption-side="top"}

### Publish
{: #wxa-feature-parity-publish}

| Feature |  IBM Cloud | IBM Software Hub |
| ---- | ---- | ---- | 
| Publish content and revert publishing | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| View all versions | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Download published version | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
{: caption="The support of the Publish capabilities on each deployment." caption-side="top"}

### Environments
{: #wxa-feature-parity-environments}

| Feature | IBM Cloud | IBM Software Hub  |
| ---- | ---- | ---- | 
| Add and preview environment | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Get API details for the environment | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Set up pre-message webhook | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Set up post-message webhook | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Set up log webhook | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Set up audio webhook | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Set up inactivity history | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Enable session history | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| View the added channels, content and extensions for the environment | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
{: caption="The support of the Environments capabilities on each deployment." caption-side="top"}

### Analyze
{: #wxa-feature-parity-analyze}

| Feature |  IBM Cloud | IBM Software Hub |
| ---- | ---- | ---- |
| View data for action completion | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| View data for conversational search responses | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| View data for recognized and unrecognized requests | ![Green check icon](images/green-check.svg) | ![Red cross icon](images/red-cross.svg) |
| View data about conversations with assistants | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
{: caption="The support of the Analyze capabilities on each deployment." caption-side="top"}

### Integration with web chat
{: #wxa-feature-parity-integrate-web-chat}

| Feature | IBM Cloud | IBM Software Hub |
| ---- | ---- | ---- | 
| Customize the chat UI | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Edit the desktop and mobile launcher | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Edit the chat home screen | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Add live chat integration with eGain provider  | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Add live chat integration	with Enghouse provider  | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Add live chat integration	with Genesys SIP provider  | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Add live chat integration	with Kustomer provider  | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) |
| Add live chat integration	with NICE inContact provider  | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Add live chat integration	with Oracle provider  | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Add live chat integration	with Salesforce provider  | ![Green check icon](images/green-check.svg) |  ![Red cross icon](images/red-cross.svg) |
| Add live chat integration	with Twilio provider  | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Add live chat integration	with Zendesk provider  | ![Green check icon](images/green-check.svg) | ![Red cross icon](images/red-cross.svg) |
| Add live chat integration	with your own provider  | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Add suggestion to connect to agent | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Enable web chat security | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Get the code to embed the web chat | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
{: caption="The support of the Integration with Web chat capabilities on each deployment." caption-side="top"}


#### Integration with Phone
{: #wxa-feature-parity-integrate-phone}

| Feature | IBM Cloud | IBM Software Hub  |
| ---- | ---- | ---- | 
| Connect to Genesys SIP provider | ![Green check icon](images/green-check.svg) | ![Red cross icon](images/red-cross.svg) |
| Connect to Genesys Audio Connector provider |  ![Green check icon](images/green-check.svg) | ![Green check with warning icon](images/green-check-warning.svg)[**¹**](#sw-genesys-audio-and-speech)  |
| Connect to Twilio provider | ![Green check icon](images/green-check.svg) | ![Red cross icon](images/red-cross.svg) |
| Connect to NICE inContact provider | ![Green check icon](images/green-check.svg) | ![Red cross icon](images/red-cross.svg) |
| Bring your own phone provider | ![Green check icon](images/green-check.svg) | ![Red cross icon](images/red-cross.svg) |
| Manage phone numbers |  ![Green check icon](images/green-check.svg) | ![Red cross icon](images/red-cross.svg) |
| Configure speech to text and text to Speech |  ![Green check icon](images/green-check.svg) | ![Red cross icon](images/red-cross.svg) |
| Configure SIP trunking security options | ![Green check icon](images/green-check.svg) | ![Red cross icon](images/red-cross.svg) |
| Handle call and transfer failures | ![Green check icon](images/green-check.svg) | ![Red cross icon](images/red-cross.svg) |
{: caption="The support of the Integration with Phone capabilities on each deployment." caption-side="top"}

**¹ IBM Software Hub :** Connecting to Genesys Audio Connector and speech configuration might be available via patch.   
{: #sw-genesys-audio-and-speech}

### Integration with other channels
{: #wxa-feature-parity-integrate-channels}

| Feature |  IBM Cloud | IBM Software Hub  |
| ---- | ---- | ---- |
| Add SMS as a channel and customize provider with IntelePeer and Twilio | ![Green check icon](images/green-check.svg) | ![Red cross icon](images/red-cross.svg) |
| Add and customize Facebook messenger as a channel |  ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) |
| Add and customize Genesys Bot Connector as a channel | ![Green check icon](images/green-check.svg) | ![Green check with warning icon](images/green-check-warning.svg)[**¹**](#sw-genesys-bot-connector) |
| Add and customize Slack as a channel | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Add and customize Microsoft teams as a channel |  ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) |
| Add and customize WhatsApp with Twilio as a channel |  ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) |
{: caption="The support of the Integration with other channels capabilities on each deployment." caption-side="top"}

**¹ IBM Software Hub :** Genesys Bot Connector as a channel might be available via patch.   
{: #sw-genesys-bot-connector}

### Search integration
{: #wxa-feature-parity-search-integration}

| Feature | IBM Cloud | IBM Software Hub |
| ---- | ---- | ---- |
| Add search integration with Elasticsearch | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Add search integration with Milvus |  ![Green check icon](images/green-check.svg) | ![Red cross icon](images/red-cross.svg) |
| Add search integration with a custom service | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Configure contextual awareness for conversational search | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Configure the search for conversational search | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Configure citations for conversational search | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Configure the content for "No results" and "Connectivity issues" | ![Green check icon](images/green-check.svg) |  ![Green check icon](images/green-check.svg) |
{: caption="The support of the Search integration capabilities on each deployment." caption-side="top"}

### Integration with other extensions
{: #wxa-feature-parity-integration-extensions}

| Feature |  IBM Cloud | IBM Software Hub  |
| ---- | ---- | ---- |
| Add integration with Segment as an extension |  ![Green check icon](images/green-check.svg) | ![Red cross icon](images/red-cross.svg) |
| Build a custom extension | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) |
{: caption="The support of the Integration with other extensions capabilities on each deployment." caption-side="top"}

#### Activity Log
{: #wxa-feature-parity-activity-log}

| Feature | IBM Cloud | IBM Software Hub |
| ---- | ---- | ---- | 
| View the activity history for the assistant | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
{: caption="The support of the Activity Log capabilities on each deployment." caption-side="top"}

#### Dialog support
{: #wxa-feature-parity-dialog-support}

| Feature |  IBM Cloud | IBM Software Hub |
| ---- | ---- | ---- |
| Adding dialog | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Dialog creation workflow | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Creating intents | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Using built-in intents | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Creating a dialog | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Testing your dialog | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Gathering information with slots | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Managing workflow with versions |  ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
{: caption="Dialog support on each deployment." caption-side="top"}

#### Assistant settings
{: #wxa-feature-parity-assistant-settings}

| Feature |  IBM Cloud | IBM Software Hub |
| ---- | ---- | ---- | 
| View the assistant details | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Configure security certificates (SSL/TLS) | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Get the details of assistant IDs and API data | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Download or upload assistant data | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
| Delete assistant | ![Green check icon](images/green-check.svg) | ![Green check icon](images/green-check.svg) | 
{: caption="The support of the Assistant settings capabilities on each deployment." caption-side="top"}
