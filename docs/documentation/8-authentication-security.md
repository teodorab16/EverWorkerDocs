---
title: Authentication & Security
excerpt: This section covers the authentication and security systems.
deprecated: false
hidden: false
icon: fad fa-square-8
metadata:
  robots: index
---
<br />

### Topics Covered:

* **Role-Based Access Control**: User, Builder, Admin permissions
* **Authentication Methods**: SSO, SCIM, external account integration

***

# Role-Based Access Control

EverWorker uses **granular, role-based permissions** to control access to platform features.

* Each user is assigned a role: User, Builder, Admin, or specialized admin/user roles (e.g., **Log Reader, Memory Manager**)
* Access to features like Canvas, AI Worker Builder, Observability, Knowledge management, and license administration is governed by role
* More on Roles and Admin **here**.

***

# Authentication Methods

The platform supports multiple login and identity systems:

* **Password-based login**: Default method for manual user creation
* **Microsoft OAuth (SSO)**: Seamless integration with Azure AD for enterprise users
* **Directory Sync (SCIM)**: Planned support for SCIM to automate provisioning and deprovisioning (Coming soon)
* **External User Support**: Invite external collaborators with scoped access and expiration controls

***

# Summary

EverWorker's authentication and security stack is designed to balance **usability and control**. With robust role management, multiple Auth type integrations, and secure credential handling, the platform is well-prepared for enterprise use. As features like SCIM and Secrets Manager evolve, EverWorker will offer even deeper support for **secure, compliant, and scalable deployments**.
