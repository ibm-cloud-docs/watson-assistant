---

copyright:
  years: 2015, 2023
lastupdated: "2023-11-30"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

[{{site.data.keyword.icp4dfull_notm}}]{: tag-cp4d}

# Installing {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull_notm}}
{: #install-data}

Learn how to install {{site.data.keyword.assistant_classic_short}} for {{site.data.keyword.icp4dfull}}.
{: shortdesc}

The {{site.data.keyword.icp4dfull_notm}} environment is a Kubernetes-based container platform that can help you quickly modernize and automate workloads that are associated with the applications and services you use. You can develop and deploy on your own infrastructure and in your data center which helps to mitigate risk and minimize vulnerabilities.

The installation process differs depending on the version you are installing. The following table shows the available versions.

| Version |  Cluster | Installation instructions |
| --- | --- | --- |

| 4.7.4 | {{site.data.keyword.icp4dfull_notm}} 4.7.x | [Installing 4.7.4](https://www.ibm.com/docs/SSQNUZ_4.7.x/svc-assistant/assistant-svc-install.html){: external} |
| 4.7.2 | {{site.data.keyword.icp4dfull_notm}} 4.7.x | [Installing 4.7.2](https://www.ibm.com/docs/SSQNUZ_4.7.x/svc-assistant/assistant-svc-install.html){: external} |
| 4.7.1 | {{site.data.keyword.icp4dfull_notm}} 4.7.x | [Installing 4.7.1](https://www.ibm.com/docs/SSQNUZ_4.7.x/svc-assistant/assistant-svc-install.html){: external} |
| 4.7.0 | {{site.data.keyword.icp4dfull_notm}} 4.7.x | [Installing 4.7.0](https://www.ibm.com/docs/SSQNUZ_4.7.x/svc-assistant/assistant-svc-install.html){: external} |
| 4.6.5 | {{site.data.keyword.icp4dfull_notm}} 4.6.x | [Installing 4.6.5](https://www.ibm.com/docs/SSQNUZ_4.6.x/svc-assistant/assistant-svc-install.html){: external} |
| 4.6.3 | {{site.data.keyword.icp4dfull_notm}} 4.6.x | [Installing 4.6.3](https://www.ibm.com/docs/SSQNUZ_4.6.x/svc-assistant/assistant-svc-install.html){: external} |
| 4.6.2 | {{site.data.keyword.icp4dfull_notm}} 4.6.x | [Installing 4.6.2](https://www.ibm.com/docs/SSQNUZ_4.6.x/svc-assistant/assistant-svc-install.html){: external} |
| 4.6.0 | {{site.data.keyword.icp4dfull_notm}} 4.6.x | [Installing 4.6.0](https://www.ibm.com/docs/SSQNUZ_4.6.x/svc-assistant/assistant-svc-install.html){: external} |
| 4.5.3 | {{site.data.keyword.icp4dfull_notm}} 4.5.x | [Installing 4.5.3](https://www.ibm.com/docs/SSQNUZ_4.5.x/svc-assistant/assistant-svc-install.html){: external} |
| 4.5.1 | {{site.data.keyword.icp4dfull_notm}} 4.5.x | [Installing 4.5.1](https://www.ibm.com/docs/SSQNUZ_4.5.x/svc-assistant/assistant-svc-install.html){: external} |
| 4.5.0 | {{site.data.keyword.icp4dfull_notm}} 4.5.x | [Installing 4.5.0](https://www.ibm.com/docs/en/SSQNUZ_4.5.x/archives/refresh-0/CP-Data-4.5.x-R0-PDF5-Installing.pdf){: external} |
| 4.0.8 | {{site.data.keyword.icp4dfull_notm}} 4.0.x | [Installing 4.0.8](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=assistant-installing-watson){: external} |
| 4.0.7 | {{site.data.keyword.icp4dfull_notm}} 4.0.x | [Installing 4.0.7](https://www.ibm.com/docs/en/SSQNUZ_4.0/archives/refresh-7/CP-Data-4.0-R7-PDF5-Installing.pdf){: external} |
| 4.0.6 | {{site.data.keyword.icp4dfull_notm}} 4.0.x | [Installing 4.0.6](https://www.ibm.com/docs/en/SSQNUZ_4.0/archives/refresh-6/CP-Data-4.0-R6-PDF5-Installing.pdf){: external} |
| 4.0.5 | {{site.data.keyword.icp4dfull_notm}} 4.0.x | [Installing 4.0.5](https://www.ibm.com/docs/en/SSQNUZ_4.0/archives/refresh-5/CP-Data-4.0-R5-PDF5-Installing.pdf){: external} |
| 4.0.4 | {{site.data.keyword.icp4dfull_notm}} 4.0.x | [Installing 4.0.4](https://www.ibm.com/docs/en/SSQNUZ_4.0/archives/refresh-4/CP-Data-4.0-R4-PDF5-Installing.pdf){: external} |
| 4.0.2 | {{site.data.keyword.icp4dfull_notm}} 4.0.x | [Installing 4.0.2](https://www.ibm.com/docs/en/SSQNUZ_4.0/archives/refresh-2/CP-Data-4.0-R2-PDF5-Installing.pdf){: external} |
| 4.0.0 | {{site.data.keyword.icp4dfull_notm}} 4.0.x | [Installing 4.0.0](https://www.ibm.com/docs/en/SSQNUZ_4.0/archives/refresh-0/CP-Data-4.0-R0-PDF5-Installing.pdf){: external} |
| 1.5.0 | {{site.data.keyword.icp4dfull_notm}} 3.0.1 or 3.5 | [Installing 1.5.0](https://www.ibm.com/docs/en/cloud-paks/cp-data/3.5.0?topic=service-installing-watson-assistant){: external} |
{: caption="Available versions" caption-side="top"}

## Support matrix
{: #install-support-matrix}

The following table describes which versions of {{site.data.keyword.assistant_classic_short}} are supported on which versions of {{site.data.keyword.icp4dfull_notm}} and Red Hat OpenShift.

| {{site.data.keyword.assistant_classic_short}} version | {{site.data.keyword.icp4dfull_notm}} version | Red Hat OpenShift version |
| --- | --- | --- |

| 4.7.4 | 4.7.x | 4.12 |
| 4.7.4 | 4.7.x | 4.10 |
| 4.7.2 | 4.7.x | 4.12 |
| 4.7.2 | 4.7.x | 4.10 |
| 4.7.1 | 4.7.x | 4.12 |
| 4.7.1 | 4.7.x | 4.10 |
| 4.7.0 | 4.7.x | 4.12 |
| 4.7.0 | 4.7.x | 4.10 |
| 4.6.5 | 4.6.x | 4.12 |
| 4.6.5 | 4.6.x | 4.10 |
| 4.6.3 | 4.6.x | 4.10 |
| 4.6.2 | 4.6.x | 4.10 |
| 4.6.2 | 4.6.x | 4.8 |
| 4.6.0 | 4.6.x | 4.10 |
| 4.6.0 | 4.6.x | 4.8 |
| 4.5.3 | 4.5.x | 4.10 |
| 4.5.3 | 4.5.x | 4.8 |
| 4.5.3 | 4.5.x | 4.6 |
| 4.5.1 | 4.5.x | 4.10 |
| 4.5.1 | 4.5.x | 4.8 |
| 4.5.1 | 4.5.x | 4.6 |
| 4.5.0 | 4.5.x | 4.10 |
| 4.5.0 | 4.5.x | 4.8 |
| 4.5.0 | 4.5.x | 4.6 |
| 4.0.8 | 4.0.x | 4.8 |
| 4.0.8 | 4.0.x | 4.6 |
| 4.0.7 | 4.0.x | 4.8 |
| 4.0.7 | 4.0.x | 4.6 |
| 4.0.6 | 4.0.x | 4.8 |
| 4.0.6 | 4.0.x | 4.6 |
| 4.0.5 | 4.0.x | 4.8 |
| 4.0.5 | 4.0.x | 4.6 |
| 4.0.4 | 4.0.x | 4.8 |
| 4.0.4 | 4.0.x | 4.6 |
| 4.0.2 | 4.0.x | 4.8 |
| 4.0.2 | 4.0.x | 4.6 |
| 4.0.0 | 4.0.x | 4.6 |
| 1.5.0 | 3.5 | 4.6 |
| 1.5.0 | 3.5 | 3.11 |
| 1.5.0 | 3.0.1 | 4.5 |
| 1.5.0 | 3.0.1 | 3.11 |
{: caption="Support matrix" caption-side="top"}
