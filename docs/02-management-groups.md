# Management Groups

## Overview

Management Groups provide a hierarchical structure for organizing Azure subscriptions and enforcing governance at scale. They allow administrators to apply policies, role assignments, and compliance requirements across multiple subscriptions from a central location.

In an enterprise Azure environment, Management Groups are typically used to separate platform services, production workloads, development environments, and sandbox resources.

## Benefits

Management Groups provide:

* Centralized governance
* Consistent policy enforcement
* RBAC inheritance
* Subscription organization
* Simplified compliance management
* Scalable cloud administration

## Typical Enterprise Hierarchy

```text
Tenant Root Group
│
├── Platform
│   ├── Identity
│   ├── Connectivity
│   └── Management
│
├── Production
│
├── NonProduction
│
└── Sandbox
```

## Policy Inheritance

Policies assigned at a higher Management Group automatically apply to child Management Groups and subscriptions.

Example:

```text
Tenant Root Group
   │
   └── Production
         │
         └── Subscription-A
```

If a policy requiring resource tagging is assigned at the Production Management Group, all resources created in Subscription-A must comply with that policy.

## RBAC Inheritance

Role assignments can also be inherited.

For example:

* Reader assigned at Platform Management Group
* Automatically applies to all child subscriptions

This reduces administrative overhead and improves consistency.

## Design Recommendations

* Keep hierarchy simple.
* Separate platform and workload subscriptions.
* Avoid deeply nested structures.
* Use Management Groups for governance, not resource organization.
* Apply security policies at higher levels whenever possible.

## Example Lab Implementation

```text
MG-Platform
MG-Production
MG-NonProduction
MG-Sandbox
```

Subscriptions:

```text
Subscr-Identity
Subscr-Connectivity
Subscr-Management
Subscr-Production
Subscr-Dev
Subscr-Sandbox
```

This structure supports enterprise-scale Azure environments while maintaining clear administrative boundaries.
