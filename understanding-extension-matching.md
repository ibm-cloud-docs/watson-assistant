---

copyright:
  years: 2026, 2026
lastupdated: "2026-02-04"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Understanding extension matching during action migration
{: #understanding-extension-matching}

When you migrate {{site.data.keyword.conversationshort}} action skill, copy an action to another assistant, duplicate an action, or import an action that includes callout configurations, the system attempts to use the extensions that match best in the target assistant. This process might lead to unexpected behavior, such as an action that points to a different extension after migration. 

If the target assistant contains multiple extensions with the same endpoint configuration (even if the overall specs differ), the system might link the action to the wrong extension.

Before you copy or import actions, ensure that the target assistant is already configured with the required extensions. This preparatory step reduces mismatches. {: important}

## Reasons for the mismatch

An Assistant's action skill step that has a callout configuration has the following aspects that are relevant to the matching algorithm. 

 - Callout hash
 - Callout path
 - Callout HTTP verb

The callout hash is a hash value that represents the entire operation object (/endpoint) configuration to which the assistant's action skill step is configured to use. The callout path and HTTP verb values are derived from the same configuration in the OpenAPI extension spec's operation object. 

Before importing any skill, action, or step, the system expects the target assistant to already contain imported extensions that define the same operation objects as the source assistant. {: note}

When you import a skill or action or step, the system tries to match the hash, path, and HTTP verb values from the assistant skill with the available list of operation objects in the target assistant extensions. The system assumes a mismatch when it is unable to find an operation object that matches all three criteria or `/aspects` across all extension specs in the target assistant. 

If multiple extension specs define the same operation object configuration, the system uses the first matching extension spec.

The {{site.data.keyword.conversationshort}} system generates hash values for operation object specifications in the OpenAPI extension specs without dereferencing them. Hence, any modifications that you make to referenced components in your OpenAPI spec is not accounted in the hash generation process.{: note}

## Methods to prevent extension mismatch

To prevent incorrect extension matching, consider one of the following options:

- **Remove duplicate extensions**
    
    Delete extensions in the target assistant that contain duplicate operation object specifications.

- **Clean up duplicate operation objects**
     
     Remove duplicate operation objects from extensions and ensure uniqueness.

- **Version your extensions explicitly**
    
    This approach is time-consuming and might require manual reconfiguration of callouts that reference modified operation objects.

    Assign unique version identifiers to each extension spec and include them in:
    
    * The document-level attributes (name, description, summary)
    * Each operation object
    * This ensures unique hash values for every operation object

