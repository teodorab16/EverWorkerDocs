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
> Each Connector is tied to a single Provider and defines how Everworker should interact with a specific set of API endpoints. This is where you enter actual values for secrets, that become encoded and not visible to the platform users.

***

## Connector Creation Fields

### Provider

**Purpose:**  
Select the existing **Provider** this Connector will use for API authentication and root configuration.

**How to use it:**  
Use the dropdown to choose from previously created Providers.

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

**Example:**  
`https://api.hubapi.com`

***

### Authentication Mode

**Purpose:**  
Generally it is configured to match the provider's Authentication mode, unless you intend otherwise.

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
Add actual values to the secrets configured in Provider settings.

<br />

***

### App Token OAuth Settings

**Purpose:**  
Allows to configure grant type and other properties for OAuth configuration if it's used in authentication.

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
| **Global ID**                | Unique, machine-friendly identifier inherited from the provider  |
| **Main API URL**             | Default endpoint path                                            |
| **Authentication Mode**      | Inherit Provider auth or set custom auth                         |
| **Public Connector**         | Whether this Connector is visible to others                      |
| **Connector Secrets**        | Secret values just for this Connector                            |
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
