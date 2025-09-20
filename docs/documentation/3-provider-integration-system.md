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
* **Central Repository**: Curated provider library with sync capabilities
* OAuth and authentication flows
* Provider versioning and updates

***

# 📐 Provider Architecture

Providers in EverWorker represent **external APIs or service ecosystems** (e.g., Microsoft 365, OpenAI, GitHub) defined using **OpenAPI specifications**. Each Provider includes a detailed schema of endpoints and methods, enabling Workers to interact with external services programmatically and consistently.

* Providers serve as the **foundation for all tool-based capabilities** within Workers
* Managed centrally by EverWorker through an automated **API Scraper system** that keeps specs current
* Can support hundreds of providers, covering major enterprise and SaaS ecosystems

***

# 🔌 Connector Management

Connectors are **instances of Providers**, configured with **authentication credentials and context-specific settings** (e.g., for different tenants, users, or environments).

* Multiple Connectors can be created per Provider (e.g., two Gmail accounts, separate OpenAI keys)
* Support for **authentication parameters** such as API keys, OAuth tokens, tenant IDs, and more
* Assigned on a **per-node or per-worker** basis in Specialized Workers, and per skill in Universal Workers
* Configurable via a secure UI, with role-based access (Builders/Admins)

***

# 💽 Central Repository

EverWorker maintains a **curated library of Providers**, regularly updated through the API Scraper engine. This is known as the **Provider Central Repository**.

* Customers **select and sync only the Providers** relevant to their needs
* Sync operation pulls **the latest, validated OpenAPI definitions**
* Eliminates manual setup and version drift
* Available during initial setup or reconfigured on demand

***

# 🪪 OAuth and Authentication Flows

EverWorker supports **multiple authentication models** to handle secure, multi-user environments:

* **User OAuth**: Requires end-user login and consent (used in Assistant Workers)
* **App Token**: Uses system-level access credential.
* Supports **OAuth scopes, redirect flows, and token refresh logic**
* Integrated seamlessly in chat, connector config UI, and session workflows

***

# 🍂 Provider Versioning and Updates

Providers are versioned through EverWorker's backend tooling:

* Admins and Builders are notified of available updates and can **sync new versions** from the Central Repository
* Version history and audit logs are maintained for governance and debugging

***

# Summary

The Provider system in EverWorker ensures **secure, flexible, and up-to-date integrations** across any enterprise or third-party services. With a clear separation between Providers and Connectors, customers can manage complex authentication needs while safely reusing integrations across Workers. Combined with a central repository and real-time version tracking, EverWorker makes external service orchestration fast, reliable, and enterprise-ready.