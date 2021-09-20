---

copyright:
  years: 2021
lastupdated: "2021-09-20"

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

Maybe you want one development team to have access to a test assistant and another development team to have access to a production assistant. And you want data scientists to be able to view analytics for user conversation logs from both assistants. And maybe you want a writer to be able to author the dialogue that is used by your assistant to converse with your customers. To manage who can do what with your actions and assistants, you can assign different access roles to different people.

## Granting users access
{: #access-control-task}

1.  Click the User ![User](images/user-icon2.png) icon in the page header.

1.  Make a note of the current instance name, and then click **Manage Users**.

    You are directed to the {{site.data.keyword.cloud}} Identity and Access Management (IAM) page.
1.  Click **Invite users**, and then enter the email addresses of the people to whom you want to grant access. 

    If you plan to grant specific resource-level access to different team members, then add one person at a time.
    {: tip}

1.  Expand *Assign users additional resources*, and then click **IAM services**.
1.  In the *No access* field, choose **Watson Assistant**. 

    You must choose **Account** as the resource group.
    {: important}

1.  Optionally select a specific region and service instance to share with this user. 

    Otherwise, the user access you define is applied to all of your services instances in all data center locations where you have instances.

    Remember, you made a note of the name of the current service instance in an earlier step.

1.  Assign the person to the following role types for the service instance:

    - Platform
    - Service

    For help, see [Popular role assignments](#access-control-recommendations). For a description of all your options, see [Understanding roles](#access-control-iam-roles).

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

## Understanding roles
{: #access-control-iam-roles}

Access to {{site.data.keyword.conversationshort}}, its service instances and all of the resources that are used by the service is managed by {{site.data.keyword.cloud}}. To share a service instance with other users and control access to the instance, you must use the {{site.data.keyword.cloud_notm}} Identify and Access Management user interface. 

{{site.data.keyword.cloud_notm}} breaks down access definitions into the following role types:

- Instance-level platform roles
- Instance-level service roles

An instance-level access role is a role that applies to a service instance and all of the resources that are created as part of the instance.

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

When you assign a service role, you can decide whether to apply the service role to an instance, which effectively applies to every assistant and skill in the instance, or to a specific resource, such as one skill or one assistant.

The highest-level role assignment wins. You can give someone Reader access to everything in an instance, and Manager access to a single skill in that instance. But, you cannot do the opposite. You cannot give a person Manager access to all but one skill. If you assign someone to the Manager role at the instance level, you cannot limit the person's access to a resource in that instance by assigning the person to a Reader level access for a single skill, for example.

#### Instance-level service roles
{: #access-control-global-service-roles}

Choose a service role for the user that will apply to all of the skills and assistants in the instance.

| Role | Privileges of the users in this role |
|------|---------------------------------------|
| **Reader** | Open and read all assistants and skills in the service instance, but not edit them. |
| **Writer** | Read, edit, delete, or create assistants and skill in the service instance. |
| **Manager** | Read, edit, delete, or create assistants and skills in the service instance; view all conversation logs; access the v1 API for all skills in the instance. |
{: caption="Table 2. Global service role details" caption-side="top"}
