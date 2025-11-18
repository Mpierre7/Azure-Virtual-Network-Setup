 Azure Virtual Network Setup (Enterprise Network Simulation)

This project simulates a secure enterprise-grade network environment inside Microsoft Azure, using Virtual Networks (VNets), Subnets, and Network Security Groups (NSGs).


 Project Overview


A hub-style VNet (vnet-enterprise-hub)

Five subnets (Frontend, App, Database, Management, GatewaySubnet)

Isolated security zones controlled by Network Security Groups

Custom NSG rules simulating real enterprise access flows

Virtual Machines for testing

A GatewaySubnet to support VPN gateway design (without deploying the paid resource)


 Architecture Diagram
                           ┌───────────────────────────────┐
                           │       Azure Subscription       │
                           └───────────────────────────────┘
                                      │
                                      ▼
                    ┌──────────────────────────────────────────┐
                    │         vnet-enterprise-hub              │
                    │            (10.0.0.0/16)                 │
                    ├──────────────────────────────────────────┤
                    │  snet-frontend (10.0.1.0/24)             │
                    │   • nsg-frontend                         │
                    │   • vm-frontend-01                       │
                    ├──────────────────────────────────────────┤
                    │  snet-app (10.0.2.0/24)                  │
                    │   • nsg-app                              │
                    ├──────────────────────────────────────────┤
                    │  snet-db (10.0.3.0/24)                   │
                    │   • nsg-db                               │
                    ├──────────────────────────────────────────┤
                    │  snet-management (10.0.4.0/24)           │
                    │   • nsg-management                       │
                    ├──────────────────────────────────────────┤
                    │  GatewaySubnet (10.0.255.0/27)           │
                    │   (VPN Gateway placeholder)              │
                    └──────────────────────────────────────────┘



Implementation Steps
Step 1 — Resource Group

Created a dedicated resource group:
rg-enterprise-network-lab

Step 2 — Virtual Network

Created the hub VNet:
vnet-enterprise-hub
Address space: 10.0.0.0/16

Step 3 — Subnets

Created all subnets:

Subnet Name	Address Range	Purpose
snet-frontend	10.0.1.0/24	Public-facing workloads
snet-app	10.0.2.0/24	Internal app services
snet-db	10.0.3.0/24	Database servers
snet-management	10.0.4.0/24	Admin / management nodes
GatewaySubnet	10.0.255.0/27	Reserved for VPN gateway
Step 4 — Network Security Groups

Created NSGs:

nsg-frontend

nsg-app

nsg-db

nsg-management

Step 5 — NSG Rules

Configured rules such as:

Frontend NSG

Allow RDP from my home IP

Allow HTTP/HTTPS from internet

App NSG

Allow traffic only from frontend subnet

Database NSG

Allow SQL only from app subnet

Management NSG

Allow RDP/administrative access only from home IP

Step 6 — NSG Association

Linked NSGs to their corresponding subnets.

Step 7 — Virtual Machines

Deployed test VMs:

vm-frontend-01 → snet-frontend

vm-app-01 (optional internal-only server)

Used for internal routing and subnet validation.

--
Author: Mayedson Pierre
