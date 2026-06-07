# Prerequisites and Licensing

## Overview

Before designing and implementing an Azure Landing Zone, organizations should assess licensing requirements, subscription models, compliance obligations, and budget constraints.

Many Azure features depend on specific Microsoft licenses. Understanding these dependencies early helps avoid architectural limitations later in the project.

## Assessment Areas

Before implementation, the following areas should be evaluated:

* Business Requirements
* Compliance Requirements
* Security Requirements
* Licensing Requirements
* Budget Constraints
* Operational Model

## Azure Subscription Models

Azure services can be consumed through different purchasing models.

### Pay-As-You-Go (PAYG)

Suitable for:

* Small organizations
* Laboratories
* Proof of Concepts
* Development environments

Advantages:

* No long-term commitment
* Flexible consumption
* Simple onboarding

### Cloud Solution Provider (CSP)

Suitable for:

* Small and medium businesses
* Organizations working with Microsoft partners

Advantages:

* Simplified billing
* Partner support
* Managed services opportunities

### Enterprise Agreement (EA)

Suitable for:

* Large organizations
* Government institutions
* Enterprises with significant Azure consumption

Advantages:

* Centralized purchasing
* Enterprise governance
* Volume discounts

## Microsoft Entra Licensing

Many identity and security features depend on Entra licensing.

### Microsoft Entra ID Free

Provides:

* User and group management
* Basic authentication
* Single Sign-On
* Basic security controls

Suitable for:

* Small environments
* Basic Azure deployments

### Microsoft Entra ID P1

Adds:

* Conditional Access
* Dynamic Groups
* Group-Based Licensing
* Self-Service Password Reset
* Advanced administration features

Recommended for most organizations.

### Microsoft Entra ID P2

Adds:

* Privileged Identity Management (PIM)
* Identity Protection
* Access Reviews
* Entitlement Management
* Risk-Based Access Controls

Recommended for enterprise environments.

## Identity Feature Comparison

| Feature                | Free  | P1  | P2  |
| ---------------------- | ----- | --- | --- |
| MFA                    | Basic | Yes | Yes |
| Conditional Access     | No    | Yes | Yes |
| Dynamic Groups         | No    | Yes | Yes |
| Group-Based Licensing  | No    | Yes | Yes |
| PIM                    | No    | No  | Yes |
| Identity Protection    | No    | No  | Yes |
| Access Reviews         | No    | No  | Yes |
| Entitlement Management | No    | No  | Yes |

## Microsoft 365 Licensing

Azure Landing Zones often integrate with Microsoft 365 services.

### Microsoft 365 Business Premium

Suitable for:

* Small and medium businesses

Includes:

* Microsoft 365
* Intune
* Basic security features
* Defender for Business

### Microsoft 365 E3

Suitable for:

* Medium and large organizations

Includes:

* Enterprise productivity services
* Intune
* Advanced compliance features

### Microsoft 365 E5

Suitable for:

* Enterprise organizations

Includes:

* Advanced security
* Advanced compliance
* Defender suite integration
* Advanced analytics

## Endpoint Management

For organizations using Intune:

Recommended features:

* Device Enrollment
* Compliance Policies
* Configuration Profiles
* Application Management
* Autopilot

Recommended licensing:

```text
Business Premium
or
Microsoft 365 E3
or
Microsoft 365 E5
```

## Microsoft Defender Licensing

Microsoft Defender products are licensed separately and should be evaluated carefully.

### Defender for Cloud

Provides:

* Secure Score
* Security Recommendations
* Vulnerability Assessment
* Regulatory Compliance
* Threat Protection

Available plans include:

```text
Defender CSPM
Defender for Servers
Defender for SQL
Defender for Storage
Defender for Containers
Defender for Key Vault
Defender for App Service
```

Organizations should enable only the plans required by their workloads.

### Defender for Endpoint

Provides:

* Endpoint Detection and Response (EDR)
* Threat Hunting
* Vulnerability Management
* Attack Surface Reduction

Commonly included in:

```text
Microsoft 365 E5
```

or purchased separately.

### Defender for Identity

Provides:

* Active Directory threat detection
* Identity attack monitoring
* Lateral movement detection

Recommended for hybrid environments.

### Defender for Office 365

Provides:

* Email protection
* Safe Attachments
* Safe Links
* Anti-phishing controls

## Monitoring and Security Operations

Additional services may be required.

### Microsoft Sentinel

Provides:

* SIEM
* SOAR
* Threat Investigation
* Security Analytics

Recommended for organizations with dedicated security operations teams.

## Typical Licensing Recommendations

### Small Organization

Example:

```text
50 Users

Microsoft 365 Business Premium
Defender for Cloud (selected workloads)
```

### Medium Organization

Example:

```text
500 Users

Microsoft 365 E3
Entra ID P1
Intune
Defender for Servers
```

### Enterprise Organization

Example:

```text
5000+ Users

Microsoft 365 E5
Entra ID P2
PIM
Identity Protection
Defender Suite
Microsoft Sentinel
```

## Budget Planning

Licensing decisions should align with business requirements.

Consider:

* User count
* Device count
* Regulatory requirements
* Security requirements
* Monitoring requirements
* Growth projections

## Licensing Assessment Checklist

Before implementation, verify:

* Required Entra licensing
* Required Intune licensing
* Required Defender plans
* Monitoring requirements
* Compliance requirements
* Budget approval
* Subscription model selection

## Design Recommendations

* Evaluate licensing before architecture design.
* Identify features that require Entra P1 or P2.
* Verify Conditional Access requirements early.
* Verify PIM requirements early.
* Review Defender licensing carefully.
* Align security requirements with budget.
* Document licensing assumptions.
* Reassess licensing annually.

## Conclusion

Licensing is a foundational element of every Azure Landing Zone.

Understanding subscription models, identity licensing, endpoint management requirements, and security licensing helps organizations design an Azure environment that is both technically capable and financially sustainable.
