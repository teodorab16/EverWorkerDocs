---
title: ● Save to Collection
excerpt: >-
  A node used to save documents to user-defined collections with smart upsert
  handling.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Save documents to user-defined MongoDB collections with intelligent upsert handling. It automatically handles both single documents and arrays, performing inserts for new documents and updates for existing ones (based on _id presence).

# When to Use

Use this node when you need to persist workflow data to structured collections for later retrieval, analysis, or reporting. Ideal for saving processed results, user-generated content, API responses, or any structured data that needs to be stored and queried. Supports both transactional updates (updating existing records) and bulk inserts (adding new records).

# Parameters

<br />

* collectionId (required) - The ID of the collection to save data to
  * Examples: `collection-id-123`, `{{0.selectedCollection}}`
* inputData (required) - Data to save - can be a single object or array of objects. If objects have _id field, they will be updated; otherwise inserted.
  * Examples:
    * `{"name": "John", "age": 30}`
    * `[{"name": "Alice"}, {"name": "Bob"}]`
    * `{{1.result.items}}`
    * `{{2.result}}`

# Capabilities

* Save single documents or arrays to collections
* Smart upsert based on _id presence (insert if missing, update if present)
* Multi-scope collection access (own, group, global)
* Performance optimization for large batches
* Automatic Entity field management (ownerId, timestamps, etc.)
* Access control enforcement

# Result Access Patterns

* `{{nodeId.result.documentIds}}` - Array of saved document IDs
* `{{nodeId.result.inserted}}` - Number of documents inserted
* `{{nodeId.result.updated}}` - Number of documents updated
* `{{nodeId.result.total}}` - Total number of documents processed

# Usage Example

```json
{
    name: "Save to Collection",
    description: "Save processed data to a user collection",
    nodeId: "n",
    operationReference: {
        methodId: "save_to_collection"
    },
    parameters: [
        {
            name: "collectionId",
            value: "collection-abc123" // Target collection ID
        },
        {
            name: "inputData",
            value: "{{1.result.processedData}}" // Array or object from previous node
        }
    ]
}
```

<br />
