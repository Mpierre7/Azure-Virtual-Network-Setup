Azure Virtual Network — Setup Steps


Step 1 — Sign in to Azure Portal

Logged into the Azure Portal to begin the deployment.
URL: https://portal.azure.com

 Screenshot

![Azure Portal Home](screenshots/01-azure-portal-home.png)


 Step 2 — Create Resource Group

Created a Resource Group to organize all infrastructure components:

Name: rg-enterprise-network-lab

Region: (Your preferred region)

Screenshot

![Resource Group](screenshots/02-rg-enterprise-network-lab.png)

Step 3 — Create the Virtual Network + Subnets

Created a Virtual Network:

VNet Name: vnet-enterprise-hub

Address Space: 10.0.0.0/16

Configured subnets:

Subnet Name	Address Range
snet-frontend	10.0.1.0/24
snet-app	10.0.2.0/24
snet-db	10.0.3.0/24
snet-management	10.0.4.0/24
GatewaySubnet	10.0.255.0/27
 Screenshot

![VNet Subnets](screenshots/03-vnet-subnets.png)



Step 4 — Create Network Security Groups

Created NSGs to enforce network segmentation:

nsg-frontend

nsg-app

nsg-db

nsg-management

 Screenshot

![NSG List](screenshots/04-nsg-list.png)



Step 5 — Configure NSG Inbound Rules

Added custom rules to simulate realistic enterprise network traffic:

Restrict RDP to my home IP

Allow frontend → app

Allow app → database

Default deny all other inbound traffic

 Screenshot

![NSG Rules Example](screenshots/05-nsg-rules-example.png)



Step 6 — Associate NSGs to Subnets

Mapped each subnet to the correct NSG:

Subnet	Assigned NSG
snet-frontend	nsg-frontend
snet-app	nsg-app
snet-db	nsg-db
snet-management	nsg-management
 Screenshot

![Subnet NSG Association](screenshots/06-subnets-with-nsgs.png)



Step 7 — Deploy Virtual Machines

Created test VMs to validate that the subnets and NSGs function correctly:
vm-app-01 → snet-app
Screenshot
![VM List](screenshots/07-vm-list.png)

