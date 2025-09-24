---
title: ● Custom Code Nodes
excerpt: >-
  Canvas allows you to create your own algorithms and advanced processes using
  Custom Code nodes.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

In addition to the built-in nodes above, EverWorker supports Custom Code Nodes that appear as a separate section in the "Add Node" dropdown.

# What are Custom Code Nodes?

Custom Code Nodes are user-created JavaScript/TypeScript functions that can be saved and reused across workflows. They appear in the dropdown under a "Custom Code Nodes" section.

# Creating Custom Code Nodes

1. Access Code Node Edtior from the menu in the left hand side.
2. Write your custom JavaScript/TypeScript code
3. Define input parameters your code expects
4. Test and save your code node
5. It will automatically appear in the "Add Node" dropdown

# Using Custom Code Nodes

When you select a custom code node from the dropdown:

* The node uses methodId: "code_node" internally
* It automatically gets a codeNodeId parameter pointing to your saved code
* Additional parameters are generated based on your code node definition
* The display name shows your custom node name in green

# Example Custom Code Node

A custom code node might look like:

```javascript
// Custom code that processes user data
function processUserData(userData, apiKey) {
    // Your custom logic here
    return {
        processedData: userData.map(user => ({
            ...user,
            processed: true,
            timestamp: new Date()
        })),
        count: userData.length
    };
}
```

This would appear in the dropdown as a selectable node that you can add to your workflow.