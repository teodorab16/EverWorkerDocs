---
title: ● Worker Call
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Execute a single sub-worker with parameters, enabling modular workflow composition and task delegation to specialized components.

# When to Use

Use this node to delegate specific tasks to specialized workers, create modular workflows, or when you need to execute reusable sub-processes with different parameters.

# Parameters

<br />

* workerId (required) - ID of the specialized worker to execute
  * Examples: "email-sender-worker", "data-processor", `{{0.selectedWorker}}`
* inputParams (optional) - Parameters to pass to the sub-worker
  * Examples: `{"userId": "123"}`, `{{previousNode.result.parameters}}`
* inheritSession (optional) - Whether sub-worker should inherit parent session context
  * Default: false
  * Examples: true, false
* parameterMapping (optional) - Optional mapping to transform input parameters to sub-worker expected format
  * Examples:
    * `{ "age": "inputParams.userAge", "name": "inputParams.userName" }`
    * `{ "userId": { "source": "inputParams", "path": "id" } }`

# Usage Example

```json
{
    name: "Call Email Worker",
    description: "Worker Call Node - delegate email sending to specialized worker",
    nodeId: "n",
    operationReference: {
        methodId: "worker_call"
    },
    parameters: [
        {
            name: "workerId", 
            value: "email-notification-sender" // Email worker ID
        },
        {
            name: "inputParams",
            value: {"recipient": "{{0.userEmail}}", "template": "welcome"} // Email parameters
        },
        { name: "inheritSession", value: true } // Maintain context
    ]
}
```

<br />
