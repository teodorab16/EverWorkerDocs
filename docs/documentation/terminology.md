---
title: 🗎 Terminology
deprecated: false
hidden: false
metadata:
  robots: index
---
## Summary of Terminology Relationships

* A **Worker** is the main product, combining behavior (Brain), knowledge (Memory), and tools (Skills) — all of which use **Providers** via **Connectors**.
* **Users** consume Workers, **Builders** create them, and **Admins** maintain the platform.
* **EKE** and **Memory Management** power the intelligence and context in all conversations.
* **Canvas** allows workflow design for Specialized Workers, while Universal Worker Builder manages Universal Workers.
* Everything relies on structured, governed access through roles and entry points.

***

### 🤖 Worker

An AI agent designed to perform tasks using LLMs, memory, connectors, and structured logic. Workers can be created, configured, and deployed through the EverWorker platform.

* **Universal Worker**: A general-purpose worker with flexible configuration, suitable for a wide range of tasks. Built using the Universal Worker Builder.
* Specialized Worker: A focused, task-specific worker constructed visually in the Canvas interface using nodes and flows.

### 🧩 Provider

An OpenAPI-based definition for external APIs or services. It acts as the technical foundation for integrating external systems into Workers.

* **Custom Provider**: A user-defined OpenAPI Provider not in the central repository.
* **Central Repository Provider**: Curated and managed by EverWorker. Syncable by customers.

### 🔌 Connector

A configuration that connects a Worker to a specific instance of a Provider, managing authentication and access.

* **Authentication Methods**: OAuth (user-level), App Token (system-level), or Hybrid (preferred user token with fallback).
* Multiple connectors can exist for a single Provider.

<br />

### 👤 Business User

A non-technical individual who interacts with pre-built Universal Workers via chat. Users don’t modify logic, skills, or memory—they access existing functionality and can upload context (files, URLs) at runtime.

### 👤 Builder

A technical or advanced user who creates, edits, and configures Workers. Builders use tools like the Universal Worker Builder and Canvas to define skills, behavior, and integrations.

### 👤 Admin

Responsible for managing infrastructure, Providers, users, and global configurations. Admins govern access control, observability, memory management, and platform operations.

### 💭 EKE (Enterprise Knowledge Engine)

The intelligence layer of the platform. It enables Workers to integrate and reason over enterprise-specific knowledge, tools, APIs, and memory in a secure and context-aware way.

### 🧠 Memory

Refers to the platform’s system for ingesting, storing, retrieving, and injecting knowledge into LLM conversations.

* Vector Memory: Stores content in embedding-based format to support semantic search and relevance.
* Memory Items: Individual pieces of content (e.g., PDF, URL, manual text).
* Memory Set: A grouping of memory items.
* Full Description: Injected into LLMs directly for context.
* Embedded Description: Used for semantic matching during retrieval.
* Chunking: Automatic splitting of large files for embedding.
* Metadata Filtering: Tagging and filtering content by origin, title, creation date, etc.

### ⏱️ Session (Universal Worker Chat)

A single conversation thread with a Worker. Sessions have individualized context and memory settings.

* Session Context: Includes files, URLs, and toggled skills for that session.
* Session Summary: Automatically generated or user-edited summaries for quick recall.
* Session History: Log of previous chats, searchable and user-manageable.

### 🖼️ Canvas

Visual builder for Specialized Workers. Allows no-code or low-code construction of task flows through a node-based interface.

* Node: Building block of a workflow. Types include API Node, Code Executor, Vector Search, Invoke Worker, If/Case, etc.
* Builder Chat: Natural language interface for generating nodes.
* Raw Tab: Manual code editing for each node.
* Status Indicators: Show readiness, execution results, and issues in each node.

### 🛠️ Universal Worker Builder

An interface for building Universal Workers using five structured tabs:

* Profile: Name, avatar, tags, and public/private toggle.
* Knowledge: Memory and knowledge sources.
* Brain: LLM configuration, personality, instructions, prompt structure.
* Skills: Tools and capabilities integrated into the Worker.
* Summary: Final review and deployment screen.

### 📖 Skills

Capabilities that a Worker can use, composed of:

* Specialized Workers: Embedded as callable units within other Workers.
* API Providers: Integrated external services (via Connectors).

Skills are selected in the Worker Builder and can be enabled/disabled per session.

### 🚀 Launchpad

The future home screen for Users, which will display active sessions, suggested actions, and personalized guidance for interacting with Workers.

### 📈 Analytics Dashboard

Tracks performance, ROI, and efficiency of digital Workers.

* ROI Metrics: Manual cost/time estimation input by builders used to show hours/money saved.
* Utilization Charts: Measure how much each Worker is used.
* Failure Rates: Track unsuccessful executions by worker or overall.

### 💻 API Scraper

A tool that extracts content from websites using XML sitemaps to feed data into memory.

* Scraping Jobs: Can be run, paused, or reset.
* Sync from Master: Reuse shared scraping configurations.
* Performance Settings: Configure concurrency, filters, and timing.

### 🚪 Entry Points

Defined access interfaces based on roles.

* User: Worker list and chat only.
* Builder: Full creation/edit access to Workers, memory, and Canvas.
* Admin: Complete system access.
* Dashboard Viewer: Analytics view only.

### 🗣️ MCP (Model Context Protocol)

An emerging integration feature to allow dynamic, secure, and consistent communication between Workers and external servers or agents.
