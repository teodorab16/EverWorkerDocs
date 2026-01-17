# Organizations Feature - Overview

## Summary
Organizations introduces **team-based access control** to EverWorker, enabling companies to replicate their organizational structure (departments, teams, projects) within the platform. This feature solves the current limitation where access is binary (Private or Public to everyone) by introducing flexible, organization-scoped access with controlled sharing capabilities.
**Business Impact:**
*   ✅ Enables enterprise deployments with proper access isolation
*   ✅ Supports multi-department usage with security boundaries
*   ✅ Facilitates cross-team collaboration with controlled sharing
*   ✅ Meets compliance requirements for data access control
*   ✅ Scales from small teams to large enterprises
* * *
## The Problem
### Current State Limitations
**Entity-Level Access is Binary:**
*   **Private** = Only creator can see
*   **Public** = Everyone in the company can see
*   No middle ground for team-level or department-level sharing
**Cannot Replicate Company Structure:**
*   Marketing team cannot isolate their workers from Finance
*   No departmental boundaries
*   HR and Finance sensitive workflows exposed to everyone
*   Cross-functional collaboration is all-or-nothing
**Security & Compliance Risks:**
*   Cannot restrict sensitive data by department
*   No audit trail by organizational unit
*   Difficult to comply with data access policies
*   Cannot support multi-tenant enterprise scenarios
* * *
## The Solution: Organizations
### What Are Organizations?
**Organizations** are logical containers that group users and entities (Workers, Connectors, Knowledge) by team, department, or project.

```yaml
Acme Corp (Company)
│
├── Marketing Organization
│   ├── Members: Alice (Builder), Bob (User), Carol (Admin)
│   └── Entities: 61 workers, connectors, knowledge items
│
├── Sales Organization
│   ├── Members: Dave (Builder), Eve (Admin), Alice (User)
│   └── Entities: 45 workers, connectors, knowledge items
│
└── Finance Organization
    ├── Members: Frank (Admin), Greg (Builder)
    └── Entities: 28 workers, connectors, knowledge items
```

* * *
## Core Capabilities
### 1\. Organization Isolation
*   Resources in Marketing are NOT visible in Sales by default
*   Each organization has its own workers, connectors, knowledge
*   Clear security boundaries between departments
### 2\. Multi-Organization Membership
*   Users can belong to multiple organizations
*   Different roles in different organizations
*   Example: Alice is Builder in Marketing, User in Sales
### 3\. Flexible Sharing
*   Share specific entities across organizations
*   Control exactly who sees what
*   Dependency validation ensures shared resources work correctly
### 4\. Active Organization Context
*   Users work in ONE organization at a time
*   Switch between organizations easily
*   All operations happen in context of active organization
* * *
## Entity Visibility Levels
Four visibility options for all entities (Workers, Connectors, Knowledge):

| Visibility | Icon | Description | Use Case |
| ---| ---| ---| --- |
| Private | 🔒 | Only creator | Personal drafts, experiments |
| Organization | 👥 | Current org only | Team-specific resources |
| Shared | 🔗 | Selected orgs | Cross-team collaboration |
| Company-Wide | 🏢 | All orgs | Company standards, templates |

**Example:**
*   "Lead Qualification Bot" → **Organization** (Marketing only)
*   "Lead Scoring Model" → **Shared** (Marketing + Sales)
*   "Company Handbook" → **Company-Wide** (everyone)
*   "My Test Bot" → **Private** (creator only)
* * *
## Key User Experiences
### Organization Switching
**User Interface:**

```cpp
┌─────────────────────────────────────┐
│ 👥 Marketing ▼    Alice (Builder) ▼ │
└─────────────────────────────────────┘
     └─ Click to switch organizations
```

**When switching from Marketing → Sales:**
*   UI updates to show Sales entities
*   Role changes (Builder → User)
*   Permissions adjust automatically
*   Private entities follow user
* * *
### Sharing Workflow
**3-Step Process:**
**Step 1:** Choose visibility level

```sql
Change to:
○ Private
○ Organization  
● Shared - Select organizations
○ Company-Wide (Admin only)
```

**Step 2:** Select target organizations

```cs
Share with:
☑ Sales
☑ Customer Success
☐ Finance
```

**Step 3:** Dependency check (automatic)

```cs
⚠️ This worker uses:
✅ Company DB - Already accessible
⚠️ Lead Scorer - NOT accessible in Sales

☑ Also share "Lead Scorer" with Sales
```

**Result:** Entity and dependencies shared automatically
* * *
## Role-Based Access Control
### Admin Role: Two Assignment Levels
**Single "Admin" role, assigned at different scopes:**
#### Organization Admin
*   Admin assigned to specific organization(s)
*   Full control within those organizations
*   Cannot access other organizations
*   Cannot create/delete organizations
**Example:** Alice is Admin in Marketing → Organization Admin for Marketing
#### Platform Admin
*   Admin assigned at platform level
*   Full control over ALL organizations
*   Can create/delete organizations
*   Manages platform settings
**Example:** Frank is Platform-level Admin → Platform Admin
* * *
### Permission Model

| Role | Create Workers | Edit Own | Edit Others | View Private | Manage Org |
| ---| ---| ---| ---| ---| --- |
| User | ❌ | ❌ | ❌ | Own only | ❌ |
| Builder | ✅ | ✅ | ❌ | Own only | ❌ |
| Org Admin | ✅ | ✅ | ✅ | All in org | ✅ |
| Platform Admin | ✅ | ✅ | ✅ | All everywhere | ✅ |

**Note:** Permissions are organization-scoped. Being a Builder in Marketing doesn't make you a Builder in Sales.
* * *
## Platform Impact Areas
### Universal & Specialized Workers
*   Scoped to organization by default
*   Can be shared across organizations
*   Dependency validation at build time
*   Runtime errors if dependencies unavailable
### Connectors & Providers
*       *   **Two-level model:**Connector Definitions (platform-wide templates)
    *   Connector Instances (org-specific with credentials)
*   Each organization has own credentials for security
*   Marketing's HubSpot ≠ Sales' HubSpot (different auth)
### Knowledge & Memory
*   Scoped to organization
*   Can be shared across organizations
*   Single source of truth when shared
### Analytics
*   Regular users see current organization only
*   Platform Admin gets "All Organizations" filter
*   Cross-organization insights for debugging

* * *
## Key Decisions Made

| Decision | Choice | Rationale |
| ---| ---| --- |
| Feature Name | Organizations | Business-friendly, matches company structure |
| Visibility Levels | 4 levels (Private, Org, Shared, Company-Wide) | Flexible without complexity |
| Admin Model | Single role, two scopes | Simpler than two role types |
| Platform Admin Access | Must switch orgs (except Analytics) | Prevents accidents, clear context |
| Connector Model | Definitions + Instances | Security isolation, credential separation |
| Default Visibility | Organization | Safe default, explicit sharing required |

* * *
* * *
## Conclusion
Organizations is a foundational platform enhancement that enables EverWorker to serve enterprise customers with complex organizational structures. By providing flexible, secure, team-based access control, this feature removes a critical barrier to adoption while maintaining the simplicity and ease-of-use that defines EverWorker.
**Key Benefits:**
*   🎯 **Enterprise-Ready:** Supports multi-department, complex org structures
*   🔒 **Secure:** Proper isolation, credential separation, audit trails
*   🤝 **Collaborative:** Controlled sharing across teams
*   📈 **Scalable:** Works for 3 people or 3,000 people
*   🚀 **Migration-Friendly:** Smooth path for existing customers
* * *