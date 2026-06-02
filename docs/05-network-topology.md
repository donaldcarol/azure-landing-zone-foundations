# Network Topology

## Overview

Network topology is one of the most important components of an Azure Landing Zone.

A well-designed network provides secure connectivity between Azure workloads, on-premises environments, internet-facing services, management tools, and shared platform services.

In an enterprise Azure environment, the recommended model is usually based on a Hub-Spoke architecture.

## Hub-Spoke Model

The Hub-Spoke model separates shared network services from application workloads.

```text
Internet
   |
Azure Front Door / Public Access Layer
   |
Application Gateway / Web Application Firewall
   |
Hub Virtual Network
   |
Azure Firewall / Routing / DNS / Bastion / VPN
   |
Spoke Virtual Networks
   |-- Production Workloads
   |-- Development Workloads
   |-- Shared Services
   |-- Sandbox Workloads
```

## Hub Virtual Network

The Hub VNet contains centralized networking and security services.

Typical components:

* Azure Firewall
* VPN Gateway
* ExpressRoute Gateway
* Azure Bastion
* Private DNS Zones
* DNS Forwarders
* Network Virtual Appliances
* Shared connectivity services

The Hub should not host normal business workloads. Its purpose is to provide secure and controlled connectivity.

## Spoke Virtual Networks

Spoke VNets host application workloads.

Examples:

```text
vnet-prod-apps
vnet-dev-apps
vnet-shared-services
vnet-sandbox
```

Each spoke can have its own subnets, NSGs, route tables, and workload-specific controls.

Spokes are connected to the Hub using VNet Peering.

## Why Not Full Mesh?

A full mesh design means that every VNet is connected directly to every other VNet.

This becomes difficult to manage as the environment grows.

Problems with full mesh:

* Too many peerings
* Harder routing control
* Inconsistent security inspection
* Difficult troubleshooting
* Higher operational complexity

Hub-Spoke is easier to govern because traffic can be centralized through the Hub.

## Traffic Flow

Typical traffic flows:

### Internet Inbound Traffic

```text
Internet
   |
Azure Front Door
   |
Application Gateway with WAF
   |
Application Subnet
   |
Backend Workload
```

This model provides global entry point, web protection, SSL termination, and controlled routing.

### Outbound Internet Traffic

```text
Spoke VNet
   |
Route Table
   |
Azure Firewall
   |
Internet
```

Outbound traffic should be inspected and controlled through Azure Firewall or another approved security appliance.

### On-Premises Connectivity

```text
On-Premises Network
   |
VPN / ExpressRoute
   |
Hub VNet
   |
Spoke VNets
```

On-premises connectivity should terminate in the Hub VNet, not directly into each workload VNet.

## Azure Firewall

Azure Firewall is commonly placed in the Hub VNet.

It provides:

* Centralized traffic inspection
* Application rules
* Network rules
* DNAT rules
* Logging
* Threat intelligence integration

Spoke VNets can use route tables to send traffic through the firewall.

Example:

```text
0.0.0.0/0 -> Azure Firewall private IP
```

## Network Security Groups

NSGs provide subnet-level or NIC-level traffic filtering.

Recommended approach:

* Apply NSGs at subnet level.
* Keep rules simple and readable.
* Avoid unnecessary Any-to-Any rules.
* Use Application Security Groups where useful.
* Deny direct inbound access from the internet.

Example:

```text
Allow HTTP/HTTPS from Application Gateway subnet
Deny direct internet access to backend servers
Allow management traffic only from Bastion or admin subnet
```

## Azure Bastion

Azure Bastion provides secure RDP and SSH access without exposing public IP addresses on virtual machines.

Recommended design:

```text
Admin User
   |
Azure Portal
   |
Azure Bastion
   |
Private IP of VM
```

Virtual machines should not have public IP addresses unless there is a very specific business requirement.

## Private Endpoints

Private Endpoints allow Azure PaaS services to be accessed through private IP addresses.

Common use cases:

* Azure Storage
* Azure SQL Database
* Key Vault
* App Services
* Container Registry

Example:

```text
Spoke VNet
   |
Private Endpoint
   |
Azure SQL Database
```

This avoids exposing services to the public internet.

## DNS Design

DNS is critical in a Hub-Spoke architecture, especially when using Private Endpoints.

Typical components:

* Private DNS Zones
* DNS Forwarders
* On-premises DNS integration
* Azure-provided DNS
* Conditional forwarding

Example:

```text
privatelink.database.windows.net
privatelink.blob.core.windows.net
privatelink.vaultcore.azure.net
```

For hybrid environments, DNS resolution must work both from Azure to on-premises and from on-premises to Azure.

## Subnet Design

A clean subnet design improves security and operations.

Example Hub VNet:

```text
vnet-hub-weu
  |
  |-- AzureFirewallSubnet
  |-- AzureBastionSubnet
  |-- GatewaySubnet
  |-- snet-dns
  |-- snet-management
```

Example Spoke VNet:

```text
vnet-prod-app-weu
  |
  |-- snet-web
  |-- snet-app
  |-- snet-data
  |-- snet-private-endpoints
```

## Public Access Layer

For internet-facing applications, a layered model is recommended.

```text
Internet
   |
Azure Front Door
   |
Application Gateway WAF
   |
Backend Application
```

Azure Front Door provides:

* Global entry point
* Global load balancing
* CDN capabilities
* TLS termination
* Web Application Firewall

Application Gateway provides:

* Regional layer 7 load balancing
* Path-based routing
* Internal application publishing
* WAF protection

## Design Recommendations

* Use Hub-Spoke for enterprise environments.
* Place shared connectivity services in the Hub.
* Place workloads in Spoke VNets.
* Avoid public IPs on virtual machines.
* Use Azure Bastion for administrative access.
* Use Private Endpoints for PaaS services.
* Centralize outbound traffic through Azure Firewall.
* Use NSGs at subnet level.
* Plan DNS carefully before deploying Private Endpoints.
* Separate production and non-production networks.
* Use naming conventions for VNets, subnets, route tables, and NSGs.

## Example Naming Convention

```text
vnet-hub-weu
vnet-prod-app-weu
vnet-dev-app-weu

snet-web
snet-app
snet-data
snet-private-endpoints

rt-prod-default
nsg-prod-web
pip-fw-weu
fw-hub-weu
```

## Example Landing Zone Network Design

```text
Azure Tenant
   |
Management Groups
   |
Connectivity Subscription
   |
Hub VNet
   |
   |-- Azure Firewall
   |-- VPN / ExpressRoute Gateway
   |-- Bastion
   |-- Private DNS Zones
   |
Production Subscription
   |
   |-- Production Spoke VNet
       |-- Web Subnet
       |-- App Subnet
       |-- Data Subnet
       |-- Private Endpoints Subnet

Development Subscription
   |
   |-- Development Spoke VNet

Sandbox Subscription
   |
   |-- Sandbox Spoke VNet
```

## Conclusion

The network topology of an Azure Landing Zone should provide secure, scalable, and manageable connectivity.

The Hub-Spoke model allows centralized control of routing, firewalling, DNS, hybrid connectivity, and management access, while keeping application workloads isolated in separate spoke networks.

This approach supports enterprise governance, security, and future growth.
