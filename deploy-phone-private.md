---

copyright:
  years: 2023
lastupdated: "2023-08-30"

keywords: directlink, private path, transit gateway, voice integration

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Integrating with phone and Private Path
{: #deploy-phone-private}

[IBM Cloud]{: tag-ibm-cloud}

You can establish {{site.data.keyword.conversationshort}} webhook and voice communication with Private Path instead of a public network. 

Designed for security, performance, and cost-effectiveness, Private Path uses Transit Gateway by way of network address translation (NAT) IP/subnet. Transit Gateway provides private network connectivity across IBM Cloud accounts and currently supports Classic Infrastructure, Direct Link, and virtual private cloud (VPC).

## Setting up Private Path
{: #deploy-phone-private-path}

### Configure Transit Gateway
{: #deploy-phone-private-configure}

1. Go to the IBM Cloud dashboard, and select **Interconnectivity** > **Transit Gateway**.

1. On the **Create** tab:

    - Enter a **name** for your Transit Gateway.
    - Use **default** for the Resource group.

1. Select Local routing or Global routing.

    - If you need to connect Classic Infrastructure or Direct Link to the Transit Gateway, use **Local routing**.
    - If you need to connect a VPC to the Transit Gateway, use **Global routing**.

1. Select a region from the **Choose location** dropdown. The location needs be close to resource for Classic Infrastructure or Direct Link, and where the VPC resides for a VPC.

### Set up your connections
{: #deploy-phone-private-connections}

You can add or edit connections after the Transit Gateway is provisioned. Setup is specific to your network.

#### Network connection
{: #deploy-phone-private-network}

Use Connection 1 to set up the network connection.

1. In the **Network connection** dropdown, select Classic infrastructure, Direct Link, or VPC. 

1. Select **Add new connection in this account** for Connection reach. 

1. Connect your network. 

    - For Classic Infrastructure, enter the **name of your connection**.
    - For Direct Link, select your Direct Link from **Existing direct links**. 
    - For VPC, select a city for **Region**, and select your VPC from **Available connections**. 

#### Watson connection
{: #deploy-phone-private-watson}

Create Connection 2 to add your Watson connection. 

1. Click the **Add connection +** button to create Connection 2.

1. In the **Network connection** dropdown, select **VPC**. 

1. Select **Request connection to a network in another account** for **Connection reach**. 

1. Enter a name for **Connection name**. The Watson team provides the **VPC CRN**. 

1. Click the **Create** button. An **Attached** message appears, if successful.

### Apply prefix filtering
{: #deploy-phone-private-filtering}

You need to apply prefix filtering so relevant subnets are advertised. 

1. Click the menu icon.

1. Select Prefix filtering.

1. Click the **Create prefix filter +** button, and list the subnets that require the connection.

### Watson team approval
{: #deploy-phone-private-approval}

Contact your IBM Watson team to approve the connection creation. 

Webhook and voice connectivity with the Transit Gateway integration is established over NAT IP/subnets that are provided by the Watson team. The NAT IP/subnet is on 192.168.x.x address space. 












