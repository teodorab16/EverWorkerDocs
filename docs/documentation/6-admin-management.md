---
title: Admin & Management
deprecated: false
hidden: false
icon: fad fa-square-6
metadata:
  robots: index
---
### Topics Covered

* **User Management**: Roles (User, Builder, Admin), permissions, and directory sync
* **Platform Settings**: Remote Connection, License Management

***

# Platform Settings

The **Settings** menu tab has two main sections:

1. **Overview**
2. **User Management**

These are presented as sub-tabs at the top of the content area.

***

## Overview Section

#### Key features:

* **Master Server Connection**
  * Displays connection status to the main server (e.g., jarvis.everworker.ai • Remote).
  * Includes a refresh button and connection state (e.g., “Connected”).
* **License Information**
  * Shows current license tier (e.g., "Basic").
  * Displays the number of active workers (e.g., 12 / 23 workers)
* **Recent Users**
  * Lists recently active or pending users, along with email and status.
  * “Manage users” button provides access to deeper user administration.

## User Management Section

#### Key features:

* **Tabs for External and Microsoft Users**
  * Allows switching between user types (likely reflecting different login methods).
* **User Table**
  * Columns: Name, Email, Job Title, Status (e.g., Active, Pending), Roles (e.g., user, admin, builder), and Actions.
  * Each user can have multiple roles and a status badge for clarity.
  * Pagination and search functionality to filter users by name or email.
  * **User Actions**
    * Via a menu (three-dot icon), you can:
      * Resend Invitation (likely for users with “Pending” status).
      * Delete User.
  * **Create New User Button**
    * Provides a form or workflow to invite or register new users into the system.

#### Core Roles:

* User: Can chat with Workers
* Builder: Can create/edit Workers and manage memory
* Admin: Full system access, including user roles, connectors, observability

<br />

| Role    | Build Workers | Manage Users | Manage Providers/ Connector | View Logs | Access Analytics | License Management | Memory Control | Queue Management |
| :------ | :------------ | :----------- | :-------------------------- | :-------- | :--------------- | :----------------- | :------------- | :--------------- |
| User    | No            | No           | No                          | No        | No               | No                 | No             | No               |
| Builder | Yes           | No           | No                          | No        | Yes (Limited)    | No                 | No             | No               |
| Admin   | Yes           | Yes          | Yes                         | Yes       | Yes              | Yes                | Yes            | Yes              |

<br />

**User**

* Primary Audience: End users (non-technical)
* Access:
  * View and chat with pre-built Universal Workers
  * Manage personal session context (files, URLs)
  * Cannot build, edit, or configure workers
* Limitations:
  * No access to Builder tools, Canvas, memory management, or logs

**Builder**

* Primary Audience: Power users, AI engineers, solution designers
* Access:
  * Full access to Universal Worker Builder and Canvas
  * Configure memory, connectors, providers
  * Use Worker Creator (Chat) to auto-generate workflows
  * Test and deploy workers
* Limitations:
  -Cannot manage licenses or view admin dashboards unless granted dual role

**Admin**

* Primary Audience: Platform owners, system operators
* Access:
  * Everything a Builder can do, plus:
  * User management (roles, invites, sync)
  * Provider/connector management
  * System configuration (log cleanup, performance monitoring)
  * License allocation

***

# Summary

EverWorker’s Admin & Management systems provide the structure and tools needed to **run the platform securely at scale**. From user roles and connectors to knowledge storage and observability, these systems ensure the platform remains **governable, transparent, and enterprise-ready** — while empowering Builders and Users alike.
