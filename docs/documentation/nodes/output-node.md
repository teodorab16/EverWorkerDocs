---
title: ● Output Node
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Final output with resolved parameters. This node extracts specific field values from the output of any other node and serves as the final output point of your worker.

# When to Use

Use this node as the final node in your workflow to define exactly what data should be returned to the user. Essential for presenting clean, structured results from complex workflows.

# Parameters

* result (required) - The final result to output from the worker
  * Example: `{{previousNode.result}}`
  * Example: `{{1.result.summary}}`
  * Example: `{{2.result.data.items}}`

# Raw Usage Example
