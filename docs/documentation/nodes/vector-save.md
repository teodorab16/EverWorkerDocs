---
title: ● Vector Save
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Save data to vector storage for semantic search and retrieval.

# When to Use

Use this node to store text data in vector databases for later semantic search and retrieval operations.

# Parameters

* memoryId (required) - Memory collection identifier
  * Example: `{{memory_id}}`
* input (required) - Text to save
  * Example: `{{text_to_save}}`
* inputFull (optional) - Full context for the data
  * Example: `{{full_context}}`
* title (optional) - Document title
  * Example: `{{document_title}}`
