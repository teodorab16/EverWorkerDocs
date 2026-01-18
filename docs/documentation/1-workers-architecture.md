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

* AI Workers: Conversational AI agents you can chat with
* AI Workflows: Visual automations built in Canvas
* How AI Workers and AI Workflows work together
* Lifecycle management (creation, deployment, versioning, sharing)

***

# AI Workers

AI Workers are **conversational AI agents** designed to be flexible, modular, and reusable across various tasks. Users interact with AI Workers through a chat interface.

They are created using the AI Worker Builder, where Builders define:

* Profile: Name, avatar, and tags
* Knowledge: Vector memory sources, context documents, semantic search
* Brain: LLM configuration, behavior prompts, role, tone, output format
* Skills: AI Workflows, API Providers (via Connectors), and MCP Tools
* Summary: Final review, visibility (public/private), and deployment

AI Workers support OAuth integrations, file uploads, and dynamic session contexts. They are ideal for users who need consistent, intelligent support across a range of workflows.

***

# AI Workflows

AI Workflows are **visual automations** built for specific, structured tasks using the Canvas interface. Unlike AI Workers, users don't chat with AI Workflows — they execute them with defined inputs and receive structured outputs.

Key characteristics:

* Built visually: Drag-and-drop Canvas with node types (API calls, logic blocks, vector search, etc.)
* Composable: Can be embedded as "Skills" within AI Workers
* Modular: Each node can use its own connector and execute independently
* Flexible: Suitable for automation, backend processes, and domain-specific logic

***

# How They Work Together

AI Workers and AI Workflows are complementary:

| | AI Workers | AI Workflows |
|---|---|---|
| **Interface** | Chat conversation | Structured input/output |
| **Built with** | AI Worker Builder | Canvas |
| **Best for** | Flexible, conversational tasks | Precise, repeatable automations |

**Key relationship**: AI Workflows can be added as **Skills** to AI Workers. This allows a conversational AI Worker to trigger precise automations when needed — combining the flexibility of chat with the reliability of structured workflows.

***

# Lifecycle Management

1. #### Creation
   * AI Workers: Built through a structured builder UI with 5 configuration tabs (Profile, Knowledge, Brain, Skills, Summary)
   * AI Workflows: Built using Canvas, via manual configuration or AI-assisted Builder Chat
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

The EverWorker architecture is designed for **modularity**, **scalability**, and **flexibility**. AI Workers offer broad utility through conversational AI, while AI Workflows deliver precise automation through visual node-based design. Together, these components support a lifecycle that enables continuous creation, testing, reuse, and governance - all managed under a role-based platform that adapts to both technical and non-technical users.