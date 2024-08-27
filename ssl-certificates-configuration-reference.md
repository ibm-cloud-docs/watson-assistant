---

copyright:
  years: 2021, 2024
lastupdated: "2024-08-27"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}


# Security certificates reference
{: #ssl-certificates-configuration-reference}

You can use `Trust uploaded certificates and any certificates signed by a trusted authority` or `Trust uploaded certificates` to the following methods for connecting an assistant to an external service specified by a user:

- [Custom extensions](/docs/watson-assistant?topic=watson-assistant-search-overview#search-overview-extension)
- Conversational skills
- [Premessage](/docs/watson-assistant?topic=watson-assistant-webhook-pre), [Postmessage](/docs/watson-assistant?topic=watson-assistant-webhook-post), and [Log webhooks](/docs/watson-assistant?topic=watson-assistant-webhook-log)
- [Search integrations](/docs/watson-assistant?topic=watson-assistant-search-overview) (except {{site.data.keyword.discoveryshort}} search integration)

You don’t need the security verification for [{{site.data.keyword.discoveryshort}} search integration](/docs/watson-assistant?topic=watson-assistant-search-add), because the connections are managed internally and secured automatically. {: note}

## Methods for choosing the Security certificates option

In the example below, three possible Security certificate options are discussed with which you can  achieve an optimal balance of security and convenience for an assistant with the following connection details.

Consider an assistant with the following connections:
- Three conversational skills each of which points to a different secure service.  All three services are signed by the same private authority.
- Two custom extensions, each of which points to a secure service whose certificate is signed by the same publicly trusted authority.
- One search integration which connects to an Elasticsearch instance with a self-signed certificate (which is typical for Elasticsearch instances in IBM Cloud).
- One log webhook, which points to an insecure service (with a URL that starts with `http://` instead of `https://`).  

Pointing to an insecure service is not recommended and your assistant can’t verify the identity of such a service.{: note}

### Method 1
{: #method1}
- Create a PEM file containing:
  * The certificate for the private authority that signed the certificates for the three secure services that implement the conversational skills.
  * The self-signed certificate for the Elasticsearch instance.
- Select `Trust uploaded certificates and any certificates signed by a trusted authority`.

Analysis
- More convenient option to use.
- You don’t need any additional effort to make the two custom extensions work because the services they point to have certificates that are signed by a publicly trusted authority. 
- You need only one certificate for the three conversational skills because they are all signed by the same authority and the certificate for that authority was included in the PEM file.
- You can add additional connections to services who certificates are also signed by the same authority without updating the PEM file.

### Method 2
{: #method2}
- Create a PEM file containing:
  * The certificate for the private authority that signed the certificates for the three secure services that implement the conversational skills.
  * The certificate for the publicly trusted authority that signed the certificates for the two  secure services that implement the custom extensions.
- The self-signed certificate for the Elasticsearch instance.
- Select `Trust uploaded certificates`.

Analysis
-	Less convenient because the PEM file requires an additional entry for the authority certificate of custom extensions. 
-	You must update the PEM file, when other services that are signed by publicly trusted authorities are added in the future. 
-	Slightly more secure because it only depends on the one indicated publicly trusted authority being secure instead of depending on all publicly trusted authorities being secure.
- The slight security advantage is not important to most users because all of the publicly trusted authorities are extremely secure.

### Method 3
{: #method3}
-	Create a PEM file containing:
    * The six certificates for the six secure services that the assistant connects to (three for conversational skills, two for custom extensions, and one for Elasticsearch).
    * The self-signed certificate for the Elasticsearch instance.
-	Select `Trust uploaded certificates`.

Analysis
-	Less convenient because it requires more certificates in the PEM file.
-	Requires an update to PEM file to add any additional service calls.
-	Slightly more secure because it does not assume that any public or private certifying authority is secure. 
-	The additional security is not needed by most users because the public certifying authorities are extremely secure and private certifying authority is controlled by you and hence can be a secure.
- This option is available for those who want the greatest security possible.

Your assistant does not verify the log webhook service in any of the above mentioned methods because the log webhook points to an insecure server and the call to log webhook continues to work. But the messages sent to and from the service lack encryption, making them vulnerable to imposter attacks.

The best way to address the vulnerabilities:
-	Make the service more secure by implementing `https`.
-	Update your assistant to call that `https` endpoint.
-	Update the PEM file for your assistant, if needed.



