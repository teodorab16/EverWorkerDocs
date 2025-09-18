---
title: ● Vector Search
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Search vector databases using semantic similarity.

# When to Use

Use this node to find semantically similar content from previously saved vector data. Perfect for building knowledge retrieval systems.

# Parameters

* memoryId (required) - Memory collection to search
   -Example: `{{memory_id}}`
* input (required) - Search query
  * Example: `{{search_query}}`
* limit (optional) - Maximum number of results
  * Default: 10
* minScore (optional) - Minimum similarity score
  * Default: 0.7
