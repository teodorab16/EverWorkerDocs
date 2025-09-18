---
title: + Input Node
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Entry point for data input with enhanced field types for rich user interfaces. This node should typically be the first node in workflows that require user-provided parameters.

# When to Use

Use this node as the first node when you need to collect input from the user before processing. Essential for interactive workflows that require user-provided data, parameters, or file uploads.

# Parameters

* userMessage (optional) - Text input from the user
  * Type: textarea
  * Placeholder: "Enter your message or question..."
  * Example: "Hi, this is John"
* uploadedFile (optional) - File uploaded by the user (returns buffer data)
  * Type: file
  * Placeholder: "Upload a document for processing (optional)"
  * Returns buffer data for downstream processing

# Raw Usage Example

![](https://files.readme.io/8066fe858cf65d5f1d294fb919d7b076cdbd283654ef3c485b48adfd1813e83c-image.png)

<br />

# Capabilities

* Standard text input
* Multi-line text input for longer content
* Numeric input with validation
* Dropdown selection with data sources
* File upload that returns buffer data

# Advanced Features

* Enhanced field types (text, textarea, number, select, file)
* Validation rules (required, min/max, patterns)
* Data sources for dropdowns (memory, workers, static options)
* File type restrictions with accept patterns
* Placeholder text and help descriptions

# Result Access

* `{{0.parameterName}}` - Access any defined parameter by name
* `{{0.userMessage}}` - Common pattern for user input
* `{{0.uploadedFile}}` - Access uploaded file data