---
title: 4. Memory & Knowledge Management (EKE)
excerpt: >-
  This section covers the Enterprise Knowledge Engine and memory management
  systems.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Topics Covered:

* **Enterprise Knowledge Engine (EKE)**: Intelligence layer orchestrating knowledge access
* **Vector Memory**: Document and knowledge embedding system
* **Session Context**: Temporary and persistent memory across interactions
* **Memory Items**: Creation, modification, and management of knowledge base

***

## 💭 Vector Memory

EverWorker uses **Vector Memory** to store and retrieve unstructured knowledge, such as documents, articles, or manual notes.

* Supports **semantic retrieval** using vector embeddings
* Each memory item is broken into **chunks** and embedded using models like `nomic-embed-text` or `mxbai`
* Items include both an **embedded body** (used for semantic search) and a **descriptive prompt** (used in LLM context injection)
* Memory entries can be **uploaded files**, **scraped URLs**, or **manual entries**
* Supports metadata filters and token budgeting to control LLM context length

***

## ⏱️ Session Context

Each interaction session maintains its own scoped **Session Context** - a mix of:

* Enabled memory items
* Uploaded content
* Session settings and metadata

Users can actively manage session context via UI toggles, and Builders can configure which memory is injected automatically.

***

## Memory Items

Memory Items are **modular, reusable knowledge blocks**. Key properties:

* Can be edited, renamed, versioned
* Include rich metadata (source, page count, tags, etc.)
* Description fields shape how the item is referenced and injected into prompts
* Access-controlled and assigned to workspaces or roles
* Are the building blocks of Worker cognition

***

# Summary

The memory system in EverWorker is designed to **augment Workers with deep, contextual, and secure knowledge access**. EKE drives smart orchestration. Vector Memory enables semantic understanding. Session Context keeps every interaction grounded and relevant. And as graph capabilities evolve, Workers will be able to reason across structured knowledge in more powerful, transparent ways.
