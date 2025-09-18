---
title: ● Map Worker
deprecated: false
hidden: false
metadata:
  robots: index
---
Overview



Parallel array processing with sub-workers. Processes arrays in parallel by executing a sub-worker on each element with configurable concurrency control.

# When to Use


Use this node when you need to process arrays or lists in parallel, such as bulk operations on users, processing multiple files, or sending notifications to multiple recipients.

# Parameters

* arrayInput (required) - Array of items to process in parallel
  * Examples:
    * `{{previousNode.result.items}}`
    * ` [1, 2, 3, 4, 5]`
    * `{{0.userList}}`
* workerId (required) - Worker to execute on each array element
  * Examples: "user-processor", "data-transformer", "email-sender"
* inputParamName (optional) - Parameter name for passing array element to sub-worker
  * Default: "item"
  * Examples: "item", "user", "data"
* concurrency (optional) - Maximum parallel executions (system-limited)
  * Default: 3
  * Examples: 1, 5, 10
* continueOnError (optional) - Whether to continue processing if an item fails
  * Default: false
  * Examples: true, false
* inheritSession (optional) - Whether sub-workers inherit parent session context
  * Default: false
* parameterMapping (optional) - Optional mapping to transform array items to sub-worker expected format
  * Examples:
    * `{ "userId": "item.id", "userName": "item.name" }`
    * `{ "age": { "source": "item", "path": "profile.age" } }`

# Usage Example

```json
{
    name: "Process User List",
    description: "Map Worker Node - process multiple users in parallel",
    nodeId: "n", 
    operationReference: {
        methodId: "map_worker"
    },
    parameters: [
        {
            name: "arrayInput",
            value: "{{previousNode.result.users}}" // Array of users
        },
        {
            name: "workerId", 
            value: "user-notification-sender" // Worker for each user
        },
        { name: "inputParamName", value: "user" }, // Parameter name in sub-worker
        { name: "concurrency", value: 5 }, // Process 5 users at once
        { name: "continueOnError", value: true } // Skip failed users
    ]
}
```

# Capabilities

* Parallel array element processing
* Configurable concurrency control
* Error handling strategies (fail-fast or continue)
* Progress tracking and execution metrics
* Dynamic parameter passing to sub-workers

# Advanced Features

* Automatic result aggregation with success/error counts
* Item index tracking (__mapItemIndex parameter)
* Memory-efficient processing for large arrays
* Partial success handling with detailed error reporting

# Result Access

`{{nodeId.results}}` - Array of all results
`{{nodeId.results.0.result}}` - First item result
`{{nodeId.successCount}}` - Number of successful executions
`{{nodeId.errorCount}}` - Number of failed executions
