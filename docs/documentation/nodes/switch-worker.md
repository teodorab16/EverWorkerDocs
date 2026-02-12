---
title: ● Route Workflow
excerpt: >-
  Evaluate conditions and execute different workflows based on the result.
  Routes execution to different workflows using switch/case logic.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Evaluate conditions and execute different workflows based on the result. Routes execution to different workflows using switch/case logic.

# When to Use

Use this node when you need to execute different workflows based on conditional logic, similar to switch/case statements in programming languages.

# Parameters

* switchValue (required) - Value to switch on
  * Example: `{{condition_value}}`
* cases (required) - Array of case definitions
  * Example: `[{ "value": "case1", "workerId": "workflow-1", "inputParams": {}, "break": true, "parameterMapping": null }, { "value": "case2", "workerId": "workflow-2", "inputParams": {}, "break": true, "parameterMapping": null }]`
* defaultCase (optional) - Default case if no matches found
  * Example: `{"workerId": "default-workflow", "inputParams": {}, "parameterMapping": null}`
* inheritSession (optional) - Whether sub-workflows inherit parent session
  * Default: false
