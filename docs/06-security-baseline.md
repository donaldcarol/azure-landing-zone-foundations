# Security Baseline

## Overview

Security is a foundational principle of every Azure Landing Zone.

A secure Azure environment should implement layered security controls across identity, networking, workloads, data, and operations.

The goal is to reduce the attack surface, enforce governance, detect threats, and respond to security incidents effectively.

## Security Principles

The security baseline is built around the following principles:

* Zero Trust
* Least Privilege
* Defense in Depth
* Assume Breach
* Continuous Monitoring
* Secure by Default

## Zero Trust Model

Azure Landing Zones should follow the Zero Trust approach.

Core principles:

* Verify explicitly
* Use least privilege access
* Assume breach

Every access request should be authenticated, authorized, and continuously validated.

## Identity Security

Identity is the primary security boundary in Azure.

### Microsoft Entra ID

All users, applications, and services should authenticate through Microsoft Entra ID.

### Multi-Factor Authentication

MFA should be mandatory for:

* Administrators
* Privileged users
* Remote access users

Benefits:

* Reduced account compromise risk
* Protection against password attacks

### Conditional Access

Recommended policies:

* Require MFA
* Block legacy authentication
* Restrict access from risky locations
* Require compliant devices

### Privileged Identity Management

Use PIM for privileged roles.

Benefits:

* Just-In-Time access
* Approval workflows
* Reduced standing privileges
* Audit trail

### Break Glass Accounts

Maintain emergency administrator accounts.

Requirements:

* Strong passwords
* Separate monitoring
* Excluded from Conditional Access
* Tested regularly

## Access Control

Role-Based Access Control (RBAC) should be used throughout the environment.

Recommended practices:

* Assign permissions to groups
* Minimize Owner assignments
* Use custom roles only when necessary
* Review permissions regularly

Typical role assignments:

```text
Platform Team -> Contributor
Security Team -> Security Admin
Auditors -> Reader
Application Team -> Contributor
```

## Network Security

Network controls provide an additional security layer.

### Network Security Groups

Use NSGs to control:

* Inbound traffic
* Outbound traffic
* Application segmentation

### Azure Firewall

Centralize traffic inspection through Azure Firewall.

Capabilities:

* Application filtering
* Network filtering
* Threat intelligence
* Logging

### Bastion

Use Azure Bastion for administrative access.

Avoid exposing:

* RDP
* SSH

directly to the internet.

### Private Endpoints

Use Private Endpoints for:

* Storage Accounts
* Azure SQL
* Key Vault
* App Services

This reduces public exposure.

## Data Protection

Data must be protected both at rest and in transit.

### Encryption at Rest

Azure services provide encryption by default.

Examples:

* Managed Disks
* Azure Storage
* Azure SQL Database

### Encryption in Transit

Use TLS for all communications.

Recommendations:

* TLS 1.2 or higher
* HTTPS everywhere
* Disable legacy protocols

### Key Management

Use Azure Key Vault to store:

* Secrets
* Certificates
* Encryption keys

Benefits:

* Centralized management
* Auditability
* Reduced credential exposure

## Compute Security

Virtual machines should follow secure configuration standards.

Recommendations:

* Remove unnecessary software
* Apply security updates
* Disable unused services
* Use Defender for Endpoint
* Restrict local administrator access

## Azure Policy

Azure Policy helps enforce security standards.

Example policies:

* Require resource tags
* Require managed disks
* Restrict allowed locations
* Require encryption
* Deny public IP creation

Example:

```text
Deny:
Public IP addresses on virtual machines
```

## Defender for Cloud

Microsoft Defender for Cloud provides:

* Secure Score
* Security recommendations
* Vulnerability assessment
* Threat detection
* Regulatory compliance tracking

Recommended approach:

* Review Secure Score regularly
* Remediate high-risk findings first
* Enable Defender plans where appropriate

## Logging and Monitoring

Security controls must be monitored continuously.

### Azure Monitor

Collect:

* Metrics
* Alerts
* Diagnostic logs

### Log Analytics Workspace

Centralized log collection.

Examples:

* Activity Logs
* Sign-In Logs
* Security Logs
* VM Logs

### Alerting

Create alerts for:

* Failed sign-ins
* Privileged role activations
* VM availability issues
* Firewall events
* Security incidents

## Vulnerability Management

Regular vulnerability assessments should be performed.

Sources:

* Defender for Cloud
* Operating system scans
* Third-party scanners

Prioritization:

```text
Critical
High
Medium
Low
```

Critical vulnerabilities should be remediated immediately.

## Backup and Recovery

Security also includes recoverability.

Recommended services:

* Azure Backup
* Recovery Services Vault
* Azure Site Recovery

Protect:

* Virtual Machines
* Databases
* File Shares

## Security Operations

A mature Azure environment should include:

* Security monitoring
* Incident response procedures
* Change management
* Regular access reviews
* Security assessments

## Example Security Baseline

```text
Identity
├── MFA
├── Conditional Access
├── PIM
└── Break Glass Accounts

Network
├── NSGs
├── Azure Firewall
├── Bastion
└── Private Endpoints

Data
├── Encryption
├── TLS
└── Key Vault

Operations
├── Defender for Cloud
├── Azure Monitor
├── Log Analytics
└── Azure Policy
```

## Design Recommendations

* Enable MFA for all administrators.
* Use Conditional Access policies.
* Implement PIM for privileged roles.
* Prefer Managed Identities over secrets.
* Use Azure Firewall for centralized traffic control.
* Deploy Bastion instead of public management ports.
* Use Private Endpoints whenever possible.
* Store secrets in Key Vault.
* Enable Defender for Cloud.
* Monitor Secure Score regularly.
* Apply Azure Policy consistently.
* Maintain tested backup and recovery procedures.

## Conclusion

Security in an Azure Landing Zone is implemented through multiple layers of protection covering identity, networking, data, workloads, and operations.

A combination of Microsoft Entra ID, Azure Policy, Defender for Cloud, Azure Firewall, Key Vault, and continuous monitoring provides a strong security foundation for enterprise Azure environments.
