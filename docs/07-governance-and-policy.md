# Governance and Policy

## Overview

Governance ensures that Azure resources are deployed, managed, and operated according to organizational standards.

Without governance, cloud environments often become difficult to manage, expensive, inconsistent, and non-compliant.

Azure Landing Zones use governance controls to enforce standards across subscriptions, resource groups, and workloads.

## Governance Objectives

The primary goals of governance are:

* Standardization
* Security
* Compliance
* Cost Control
* Operational Consistency
* Risk Reduction

## Governance Architecture

Azure governance is typically implemented through:

```text
Management Groups
        |
Azure Policy
        |
Subscriptions
        |
Resources
        |
------------------
|                |
Security      Operations
|                |
Defender     Azure Monitor
PIM          Log Analytics
MFA          Alerts
CA           Update Manager
```

Policies and permissions are inherited throughout the hierarchy.

## Management Groups

Management Groups provide centralized governance for multiple subscriptions.

Benefits:

* Policy inheritance
* RBAC inheritance
* Organizational structure
* Compliance enforcement

Example:

```text
Tenant Root Group
│
├── Platform
│
├── Production
│
├── NonProduction
│
└── Sandbox
```

Policies assigned at higher levels automatically apply to child subscriptions.

## Azure Policy

Azure Policy is the primary governance tool in Azure.

It evaluates resources and ensures compliance with organizational standards.

Policy effects include:

* Audit
* Deny
* Append
* Modify
* DeployIfNotExists

## Example Policies

### Allowed Regions

Restrict resource deployment to approved locations.

Example:

```text
Allowed:
West Europe
North Europe

Denied:
East US
Southeast Asia
```

### Required Tags

Every resource must contain:

```text
Environment
Owner
CostCenter
Application
BusinessUnit
```

### Allowed Resource Types

Example:

```text
Allow:
Virtual Machines
Storage Accounts
Key Vault

Deny:
Unapproved Services
```

### Public IP Restrictions

Example:

```text
Deny:
Public IP creation for virtual machines
```

### Encryption Requirements

Example:

```text
Require:
Disk Encryption
Storage Encryption
TLS 1.2+
```

## Initiative Definitions

Policy initiatives group multiple policies together.

Example:

```text
Security Baseline Initiative
│
├── Require Tags
├── Require Encryption
├── Restrict Regions
├── Restrict Public IPs
└── Enforce Diagnostics
```

Benefits:

* Easier management
* Consistent compliance controls
* Simplified reporting

## Resource Naming Standards

Consistent naming improves administration and troubleshooting.

Example:

### Resource Groups

```text
rg-prod-network-weu
rg-prod-app-weu
rg-dev-app-weu
```

### Virtual Networks

```text
vnet-hub-weu
vnet-prod-app-weu
```

### Virtual Machines

```text
vm-prod-web01
vm-prod-app01
vm-dev-web01
```

### Storage Accounts

```text
stprodlogsweu
stdevbackupweu
```

## Tagging Strategy

Tags provide metadata for resources.

Recommended tags:

| Tag          | Example       |
| ------------ | ------------- |
| Environment  | Production    |
| Owner        | IT Operations |
| CostCenter   | CC100         |
| Application  | ERP           |
| BusinessUnit | Finance       |

Benefits:

* Cost reporting
* Automation
* Resource ownership tracking
* Governance reporting

## Resource Locks

Resource locks prevent accidental changes.

Types:

### Delete Lock

Prevents deletion.

### ReadOnly Lock

Prevents modification.

Example use cases:

* Production databases
* Shared networking resources
* Key Vaults
* Log Analytics Workspaces

## Cost Governance

Cloud governance must include financial controls.

Recommendations:

### Budgets

Create subscription budgets.

Example:

```text
Production Budget:
5000 EUR/month

Development Budget:
1000 EUR/month
```

### Cost Alerts

Generate notifications when thresholds are exceeded.

Examples:

```text
50%
75%
90%
100%
```

### Resource Cleanup

Regularly remove:

* Unused disks
* Unused public IPs
* Expired test environments
* Orphaned resources

## Role-Based Access Control

Governance includes permission management.

Recommendations:

* Use groups instead of individual assignments
* Minimize Owner role assignments
* Apply least privilege
* Review permissions regularly

Example:

```text
Platform Team
  -> Contributor

Security Team
  -> Security Administrator

Audit Team
  -> Reader
```

## Compliance Management

Governance helps support compliance frameworks.

Examples:

* ISO 27001
* CIS Benchmark
* NIST
* GDPR

Microsoft Defender for Cloud provides compliance dashboards and recommendations.

## Monitoring Governance Compliance

Compliance should be monitored continuously.

Tools:

* Azure Policy Compliance
* Defender for Cloud
* Azure Monitor
* Log Analytics

Key metrics:

* Policy compliance percentage
* Non-compliant resources
* Resource drift
* Cost anomalies

## Example Governance Baseline

```text
Management Groups
├── Platform
├── Production
├── NonProduction
└── Sandbox

Policies
├── Allowed Regions
├── Required Tags
├── Encryption Required
├── No Public IPs
└── Diagnostics Enabled

RBAC
├── Least Privilege
├── Group Assignments
└── PIM

Cost Controls
├── Budgets
├── Alerts
└── Reporting
```

## Design Recommendations

* Implement Management Groups early.
* Use Azure Policy extensively.
* Enforce resource tagging.
* Define naming standards before deployment.
* Restrict resource locations.
* Apply RBAC consistently.
* Monitor policy compliance regularly.
* Create budgets and cost alerts.
* Protect critical resources with locks.
* Use policy initiatives whenever possible.

## Conclusion

Governance is the framework that ensures Azure resources remain secure, compliant, standardized, and cost-effective over time.

Management Groups, Azure Policy, RBAC, tagging, naming standards, and cost controls work together to provide a scalable governance model for enterprise Azure environments.
