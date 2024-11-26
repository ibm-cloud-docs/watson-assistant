---

copyright:
  years: 2015, 2024
lastupdated: "2024-11-26"

subcollection: watson-assistant

content-type: maintenance

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.conversationshort}} planned maintenance
{: #maintenance}

{{site.data.keyword.conversationshort}} maintenance is planned for the period of 7 December 2024 through 23 December 2024.

The maintenance will be performed only during the weekends, specifically on the days 7-8, 14-15, and 21-22 in December.

The following multi-tenant plans are impacted:

- **Standard**
- **Lite**
- **Trial**
- **Plus**
- **Enterprise**

This maintenance does not affect **Premium** or **Enterprise Data Isolated** plans.

During the specified period, you might experience the following limitations:

**Not Functional in Read-Only mode**

- You can't create, update, or delete Assistants.
- You can't create, update, or delete Skills.
- You can't create, update, or delete Integrations.
- You can't create, update, or delete Workspaces.
- You can't assign Skills to Assistants.
- You can't assign Skill Versions to Environments.
- You can't make changes or invoke "write" calls to any resources.

**Functional in Read-Only mode**

- **Runtime calls**: the `/message` endpoints for both API V1 and API V2 remain unaffected.
- **Improve or Analytics capabilities**: `/logs` and **Recommendations in Assistant Tooling** remain unaffected.
- **Assistants**, **Skills**, **Skill versions**, **Workspaces**, **Integrations** can be retrieved through the API or Assistant Tooling.
- Retrieval or read calls to the resources remain unaffected.
