---
title: Workers Architecture
excerpt: This section covers the foundational architecture of the worker system
deprecated: false
hidden: false
icon: fad fa-square-1
metadata:
  robots: index
---
### Topics Covered:

* AI Workers: General-purpose, reusable AI agents that can be customized and shared
* AI Workflows: Deeply customized agents built for specific use cases using Canvas/Studio
* Assistant Workers: Context-specific agents that exist only to assist humans in specific workflows
* Worker lifecycle management (creation, deployment, versioning, sharing)

***

# Worker Types

### &#x20;AI Workers

AI Workers are general-purpose AI agents designed to be flexible, modular, and reusable across various tasks.
They are created using the AI Worker Builder, where Builders define:

* Profile: Name, avatar, tags, visibility (public/private)
* Knowledge: Vector memory sources, context documents, semantic search
* Brain: LLM configuration, behavior prompts, role, tone, output format
* Skills: API integrations and other embedded capabilities (via Connectors and AI Workflows)

AI Workers support OAuth integrations, file uploads, and dynamic session contexts. They are ideal for users who need consistent, intelligent support across a range of workflows.

### &#x20;AI Workflows

AI Workflows are workflow-driven agents built for specific, structured tasks using the Canvas interface.
They rely on node-based logic, supporting complex control flows, conditions, and data operations.
Key characteristics:

* Built visually: Drag-and-drop Canvas with node types (API calls, logic blocks, vector search, etc.)
* Composable: Can be used as "Skills" within AI Workers
* Modular: Each node can use its own connector and execute independently
* Flexible: Suitable for automation, backend processes, and domain-specific logic

### &#x20;Assistant Workers

Assistant Workers are lightweight, contextual agents tailored to assist humans in narrow scenarios, like connecting to a user’s Gmail or calendar.

* Technically implemented as AI Workers with preconfigured OAuth (personal) connectors and UI behaviors
* Focused on user-specific authorization and real-time integration with personal data

***

# Worker Lifecycle Management

1. #### Creation
   * AI Workers: Built through a structured builder UI with 5 configuration tabs
   * AI Workflows: Built using the Canvas, via manual configuration or AI-assisted Builder Chat
   * Assistant Workers: Created by cloning a AI Worker and adding personal account integrations
2. #### Deployment
   * Workers are deployed into the Worker List (Launchpad) for Users to interact with
   * Builders can set visibility (private/shared/public)
   * AI Workflows can be embedded as Skills in other Workers
3. #### Versioning
   * Workers are versioned implicitly through configuration history and deployment
   * Future enhancements will include templating, rollback, and explicit version labels
4. #### Sharing
   * AI Workers can be marked as public and shared across the organization
   * AI Workflows are reusable as modules within other agents
   * Templates can be saved and reused for consistent setups across teams

***

# Summary

The EverWorker architecture is designed for **modularity**, **scalability**, and **flexibility**. AI Workers offer broad utility, AI Workflows deliver precise automation, and Assistant Workers provide human-centric micro-assistance. Together, these components support a lifecycle that enables continuous creation, testing, reuse, and governance - all managed under a role-based platform that adapts to both technical and non-technical users.
