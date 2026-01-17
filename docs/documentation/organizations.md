---
title: Organizations
excerpt: >-
  Team-based access control for organizing users, workers, and resources by department or team
deprecated: false
hidden: false
icon: fad fa-users
metadata:
  robots: index
---

Organizations enable **team-based access control** in EverWorker, allowing companies to replicate their organizational structure (departments, teams, projects) within the platform. This feature provides flexible, organization-scoped access with controlled sharing capabilities.

***

# Overview

**Organizations** are logical containers that group users and entities (Workers, Connectors, Knowledge) by team, department, or project.

```
Acme Corp (Company)
│
├── Marketing Organization
│   ├── Members: Alice (Builder), Bob (User), Carol (Admin)
│   └── Entities: Workers, connectors, knowledge items
│
├── Sales Organization
│   ├── Members: Dave (Builder), Eve (Admin), Alice (User)
│   └── Entities: Workers, connectors, knowledge items
│
└── Finance Organization
    ├── Members: Frank (Admin), Greg (Builder)
    └── Entities: Workers, connectors, knowledge items
```

***

# Key Benefits

* **Enterprise-Ready**: Supports multi-department, complex organizational structures
* **Secure**: Proper isolation between teams with clear security boundaries
* **Collaborative**: Controlled sharing across teams when needed
* **Scalable**: Works for small teams to large enterprises
* **Compliant**: Meets data access control requirements

***

# Core Capabilities

### Organization Isolation

Resources in one organization are NOT visible in another by default:
* Each organization has its own workers, connectors, and knowledge
* Clear security boundaries between departments
* Marketing workers stay in Marketing unless explicitly shared

### Multi-Organization Membership

Users can belong to multiple organizations with different roles:
* Alice can be a **Builder** in Marketing and a **User** in Sales
* Permissions are organization-scoped
* Being a Builder in Marketing doesn't make you a Builder in Sales

### Organization Switching

Users work in ONE organization at a time:
* Switch between organizations easily from the header
* All operations happen in context of the active organization
* UI updates to show the current organization's entities
* Role and permissions adjust automatically when switching

### Filtering Options

When viewing workers and other entities:
* **All**: View everything you have access to
* **Global**: View company-wide resources
* **Organization**: View current organization's resources only
* **Own**: View only your personal/private resources

***

# Entity Visibility Levels

Four visibility options for Workers, Connectors, and Knowledge:

| Visibility | Description | Use Case |
|------------|-------------|----------|
| **Private** | Only creator can see | Personal drafts, experiments |
| **Organization** | Current organization only | Team-specific resources |
| **Shared** | Selected organizations | Cross-team collaboration |
| **Company-Wide** | All organizations | Company standards, templates |

**Examples:**
* "Lead Qualification Bot" → **Organization** (Marketing only)
* "Lead Scoring Model" → **Shared** (Marketing + Sales)
* "Company Handbook" → **Company-Wide** (everyone)
* "My Test Bot" → **Private** (creator only)

***

# Role-Based Access Control

### Roles Within Organizations

| Role | Create Workers | Edit Own | Edit Others | View Private | Manage Org |
|------|----------------|----------|-------------|--------------|------------|
| User | No | No | No | Own only | No |
| Builder | Yes | Yes | No | Own only | No |
| Organization Admin | Yes | Yes | Yes | All in org | Yes |
| Platform Admin | Yes | Yes | Yes | All everywhere | Yes |

### Admin Levels

**Organization Admin**
* Admin assigned to specific organization(s)
* Full control within those organizations
* Cannot access other organizations
* Cannot create/delete organizations

**Platform Admin**
* Admin assigned at platform level
* Full control over ALL organizations
* Can create/delete organizations
* Manages platform-wide settings

***

# Managing Organizations

### Creating an Organization

Platform Admins can create new organizations:

1. Navigate to **Settings** > **Organizations**
2. Click **Create Organization**
3. Enter organization name and description
4. Add initial members and assign roles
5. Click **Create**

### Adding Members

Organization Admins can add members to their organization:

1. Go to the organization settings
2. Click **Add Member**
3. Select users from the company directory
4. Assign their role within the organization
5. Click **Add**

### Switching Organizations

To switch your active organization:

1. Click the organization name in the header
2. Select the organization you want to switch to
3. The UI refreshes to show that organization's context

***

# Platform Impact

### Workers (AI Workers & AI Workflows)

* Scoped to organization by default
* Can be shared across organizations
* Dependencies are validated when sharing

### Connectors

* Organization-specific with separate credentials
* Each organization configures their own connector instances
* Marketing's HubSpot connector ≠ Sales' HubSpot connector

### Knowledge

* Scoped to organization
* Can be shared across organizations for collaboration
* Maintains single source of truth when shared

### Analytics

* Regular users see current organization only
* Platform Admins can view cross-organization analytics

***

# Use Cases

### Department Isolation

Keep sensitive workflows separate:
* HR workflows for employee data stay in HR
* Finance workflows for financial data stay in Finance
* No accidental exposure between departments

### Cross-Team Collaboration

Share specific resources when needed:
* Marketing shares lead qualification bot with Sales
* Both teams can use it, but Marketing controls it
* Dependencies are validated to ensure it works

### Multi-Tenant Enterprise

Support complex organizational structures:
* Regional teams (Americas, EMEA, APAC)
* Functional teams (Engineering, Product, Design)
* Project-based teams (Project Alpha, Project Beta)

***

# Best Practices

1. **Start with Organization visibility** - Make team resources visible to the team by default
2. **Use Private for drafts** - Keep work-in-progress private until ready
3. **Share intentionally** - Only share across organizations when there's a clear need
4. **Validate dependencies** - When sharing workers, ensure all dependent resources are also accessible
5. **Review membership regularly** - Keep organization membership up to date as teams change
