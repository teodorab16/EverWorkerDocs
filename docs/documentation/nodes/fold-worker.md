---
title: ● Fold Worker
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Sequential accumulator processing that processes an array sequentially using a sub-worker, accumulating results into a single value (reduce/fold pattern).

# When to Use

Use this node for sequential data aggregation, calculations that build upon previous results, or any reduce/fold operation. Perfect for summing values, building reports, accumulating statistics, or processing ordered data where each step depends on the previous result. The safe merge feature makes it ideal when you need persistent configuration (API keys, formatting options) alongside evolving calculations.

# Parameters

* arrayInput (required) - Array of items to process sequentially
  * Examples:
    * `[1, 2, 3, 4, 5]`
    * `[{id: 1}, {id: 2}]`
    * `{{previous_node.items}}`
* workerId (required) - ID of the worker to execute for each item
  * Examples: "data-aggregator", "sum-calculator", "report-builder"
* initialAccumulator (required) - Starting accumulator value. Constants here persist across ALL iterations via safe merge.
  * Examples:
    * `{"sum": 0, "apiKey": "xyz123", "format": "json"}`
    * `{"total": 0, "baseUrl": "https://api.com", "results": []}`
    * `{}`
* accumulatorParamName (optional) - Parameter name used to pass current accumulator to sub-worker
  * Default: "accumulator"
  * Examples: "accumulator", "total", "result"
* itemParamName (optional) - Parameter name used to pass current item to sub-worker
  * Default: "item"
  * Examples: "item", "current", "data"
* inheritSession (optional) - Whether sub-workers inherit the parent session context
  Default: false
* errorMode (optional) - How to handle sub-worker errors
  * Default: "strict" (stop on error)
  * Options: "strict", "safe" (skip and continue)
* earlyTermination (optional) - Optional condition to stop processing before all items are done
  * Example: `{"enabled": true, "checkProperty": "sum", "exitValue": 1000}`
* accumulatorLimits (optional) - Memory limits and check intervals for large accumulator monitoring
  * Example: `{"maxSizeBytes": 52428800, "memoryCheckInterval": 10}`
* parameterMapping (optional) - Map accumulator and item fields to specific sub-worker parameters
  * Examples:
    * `{"currentSum": "accumulator.sum", "value": "item.amount", "apiKey": "accumulator.apiKey"}`
    * `{"total": "accumulator", "data": "item"}`

# Usage Example

```json
{
    name: "Calculate Invoice Total with Fees",
    description: "Sum invoice line items while preserving tax rate and API credentials",
    nodeId: "2",
    operationReference: {
        methodId: "fold_worker"  
    },
    parameters: [
        {
            name: "arrayInput",
            value: "{{1.invoiceItems}}" // Array of invoice line items
        },
        {
            name: "workerId",
            value: "line-item-calculator" // Worker that calculates item totals
        },
        {
            name: "initialAccumulator", 
            value: {
                total: 0,
                taxRate: 0.08, 
                currency: "USD",
                apiKey: "invoice-api-123",
                fees: []
            } // Constants (taxRate, currency, apiKey) persist; total and fees evolve
        },
        {
            name: "parameterMapping",
            value: {
                currentTotal: "accumulator.total",
                taxRate: "accumulator.taxRate", 
                apiKey: "accumulator.apiKey",
                lineItem: "item"
            } // Map constants and evolving data to sub-worker parameters
        },
        { name: "errorMode", value: "safe" }, // Continue if individual items fail
        {
            name: "earlyTermination",
            value: {"enabled": true, "checkProperty": "total", "exitValue": 10000} // Stop if total exceeds limit
        }
    ]
}
```

# Capabilities

* Sequential array processing with accumulation pattern
* Safe merge: initial constants preserved automatically across iterations
* Early termination based on accumulator property values
* Memory monitoring and overflow protection
* Error handling modes: strict (fail-fast) or safe (continue)
* Parameter mapping to transform accumulator/item data
* Session inheritance and custom parameter naming
* Progress tracking with detailed result statistics

# Advanced Features

* Safe Merge: Initial constants automatically preserved across all iterations
* Early Termination: Stop processing based on accumulator property conditions
* Memory Safeguards: Automatic monitoring and warnings for large accumulators
* Error Recovery: Safe mode allows skipping failed items while preserving accumulator
* Parameter Mapping: Transform accumulator and item data for sub-worker compatibility
* Progress Tracking: Detailed statistics on processing success and failures
* Custom Parameter Names: Configure how accumulator and items are passed to sub-workers
* Session Management: Optional session inheritance for stateful sub-workers

# Result Access

`{{nodeId.finalAccumulator}}` - Access the final accumulated result
`{{nodeId.processedItems}}` - Number of items successfully processed
`{{nodeId.totalItems}}` - Total number of items in the input array
`{{nodeId.skippedItems}}` - Number of items skipped due to errors
`{{nodeId.memoryWarnings}}` - Count of memory usage warnings
