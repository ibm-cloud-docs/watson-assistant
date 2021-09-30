---

copyright:
  years: 2020, 2021
lastupdated: "2021-09-28"

subcollection: watson-assistant

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# Managing access
{: #access-control}

You can give other people access to your {{site.data.keyword.conversationshort}} resources, and control the level of access they get.
{: shortdesc}

Maybe you want one development team to have access to a test assistant and another development team to have access to a production assistant. And you want data scientists to be able to view analytics for user conversation logs from both assistants. And maybe you want a writer to be able to author the conversation that is used by your assistant with your customers. To manage who can do what with your assistants, you can assign different access roles to different people.

## Before you grant access to others
{: #access-control-prereqs}

For each person to whom you grant access to your {{site.data.keyword.conversationshort}} service instance, decide whether you want to give the person a role with instance-level or resource-level access. Instance-level access applies to all of the assistants in a single service instance. Resource-level access applies to individual assistants within a service instance only.

## Granting users access to your resources
{: #access-control-task}

1.  If you plan to give a user access to an assistant in your service instance, you need to get the ID for the assistant's *draft* and *live* environments. You need to provide these IDs in a later step. To learn more about environments, see [Environments](/docs/watson-assistant?topic=watson-assistant-publish-overview#environments).

    - To get the **draft environment** ID for your assistant, go to the **Preview** page. Click **See your test integrations**, and then click **Test integration settings**. From **API details**, copy the **Environment ID** and paste it somewhere that you can access it from later.

    - To get the **live environment** ID for your assistant, go to the **Connect** page. Click **Settings**. From **API details**, copy the **Environment ID** and paste it somewhere that you can access it from later.

1.  Click the User ![User](images/user-icon2.png) icon in the page header.

1.  Make a note of the current instance name, and then click **Manage Users**.

1.  From the **Access and permissions** dialog, click the link for **Go to the Identity and Access Management page**.

1.  You are directed to the {{site.data.keyword.cloud}} Identity and Access Management (IAM) page.

1.  Click **Invite users**, and then enter the email addresses of the people to whom you want to grant access. 

    If you plan to grant specific resource-level access to different team members, then add one person at a time.
    {: tip}

1.  Expand *Assign users additional resources*, and then click **IAM services**.

1.  In the *Which service do you want to assign access to?* field, choose **Watson Assistant**. 

1.  Optionally, you can scope the access by choosing **Resources based on selected attributes**. Otherwise, the user access you define is applied to all of your services instances in all data center locations where you have instances.

    Choices include:
    
    - Resource group
    - Location 
    - Service instance: This is where you can choose a specific instance including your assistant. Remember, you made a note of the name of the current service instance in an earlier step.
    - Resource type
    - Assistant ID: Paste the associated ID (that you copied in an earlier step) into the **Assistant or Skill ID** field.

1.  Assign the person to the following role types for the service instance:

    - Platform access
    - Service access

    For help, see [Popular role assignments](#access-control-recommendations). For a description of all your options, see [Understanding roles](#access-control-iam-roles).

1.  **Optional**: Select a single resource, such as a skill or assistant, and then assign the person to the appropriate service role for the resource.

    For a description of your resource-level service options, see [Resource-level access roles](#access-control-resource-service-roles).

1.  Click **Add**.

1.  Click **Invite** to finish the process.

## Popular role assignments
{: #access-control-recommendations}

To get you started quickly, consider applying these roles at first.

- To give someone the same level of access to a {{site.data.keyword.conversationshort}} service instance as you have, assign the user to the following roles:

    - Instance platform role: **Administrator**
    - Instance service role: **Manager**

- To give someone manager access to a specific set of resources, but read-only access to everything else, assign the user to the following roles:

    - Instance platform role: **Viewer**
    - Instance service role: **Reader**

    Then, for each assistant that you want the person to be able to manage, add another role assignment like this:

    - Instance platform role: **Viewer**
    - For an individual assistant, assign the **Manager** role.

## Understanding roles
{: #access-control-iam-roles}

Access to {{site.data.keyword.conversationshort}}, its service instances, and all of the resources that are used by the service is managed by {{site.data.keyword.cloud}}. To share a service instance with other users and control access to the instance, you must use the {{site.data.keyword.cloud_notm}} Identify and Access Management user interface. 

{{site.data.keyword.cloud_notm}} breaks down access definitions into the following role types:

- Instance-level platform roles
- Instance-level service roles
- Resource-level service roles

An instance-level access role is a role that applies to a service instance and all of the resources that are created as part of the instance. A resource-level service role gives you the ability to apply a finer-tuned level of access control to a single skill or assistant in an instance.

### Platform roles
{: #access-control-global-platform-roles}

A platform role controls a person's ability to access a service instance in {{site.data.keyword.cloud_notm}}. Choose a platform role to assign to the user.

| Role | Privileges of the users in this role |
|------|---------------------------------------|
| **Administrator** | Access and change all resources for the instance, and invite other people to access the instance. |
| **Viewer** | View the service instance, but cannot invite others to access the instance. |
{: caption="Table 1. Global platform role details" caption-side="top"}

The **Editor** and **Operator** platform roles are equivalent to the Administrator role.

At a minimum, you must give someone *Viewer* platform access to a service instance or they cannot access anything.
{: important}

### Service roles
{: #access-control-service-roles}

A service role controls what a person can do in {{site.data.keyword.conversationshort}}.

When you assign a service role, you can decide whether to apply the service role to an instance, which effectively applies to every assistant in the instance, or to a specific resource, such as one assistant.

The highest-level role assignment wins. You can give someone Reader access to everything in an instance, and Manager access to a single assistant in that instance. But, you cannot do the opposite. You cannot give a person Manager access to all but one assistant. If you assign someone to the Manager role at the instance level, you cannot limit the person's access to a resource in that instance by assigning the person to a Reader level access for a single assistant, for example.

#### Instance-level service roles
{: #access-control-global-service-roles}

Choose a service role for the user that will apply to all of the assistants in the instance.

| Role | Privileges of the users in this role |
|------|---------------------------------------|
| **Reader** | Open and read all assistants in the service instance, but not edit them. |
| **Writer** | Read, edit, delete, or create assistants in the service instance. |
| **Manager** | Read, edit, delete, or create assistants in the service instance; view all conversation logs; access the v1 API for all skills in the instance. |
{: caption="Table 2. Global service role details" caption-side="top"}

#### Resource-level service roles
{: #access-control-resource-service-roles}

To fine tune a person's level of access to individual assistants within the instance, assign one or more resource-level service roles to the user.

You do not need to assign resource-level roles to people who already have access to all the resources based on their global service role. But, if you want to tailor a bit more who can read, edit, or add to specific assistants within the instance, then apply resource-level roles.

You cannot assign someone to a resource-level role that has fewer privileges than the instance-level role to which the person is assigned. If the person has an instance-level Manager access role, for example, you cannot give them read-only access to a specific assistant. The higher-level role assignment wins.
{: important}

| Role | Privileges of the users in this role |
|------|---------------------------------------|
| Reader | Open and read the assistant, but not edit it. |
| Writer | Read, edit, delete, or create an assistant. |
| Manager | Read, edit, delete, or create an assistant, and view analytics (conversation logs). |
{: caption="Table 3. Resource service role details" caption-side="top"}

Anyone who creates an assistant is automatically granted the Manager service role to that resource.

## Common role assignments
{: #access-control-common-roles}

| Goal | Instance-level platform role | Instance-level service roles | Resource-level service roles |
|------|------------------------------|------------------------------|-----------------------------|
| Make someone a service instance co-owner | Administrator | Manager | N/A |
| Give someone reader access to only one assistant in an instance | Viewer | Reader | Reader |
| Allow someone to edit and view logs of all the assistants in the service instance | Viewer | Manager | N/A |
| Allow someone to edit an assistant in the service instance, but not view logs | Viewer | Writer | Writer |
| Give someone full access to only one assistant in an instance | Viewer | Reader | Manager |
{: caption="Table 4. Common role assignments" caption-side="top"}

N/A stands for no assignment, meaning no role of the type is assigned.

## Resource-level role impact on available actions
{: #access-control-ui-impact}

The {{site.data.keyword.conversationshort}} user interface and API comply with the access roles that are defined for a service instance. When someone logs in to the user interface, it adjusts to show only what the current user can access, and it disables functions that the user does not have permissions to do. Similarly, the API allows access only to resources and methods that are permitted for the role that is associated with the specified API key.

If you cannot access the API Details page for a skill or assistant, you might not have the access that is required to use the instance-level API credentials. You can use a personal API key instead. Go to the [IBM Cloud API keys](https://cloud.ibm.com/iam/apikeys){: external} page to create an IBM Cloud API key to use to authenticate your API requests. For more information, see [Managing user API keys](/docs/account?topic=account-userapikey){: external}. With the personal key, you can make API requests that you have the appropriate privileges to complete. 
{: note}

The following table shows the UI and API actions that can be performed by different resource-level service roles.

| Action | Reader | Writer | Manager |
|--------|--------|--------|---------|
| Open and view an assistant or integration | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| View API details for an assistant  | | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Create an assistant | | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Rename, edit, delete an assistant | | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Create, edit, or delete an integration | | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Add actions | | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Swap versions for an assistant | | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Revert to a previous version | | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Save or delete versions | | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Import, add, edit, or delete actions or action examples | | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Edit system actions | | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Open and view action steps | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Add, move, edit, or delete action steps | | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Change action step settings | | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Test in actions Preview pane | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Test in search "Try it out" pane | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Add, edit, or delete session variables in actions | | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| View analytics | | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| v1 runtime API (`/message` endpoint) | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| v2 runtime API (`session` and `/message` endpoints) | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| v1 authoring API (all but `/message` endpoint) | | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| v1 and v2 logs API | | | ![checkmark icon](../../icons/checkmark-icon.svg) |
{: row-headers}
{: class="comparison-table"}
{: caption="Table 5. Action privileges per service role" caption-side="top"}
{: summary="This table has row and column headers. The row headers identify the user interface or API actions. The column headers identify the different resource-level roles. To understand which roles can do an action, go to the row that describes the action, and find the columns for the role you are interested in."}
