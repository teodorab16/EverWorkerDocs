---
title: ● Browser
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Browser automation capabilities for complex web interactions, form filling, and dynamic content extraction.

# When to Use

Use when you need to execute reusable custom code logic that has been saved as a code node in the collection. Perfect for complex business logic that can't be expressed through standard nodes.

# Parameters

* browserProgram (required) - Instructions for browser automation
  * Type: textarea
  * Default: "Navigate to [https://example.com](https://example.com) and extract the main content"
* enableProxy (optional) - Enable proxy usage
  * Type: boolean
  * Default: false
* sessionTtl (optional) - Session time-to-live
  * Default: "30m"
* sessionId (optional) - Specific session ID to use
  * Default: null
