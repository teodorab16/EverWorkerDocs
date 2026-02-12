---
title: ● Run AI Workflow
excerpt: >-
  Execute another workflow with specific inputs, enabling modular
  workflow composition and task delegation to specialized components.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Execute another workflow with specific inputs, enabling modular workflow composition and task delegation to specialized components.

# When to Use

Use this node to delegate specific tasks to other workflows, create modular workflow compositions, or when you need to execute reusable sub-workflows with different parameters.

# Parameters

<br />

* workerId (required) - ID of the workflow to execute
  * Examples: "email-sender-workflow", "data-processor", `{{0.selectedWorker}}`
* inputParams (optional) - Parameters to pass to the workflow
  * Examples: `{"userId": "123"}`, `{{previousNode.result.parameters}}`
* inheritSession (optional) - Whether the workflow should inherit parent session context
  * Default: false
  * Examples: true, false
* parameterMapping (optional) - Optional mapping to transform input parameters to the workflow's expected format
  * Examples:
    * `{ "age": "inputParams.userAge", "name": "inputParams.userName" }`
    * `{ "userId": { "source": "inputParams", "path": "id" } }`

# Usage Example

```json
{
    name: "Call Email Workflow",
    description: "Run AI Workflow Node - delegate email sending to a workflow",
    nodeId: "n",
    operationReference: {
        methodId: "worker_call"
    },
    parameters: [
        {
            name: "workerId",
            value: "email-notification-sender" // Workflow ID
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
