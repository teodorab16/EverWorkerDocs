---
title: Provider & Integration System
excerpt: >-
  This section covers the system for integrating external services and managing
  providers and connectors.
deprecated: false
hidden: false
icon: fad fa-square-3
metadata:
  robots: index
---
### Topics Covered:

* **Provider Architecture**: OpenAPI-based external service integrations
* **Connector Management**: Authentication and access control for providers
* **LLM Models**: Configure and manage available LLM models
* **Central Repository**: Curated provider library with sync capabilities
* OAuth and authentication flows
* Provider versioning and updates

***

# Provider Architecture

Providers in EverWorker represent **external APIs or service ecosystems** (e.g., Microsoft 365, OpenAI, GitHub) defined using **OpenAPI specifications**. Each Provider includes a detailed schema of endpoints and methods, enabling Workers to interact with external services programmatically and consistently.

* Providers serve as the **foundation for all tool-based capabilities** within Workers
* Managed centrally by EverWorker through an automated **API Scraper system** that keeps specs current
* Can support hundreds of providers, covering major enterprise and SaaS ecosystems
* **Supports both JSON and YAML formats** for OpenAPI specification uploads

***

# Connector Management

Connectors are **instances of Providers**, configured with **authentication credentials and context-specific settings** (e.g., for different tenants, users, or environments).

* Multiple Connectors can be created per Provider (e.g., two Gmail accounts, separate OpenAI keys)
* Support for **authentication parameters** such as API keys, OAuth tokens, tenant IDs, and more
* Assigned on a **per-node or per-worker** basis in AI Workflows, and per skill in AI Workers
* Configurable via a secure UI, with role-based access (Builders/Admins)

***

# LLM Models

LLM Models allows Admins to configure and manage the **Large Language Models** available across the platform. This feature is accessible as a tab within **Providers** in the navigation menu (alongside Your Connectors, Your API Providers, MCP Servers, and Incoming Webhooks).

### Key Capabilities:

* **Add New LLM Models**: Register new models with their provider, capabilities, and pricing
* **Configure Model Features**: Define what each model supports:
  * Reasoning, Streaming, Structured Output
  * Function Calling, Fine-tuning, Realtime
  * Predicted Outputs
* **Input/Output Configuration**:
  * Maximum token limits for input and output
  * Cost per million tokens (CPM) for billing/budgeting
  * Cached input pricing
  * Modality support (text, image, audio)
* **Enable/Disable Models**: Toggle model availability across the platform
* **Edit and Delete**: Update model configurations or remove deprecated models

### Model Properties:

| Property | Description |
|----------|-------------|
| **Name** | The model identifier (e.g., gpt-4, claude-3-sonnet) |
| **Provider** | The LLM provider (e.g., openai, anthropic, google) |
| **Status** | Active or Inactive |
| **Features** | Capabilities like streaming, function calling, etc. |
| **Input Tokens** | Maximum context window size |
| **Output Tokens** | Maximum response length |
| **Cost (CPM)** | Pricing per million tokens for input and output |

***

# Central Repository

EverWorker maintains a **curated library of Providers**, regularly updated through the API Scraper engine. This is known as the **Provider Central Repository**.

* Customers **select and sync only the Providers** relevant to their needs
* Sync operation pulls **the latest, validated OpenAPI definitions**
* Eliminates manual setup and version drift
* Available during initial setup or reconfigured on demand

***

# OAuth and Authentication Flows

EverWorker supports **multiple authentication models** to handle secure, multi-user environments:

* **User OAuth**: Requires end-user login and consent (used when Workers need access to user's personal accounts)
* **App Token**: Uses system-level access credential.
* Supports **OAuth scopes, redirect flows, and token refresh logic**
* Integrated seamlessly in chat, connector config UI, and session workflows

***

# Provider Versioning and Updates

Providers are versioned through EverWorker's backend tooling:

* Admins and Builders are notified of available updates and can **sync new versions** from the Central Repository
* Version history and audit logs are maintained for governance and debugging

***

# Summary

The Provider system in EverWorker ensures **secure, flexible, and up-to-date integrations** across any enterprise or third-party services. With a clear separation between Providers and Connectors, customers can manage complex authentication needs while safely reusing integrations across Workers. Combined with a central repository and real-time version tracking, EverWorker makes external service orchestration fast, reliable, and enterprise-ready.
