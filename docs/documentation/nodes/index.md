---
title: Canvas Nodes Reference
excerpt: Complete reference for all AI Workflow nodes in Canvas
deprecated: false
hidden: false
icon: fad fa-arrow-down-square-triangle
metadata:
  robots: index
---
Nodes are the building blocks of AI Workflows in Canvas. Each node performs a specific function — from LLM calls and API requests to data transformations and control flow.

***

# Node Categories

### Input & Output
| Node | Purpose |
|------|---------|
| [Input Node](doc:input-node) | Define workflow input parameters |
| [Output Node](doc:output-node) | Define workflow output structure |

### AI & LLM
| Node | Purpose |
|------|---------|
| [Universal LLM](doc:universal-llm) | Call any configured LLM model |
| [AI Worker Call](doc:ai-worker-call) | Invoke an AI Worker from a workflow |

### Data & APIs
| Node | Purpose |
|------|---------|
| [API Call](doc:api-call-1) | Make HTTP requests to external APIs |
| [Read URL](doc:read-url) | Fetch and parse web content |
| [Browser](doc:browser) | Headless browser automation |
| [CSV to JSON](doc:csv-to-json) | Convert CSV data to JSON format |
| [PDF to Images](doc:pdf-to-images) | Convert PDF pages to images |

### Storage & Memory
| Node | Purpose |
|------|---------|
| [Storage Upload](doc:storage-upload) | Upload files to storage |
| [Vector Save](doc:vector-save) | Save content to vector memory |
| [Vector Search](doc:vector-search) | Semantic search in vector memory |
| [Save to Collection](doc:save-to-collection) | Save data to MongoDB collection |
| [Find in Collection](doc:find-in-collection) | Query MongoDB collections |

### Control Flow
| Node | Purpose |
|------|---------|
| [Worker Call](doc:worker-call) | Call another AI Workflow |
| [Switch Worker](doc:switch-worker) | Conditional branching |
| [Map Worker](doc:map-worker) | Process arrays in parallel |
| [Fold Worker](doc:fold-worker) | Aggregate array results |
| [Until Worker](doc:until-worker) | Loop until condition met |

### Code Execution
| Node | Purpose |
|------|---------|
| [Custom Code Nodes](doc:custom-code-nodes) | Execute JavaScript/Python code |

***

# Common Patterns

**Parameter Templating**: Use `{{nodeId.field}}` syntax to reference outputs from previous nodes.

**Example**: `{{1.response.data.items}}` references the `items` array from node 1's response.