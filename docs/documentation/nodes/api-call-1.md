---
title: API Call
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Standard API call functionality for HTTP requests to external services and integrations. Supports all standard HTTP methods with flexible parameter handling and authentication.

# When to Use

Use this node to integrate with external APIs, fetch data from web services, or send data to third-party systems. Essential for connecting your workflow to external data sources and services. Always run a test to see the output structure before connecting to other nodes.

<Callout icon="⚠️">
  **Important**: This node requires a globalId to be set in the operationReference for provider authentication:
</Callout>

```json
operationReference: {
    methodId: "standard_api_call",
    globalId: "your-provider-global-id", // Required for authentication
    providerId: "your-provider-id" // Also required if globalId present
}
```

<br />
