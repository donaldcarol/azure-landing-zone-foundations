# Subscription Strategy

## Overview

Azure subscriptions provide logical, administrative, and billing boundaries within an Azure tenant.

A well-designed subscription strategy improves security, governance, cost management, and operational efficiency.

## Why Multiple Subscriptions?

Using a single subscription for all workloads creates challenges:

* Difficult cost allocation
* Limited delegation options
* Increased operational risk
* Complex governance

Enterprise environments typically use multiple subscriptions.

## Recommended Subscription Model

### Platform Subscriptions

```text
Identity Subscription
Connectivity Subscription
Management Subscription
```

### Workload Subscriptions

```text
Production Subscription
Development Subscription
Testing Subscription
Sandbox Subscription
```

## Identity Subscription

Contains:

* Microsoft Entra ID integrations
* Domain Services
* Identity-related services

Purpose:

* Centralized identity management
* Reduced attack surface
* Administrative separation

## Connectivity Subscription

Contains:

* Hub VNet
* Azure Firewall
* VPN Gateway
* ExpressRoute Gateway
* Bastion

Purpose:

* Shared networking services

## Management Subscription

Contains:

* Log Analytics Workspace
* Azure Monitor
* Update Manager
* Automation Accounts
* Recovery Services Vault

Purpose:

* Centralized operations management

## Production vs Non-Production

Production workloads should always be isolated from development and testing environments.

Benefits:

* Security separation
* Independent RBAC
* Easier cost tracking
* Reduced operational risk

## Sandbox Subscription

Used for:

* Training
* Proof of Concepts
* Experimental deployments

Sandbox subscriptions typically have fewer permissions and stricter spending limits.

## Design Recommendations

* Separate production and non-production workloads.
* Separate shared platform services.
* Implement subscription-level RBAC.
* Apply Azure Policies consistently.
* Monitor subscription spending.
