---
title: 9. Navigation & User Experience
excerpt: >-
  This section covers the navigation structure and user experience design
  patterns.
deprecated: false
hidden: false
metadata:
  robots: index
---
### Topics Covered:

* **Persona-Based Navigation**: Tailored interfaces for Users, Builders, and Admins
* **Menu Structure**: Organized access to platform features
* **Design System**: UI/UX components, themes, and interaction patterns
* **Entry Points**: Role-based landing experiences

***

# Persona-Based Navigation

The EverWorker platform adapts its interface based on the user’s role, ensuring clarity and minimizing cognitive overload.

* **User**:
  * Sees only the **Worker Chat Interface**
  * Access to **session history, file upload**, and **memory toggles**
  * No visibility into builder or system features
* **Builder:**
  * Access to:
    * **Canvas**
    * **Universal Worker Builder**
    * **Worker Creator (Chat)**
    * **Memory Manager**
    * **Connectors & Providers**
  * Tailored menus for creation, testing, and iteration
* **Admin:**
  * Full platform access including:
    * **User Management**
    * **Observatory**
    * **License & App Control**
    * **Analytics Dashboard**
* **Dashboard Viewer, Log Reader**, and others see **restricted views** aligned with their roles

***

# Menu Structure

The platform uses a **left-hand vertical sidebar** for persistent navigation, organized by function:

1. **Home / Launchpad** (role-based)
2. **Workers** (Universal, Specialized)
3. **Canvas**
4. **Memory**
5. **Connectors**
6. **Analytics**
7. **Admin Tools** (visible to Admins only)
8. **Settings** (personal + system)
9. **Help & Support**

Each section expands into **contextual sub-navigation** or modal views when needed.

***

# Design System

EverWorker employs a consistent, lightweight, and scalable **design system**:

* **Themes**: Light and dark modes
* **Component library**: Reusable UI blocks (cards, tables, modals, tabs)
* **Interaction patterns**:
  * Breadcumbs and contextual toolbars
  * Hover states, tooltips, and collapsible sections
  * Inline loaders and state indicators
* Designed for **responsiveness**, with desktop-first UX and tablet/mobile considerations in roadmap

***

# Entry Points

Role-specific landing experiences ensure users are directed to what matters:

* User → Enters directly into the Worker List or last active session
* Builder → Enters into Canvas or a project dashboard
* Admin → Lands on Platform Center or Observatory
* First-time users see a guided onboarding modal with contextual tips and examples

***

# Summary

EverWorker’s navigation model is designed to be intuitive, role-aware, and task-oriented. Whether you're a User looking to get work done, a Builder launching workflows, or an Admin overseeing platform operations, the interface adapts to keep you focused and productive with minimal friction.
