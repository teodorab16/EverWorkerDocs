---
title: ● Until Worker
excerpt: Iterative execution node that runs until a condition becomes true
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Iterative execution until condition becomes true. Repeatedly executes a sub-worker until a specified condition becomes true, maintaining state between iterations with safe merge support.

# When to Use

Use this node for polling operations, convergence algorithms, retry logic, or any scenario requiring repeated execution until a goal is achieved. Perfect for API status checks, data processing until completion, or iterative refinement processes. The safe merge feature makes it ideal when you need to pass both evolving state and constant configuration to sub-workers.

# Parameters

* workerId (required) - ID of the worker to execute repeatedly
  * Examples: "data-processor-worker", "api-checker-worker"
* initialState (required) - Starting state for the first iteration. Constants here persist across ALL iterations via safe merge.
  * Examples:
    * `{"count": 0, "apiKey": "xyz123", "results": []}`
    * `{"url": "https://api.com", "retries": 0, "maxRetries": 3}`
* condition (required) - Termination condition - when this becomes true, the loop stops
  * Examples:
    * Simple: `{"property": "count", "operator": "gte", "value": 10}`
    * Logical: `{"operator": "and", "conditions": [...]}`
    * Custom: `{"type": "custom", "checkWorkerId": "condition-worker"}`
* stateParamName (optional) - Parameter name used to pass current state to sub-worker
  * Default: "state"
  * Examples: "state", "currentData", "iterationState"
* maxIterations (optional) - Maximum number of iterations before forced termination
  * Default: 100
  * Examples: 100, 50, 1000
* iterationDelay (optional) - Milliseconds to wait between iterations (useful for rate limiting)
  * Default: 0
  * Examples: 0, 1000, 5000
* inheritSession (optional) - Whether sub-worker inherits the parent session
  * Default: false
* errorMode (optional) - How to handle sub-worker errors
  * Default: "strict" (fail immediately)
  * Options: "strict", "safe" (continue)
* parameterMapping (optional) - Map state fields to specific sub-worker parameters
  * Examples:
    * `{"apiKey": "state.apiKey", "currentCount": "state.count"}`
    * `{"url": "state.baseUrl", "iteration": "__untilIteration"}`

# Usage Example

```json
{
    name: "API Status Checker", 
    description: "Poll an API until job completion, preserving constants",
    nodeId: "3",
    operationReference: {
        methodId: "until_worker"
    },
    parameters: [
        {
            name: "workerId",
            value: "api-status-checker" // Worker that checks API status
        },
        {
            name: "initialState",
            value: {
                url: "https://api.example.com/job/123",
                apiKey: "xyz123", 
                timeout: 30000,
                status: "pending"
            } // Constants (url, apiKey) persist; status gets updated
        },
        {
            name: "condition",
            value: {"property": "status", "operator": "equals", "value": "completed"} // Stop when status becomes completed
        },
        { name: "maxIterations", value: 10 }, // Safety limit
        { name: "iterationDelay", value: 5000 }, // 5 second delay between checks
        {
            name: "parameterMapping",
            value: {"url": "state.url", "apiKey": "state.apiKey"} // Map constants to sub-worker parameters
        }
    ]
}
```

# Capabilities

* Iterative execution until condition is met
* Three condition types: Simple, Logical (AND/OR), Custom worker-based
* State preservation and evolution across iterations
* Safe merge: initial constants persist automatically
* Session inheritance and parameter mapping
* Memory and timeout safeguards
* Configurable iteration delays and error handling

# Advanced Features

* Safe Merge: Initial constants automatically preserved across iterations
* Condition Types: Simple property checks, complex AND/OR logic, custom worker validation
* Valid Operators: equals, gte, lte, gt, lt, ne
* Parameter Mapping: Transform state into sub-worker input parameters
* Special Variables: __untilIteration provides current iteration number
* Error Handling: Strict mode (fail fast) or safe mode (skip errors)
* Memory Safeguards: Automatic memory usage monitoring and warnings
* Session Management: Optional session inheritance for stateful sub-workers

# Result Access

`{{nodeId.finalState}}` - Access the final state after condition is met
`{{nodeId.iterations}}` - Number of iterations executed
`{{nodeId.conditionMet}}` - Boolean indicating if condition was satisfied
`{{nodeId.terminationReason}}` - Why the loop ended (condition_met, max_iterations, etc.)
`{{nodeId.executionTimeMs}}` - Total execution time in milliseconds