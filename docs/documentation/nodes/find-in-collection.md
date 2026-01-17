---
title: ● Find in Collection
excerpt: >-
  A node used to query documents from user-defined collections with full MongoDB
  query support.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Query documents from user-defined MongoDB collections with full query support. It supports both single document (findOne) and multiple document (find) queries with MongoDB selector and options syntax.

# When to Use

Use this node when you need to retrieve data from collections for further processing or decision-making. Ideal for looking up user records, finding related data, filtering by criteria, or implementing search functionality. Use findOne mode when you expect a single result (like user lookup by email), and find mode when you need multiple results (like listing all active users).

# Parameters

<br />

* collectionId (required) - The ID of the collection to query
  * Examples: `collection-id-123`, `{{0.selectedCollection}}`
* mode (required) - Query mode - findOne returns single document, find returns array
  * Options: `findOne`, `find`
* selector (optional) - MongoDB query selector as JSON. Empty {} returns all documents. Supports template syntax.
  * Examples:
    * `{"name": "John"}`
    * `{"age": {"$gte": 18}}`
    * `{"_id": "{{1.result.userId}}"}`
    * `{"status": "active", "score": {"$gt": 100}}`
* options (optional) - MongoDB query options as JSON. Supports limit, sort, fields, skip.
  * Examples:
    * `{"limit": 10}`
    * `{"sort": {"createdAt": -1}}`
    * `{"limit": 5, "sort": {"score": -1}}`
    * `{"fields": {"name": 1, "email": 1}}`

# Capabilities

* Query single documents with findOne mode
* Query multiple documents with find mode
* Full MongoDB selector syntax support
* Query options support (limit, sort, fields, skip)
* Multi-scope collection access (own, group, global)
* Template syntax for dynamic queries
* Access control enforcement

# Result Access Patterns

**For findOne mode:**
* `{{nodeId.result.document}}` - Retrieved document
* `{{nodeId.result.found}}` - Boolean indicating if document was found

**For find mode:**
* `{{nodeId.result.documents}}` - Array of retrieved documents
* `{{nodeId.result.count}}` - Number of documents retrieved

# Usage Example

```json
{
    name: "Find User by Email",
    description: "Find a specific user document from a collection",
    nodeId: "n",
    operationReference: {
        methodId: "find_in_collection"
    },
    parameters: [
        {
            name: "collectionId",
            value: "users-collection-id" // Target collection ID
        },
        {
            name: "mode",
            value: "findOne" // Single document query
        },
        {
            name: "selector",
            value: "{\"email\": \"{{1.result.userEmail}}\"}" // Query by email from previous node
        },
        {
            name: "options",
            value: "{\"fields\": {\"name\": 1, \"email\": 1, \"status\": 1}}" // Return only specific fields
        }
    ]
}
```

<br />
