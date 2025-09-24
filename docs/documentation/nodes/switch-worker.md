---
title: ● Switch Worker
excerpt: >-
  A node used for a conditional execution based on switch/case logic. Executes
  different workers based on the value of a switch expression.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Conditional execution based on switch/case logic. Executes different workers based on the value of a switch expression.

# When to Use

Use this node when you need to execute different workflows based on conditional logic, similar to switch/case statements in programming languages.

# Parameters

* switchValue (required) - Value to switch on
  * Example: `{{condition_value}}`
* cases (required) - Array of case definitions
  * Example: `[{ "value": "case1", "workerId": "worker-1", "inputParams": {}, "break": true, "parameterMapping": null }, { "value": "case2", "workerId": "worker-2", "inputParams": {}, "break": true, "parameterMapping": null }]`
* defaultCase (optional) - Default case if no matches found
  * Example: `{"workerId": "default-worker", "inputParams": {}, "parameterMapping": null}`
* inheritSession (optional) - Whether sub-workers inherit parent session
  * Default: false