---
title: Creating a connector
deprecated: false
hidden: false
icon: far fa-angles-down
metadata:
  robots: index
---
<br />

# Connectors

A **Connector** in Everworker links your workflow and nodes to a specific **Provider's API endpoints**. It configures the details necessary to access, map, and secure external actions, letting your automations call third-party services easily and securely.

This guide explains each field in the **Connector creation UI**, along with recommended best practices.

> ℹ️ Connector overview
>
> Each Connector is tied to a single Provider and defines how Everworker should interact with a specific set of API endpoints.

***

## Connector Creation Fields

### Provider

**Purpose:**  
Select the existing **Provider** this Connector will use for API authentication and root configuration.

**How to use it:**  
Use the dropdown to choose from previously created Providers.

> ⚠️ Important
>
> Each Connector can reference only **one** Provider.

***

### Name

**Purpose:**  
A human-friendly label for your Connector.

**Best practice:**  
Make it clear and specific to the set of endpoints you intend to expose or work with.

**Examples:**

* **ClickUp Task Manager**
* **HubSpot Contact Sync**
* **Private CRM Actions**

***

### Description

**Purpose:**  
Provide additional detail about the Connector's role. This is useful for usage notes, special endpoint coverage, or workflow context.

**Example:**  
_Creates and updates user tasks. Requires OAuth read/write permissions._

***

### Global ID

**Purpose:**  
A unique, machine-compatible identifier for this Connector, used in code, workflow definitions, and API calls.

**Important:**  
It references the exact Global ID of the Provider the Connector is created from and **cannot be changed**.

***

### Main API URL

**Purpose:**  
The primary root endpoint or base path for the API requests this Connector will make.

**How to use it:**  
This is usually the path appended to the Provider's base URL. It may also include placeholders for parameters.

**Example:**  
`/v2/task`

If the Provider base URL is `https://api.clickup.com`, the resulting request path becomes:  
`https://api.clickup.com/v2/task`

***

### Authentication Mode

**Purpose:**  
Determines how authentication is managed for all endpoints in the Connector.

**Options:**

* **Inherited from Provider** — Uses the Provider's authentication method. This is the default.
* **Override** — Lets you specify a different method for this Connector.

**Use this when:**  
You need more granular control, such as:

* additional headers
* different secrets
* different OAuth scopes
* endpoint-specific authentication behavior

***

### Public Connector

**Purpose:**  
Indicates whether this Connector can be used by anyone in your workspace or remains private to your workflows.

**How to use it:**

* Enable it if the Connector should be discoverable and reusable by others
* Disable it for sensitive, restricted, or experimental APIs

***

### Connector Secrets

**Purpose:**  
Add credentials that are specific to this Connector and are not part of the shared Provider configuration.

**Use cases:**

* endpoint-specific API keys
* secondary tokens
* connector-specific credentials

> ❗️Security best practice
>
> Never include secrets in the Connector **Name** or **Description**. Always use **Connector Secrets**, which are encrypted and access-controlled.

***

### App Token OAuth Settings

**Purpose:**  
Configure OAuth flows and application tokens if this Connector needs to handle authentication differently from, or in addition to, the linked Provider.

**Available fields:**

* **Client ID / Client Secret** — if different from the Provider
* **Scopes** — OAuth scopes required by this Connector
* **Custom Auth URL / Token URL** — for non-standard OAuth flows

**Best practices:**

* Use these settings only when your Connector needs custom OAuth behavior
* Leave them inherited by default unless your endpoints require different permissions
* Override only when necessary to keep configuration simple and maintainable

***

## After Saving

After configuring all fields, save your Connector.

Your Connector can then be:

* used when building workflows
* attached to nodes and automations
* shared with team members if marked as **Public**

***

## Summary Table

| Field                        | Description                                                      |
| :--------------------------- | :--------------------------------------------------------------- |
| **Provider**                 | Which configured Provider to use                                 |
| **Name**                     | Human-readable Connector label                                   |
| **Description**              | Purpose, endpoint group, and usage notes                         |
| **Global ID**                | Unique, machine-friendly identifier                              |
| **Main API URL**             | Default endpoint path or base request path                       |
| **Authentication Mode**      | Inherit Provider auth or set custom auth                         |
| **Public Connector**         | Whether this Connector is visible to others                      |
| **Connector Secrets**        | Extra credentials just for this Connector                        |
| **App Token OAuth Settings** | Connector-specific OAuth configuration, typically left inherited |

***

## Tips and Best Practices

* **Name and describe Connectors clearly** so others can understand and reuse them
* Use **Connector Secrets** for anything that is not global or Provider-wide
* Set a Connector to **Public** only if you want it discoverable by all workspace members
* Keep OAuth and credential flows as simple as possible unless you have a specific need to override them

> ✅ Recommendation
>
> In most cases, inheriting authentication and OAuth settings from the Provider is the simplest and safest approach.
