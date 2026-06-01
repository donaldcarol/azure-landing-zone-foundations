# Identity and Access Management

## Overview

Identity is the primary security boundary in Microsoft Azure.

A secure Azure Landing Zone relies on centralized identity management, strong authentication, least-privilege access, and continuous governance.

## Microsoft Entra ID

Microsoft Entra ID provides:

* Authentication
* Authorization
* Identity governance
* Conditional Access
* Single Sign-On (SSO)

All Azure resources depend on Microsoft Entra ID for access control.

## Role-Based Access Control (RBAC)

RBAC provides granular permissions to Azure resources.

Common roles:

| Role                      | Purpose            |
| ------------------------- | ------------------ |
| Owner                     | Full control       |
| Contributor               | Manage resources   |
| Reader                    | View-only access   |
| User Access Administrator | Manage permissions |

## Principle of Least Privilege

Users should receive only the permissions required to perform their tasks.

Benefits:

* Reduced attack surface
* Improved compliance
* Better operational control

## Multi-Factor Authentication

MFA should be mandatory for:

* Administrators
* Privileged users
* Remote access users

Benefits:

* Protection against password compromise
* Reduced identity-based attacks

## Conditional Access

Conditional Access enables policy-based access decisions.

Examples:

* Require MFA outside trusted locations
* Block legacy authentication
* Restrict access from unmanaged devices

## Privileged Identity Management (PIM)

PIM provides:

* Just-In-Time administration
* Approval workflows
* Time-limited role activation
* Audit trails

## Managed Identities

Managed Identities eliminate the need to store credentials in applications.

Types:

### System Assigned

Lifecycle tied to a resource.

### User Assigned

Reusable across multiple resources.

## Service Principals

Applications authenticate to Azure using Service Principals.

Common use cases:

* CI/CD pipelines
* Automation
* Infrastructure deployment

## Break Glass Accounts

Emergency administrator accounts should:

* Exclude Conditional Access policies
* Use strong passwords
* Be monitored and tested regularly

## Design Recommendations

* Enable MFA for all privileged accounts.
* Use Conditional Access.
* Implement PIM.
* Prefer Managed Identities over secrets.
* Minimize Global Administrator usage.
* Maintain emergency access accounts.
