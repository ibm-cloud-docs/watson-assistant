---

copyright:
  years: 2026, 2026
lastupdated: "2026-07-24"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Upgrading to agents with an in-place upgrade
{: #in-place-upgrade}

Use this guide to upgrade a watsonx Assistant instance to watsonx Orchestrate. The upgrade adds the agent-building capabilities of watsonx Orchestrate to your existing instance. Your conversational AI assets, including assistants, dialog flows, and actions, remain in place and continue to operate without disruption.

## Before you begin
{: #in-place-upgrade-before-you-begin}

Verify that your instance meets the following conditions before you start the upgrade:

- The watsonx Assistant instance is provisioned on IBM Cloud.
- The instance is on a [supported service plan](#in-place-upgrade-supported-plans).

### Supported service plans
{: #in-place-upgrade-supported-plans}

| Plan | In-place upgrade available |
|------|---------------------------|
| Standard | Yes |
| Plus | Yes |
| Enterprise | Yes |
| Lite | No |
| Trial | No |
| Enterprise with Data Isolation | No |
| Premium API | No |
| Premium MAU | No |

## Upgrade your instance to watsonx Orchestrate
{: #in-place-upgrade-steps}

Complete the following steps to upgrade your watsonx Assistant instance:

1. Go to [cloud.ibm.com/resources](https://cloud.ibm.com/resources) and sign in with your IBM Cloud credentials.

1. Locate and open the instance page for a watsonx Assistant instance on a compatible plan.

1. If your account and instance are eligible, an **Upgrade to agents** button appears on the instance page. If the button is not visible, your instance plan does not qualify for the in-place upgrade.

1. Click **Upgrade to agents**. The system begins provisioning watsonx Orchestrate features on your instance.

1. After the upgrade completes, click **Launch Agent Builder**. The watsonx Orchestrate product interface opens directly from the watsonx Assistant tile.

## Navigate back to Assistant builder
{: #in-place-upgrade-navigate-back}

After the upgrade, access Assistant builder directly from within watsonx Orchestrate:

1. In the watsonx Orchestrate interface, click the menu icon in the navigation menu.

1. Click **Assistant builder** to open your existing assistants.

## What remains in place after the upgrade
{: #in-place-upgrade-what-remains}

Your existing AI assistants and all associated configuration remain in place after the upgrade completes. The following assistant types continue to operate without modification:

- Assistants that use Dialog flows
- Assistants that use Actions
