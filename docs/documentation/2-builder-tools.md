---
title: Builder Tools
excerpt: >-
  This section provides guidance for the creation, configuration and deployment
  of AI agents
deprecated: false
hidden: false
icon: fad fa-square-2
metadata:
  robots: index
---
The **Builder Tools** section of the EverWorker platform provides everything a Builder needs to create, configure, and deploy powerful AI agents tailored to specific workflows. It includes both **visual** and **natural language** creation tools to accommodate a range of technical skill levels and complexity requirements.

### Topics Covered:

* **AI Worker Builder**: A structured, multi-tab interface for configuring and deploying AI Workers
* **Canvas**: A visual, node-based interface for building AI Workflows through drag-and-drop logic blocks, connectors, and custom flows.
* **Worker Creator (Chat)**: An AI-powered assistant that helps Builders generate workflows using natural language prompts—ideal for quick prototyping and non-technical creators.
* **Node Types, Connections, and Workflow Logic**: Details on available nodes (API, conditional logic, vector memory, etc.), how they connect, and how workflows execute step-by-step.

***

# AI Worker Builder

A structured UI that guides Builders through the configuration of **AI Workers**, which are reusable, general-purpose agents.

### Key Tabs:

* **Profile** – Define name, avatar, description, tags, and custom welcome message
* **Knowledge** – Attach vector memory sets, select embedder, configure retrieval behavior
* **Brain** – Set up input structure, tone, formatting, and base LLM parameters
* **Skills** – Add connectors, APIs, or embedded AI Workflows as callable tools
* **Summary** – Final validation screen with a toggle for public sharing and template generation

### Profile Tab Details

The Profile tab allows Builders to configure the Worker's identity and user-facing presentation:

* **Name & Avatar**: Set a recognizable name and visual identity
* **Description & Tags**: Help users discover and understand the Worker's purpose
* **Custom Welcome Message**: Configure a personalized greeting that users see when starting a new chat session with the Worker

_`Best for: Workers used across teams or tasks with dynamic input/output handling`_

***

# Canvas

**Canvas** is EverWorker's **visual builder** for creating **AI Workflows**. It provides a **drag-and-drop, node-based interface** to design workflows that execute structured logic.

### Key Capabilities:

* **No-code and low-code** creation via a visual graph structure
* **Modular Node System** with over a dozen node types (API, logic, vector memory, browser automation, etc.)
* **Node-by-node testing** and real-time execution feedback
* **Custom connectors** per node for precise control of external service integration
* **In-canvas metadata editing**: name, description, tags directly in the workspace
* **Grid snap**: Nodes automatically align to grid for cleaner layouts
* **Monaco Editor**: Professional code editing with syntax highlighting and IntelliSense for Custom Nodes
* **Retry with delay**: Configure automatic retries with delay intervals for LLM and API nodes
* **Node ID display**: Node IDs displayed on cards for easy reference and debugging
* **Search in add-node list**: Quickly find nodes by name when adding new nodes to the canvas

### Node Types Include:

* **API Node**: Call external services
* **Custom Node**: Run JS/Python snippets
* **If / Case**: Conditional logic
* **Map / Fold**: Looping and aggregation across lists
* **Vector Search / Save**: Retrieve or store memory embeddings
* **PDF to Image**: Convert documents for downstream processing
* **Run AI Workflow**: Execute another workflow with specific inputs
* **BaaS**: Browser automation for UI workflows

### Current Focus:

* Smoothing builder experience, improving node UX, and guiding flow creation
* Enhancing runtime stability and compatibility between nodes
* Enabling advanced branching, triggering, and in-session context reuse

***

# Worker Creator (Chat)

This AI-driven assistant helps Builders **create workflows through natural language instructions**. It is integrated into Canvas and designed to accelerate setup by translating user prompts into executable node structures.

### Capabilities:

* Convert plain-language tasks into workflows
* Suggest or auto-create nodes, parameters, and connections
* Explain node functions and behavior logic
* Planned: error correction, undo/redo, diff views for workflow changes

***

# Workflow Logic and Node Connections

* Nodes are linked via **input/output ports** to create directed execution chains
* Each connection passes structured data or control signals
* **Execution status indicators** show whether nodes are ready, completed, or failed
* Execution can be **step-by-step** (per node) or** end-to-end**
* Advanced builders can edit node logic via a **Raw tab** for direct JSON/config access

***

# Templates and Skill Combinations

Builders can accelerate development using templated instructions, logic blocks, and skill bundles:

* **Behavior Templates**: Prewritten prompt structures for different agent personas
* **Skill Combinations**: Suggested sets of AI Workflows and API integrations based on common workflows
* **Worker Templates**: Entire AI Worker or AI Workflow blueprints, reusable and modifiable
* Future features will support **AI-suggested templates** and **version-controlled templates** across teams

***

# Summary

The Builder Tools in EverWorker are designed to make **complex AI workflows accessible and customizable**, whether through code, visuals, or natural language. Canvas offers power and structure for building specialized logic, while Worker Creator provides speed and ease. Combined with rich node types and reusable templates, these tools enable Builders to create flexible, intelligent automation tailored to any business use case.