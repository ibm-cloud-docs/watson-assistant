---

copyright:
  years: 2021, 2024
lastupdated: "2024-12-20"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# High availability and disaster recovery
{: #admin-recovery}

{{site.data.keyword.conversationfull}} is highly available within multiple {{site.data.keyword.cloud}} locations (for example, Dallas and Washington, DC). However, recovering from potential disasters that affect an entire location requires planning and preparation.
{: shortdesc}

You are responsible for understanding your configuration, customization, and usage of {{site.data.keyword.conversationshort}}. You are also responsible for being ready to re-create an instance of the service in a new location and to restore your data in any location. See [How do I ensure zero downtime?](/docs/resiliency?topic=resiliency-ha-redundancy#zero-downtime){: external} for more information.

## High availability
{: #admin-recovery-ha}

{{site.data.keyword.conversationshort}} supports high availability with no single point of failure. The service achieves high availability automatically and transparently by using the multi-zone region feature provided by {{site.data.keyword.cloud_notm}}.

{{site.data.keyword.cloud_notm}} enables multiple zones that do not share a single point of failure within a single location. It also provides automatic load balancing across the zones within a region.

## Disaster recovery
{: #admin-recovery-dr}

Disaster recovery can become an issue if an {{site.data.keyword.cloud_notm}} location experiences a significant failure that includes the potential loss of data. Because the multi-zone region feature is not available across locations, you must wait for IBM to bring a location back online if it becomes unavailable. If underlying data services are compromised by the failure, you must also wait for IBM to restore those data services.

If a catastrophic failure occurs, IBM might not be able to recover data from database backups. In this case, you need to restore your data to return your service instance to its most recent state. You can restore the data to the same or to a different location.

Your disaster recovery plan includes knowing, preserving, and being prepared to restore all data that is maintained on {{site.data.keyword.cloud_notm}}. See [Backing up and restoring data](/docs/watson-assistant?topic=watson-assistant-admin-backup-restore) for information about how to back up your service instances.
