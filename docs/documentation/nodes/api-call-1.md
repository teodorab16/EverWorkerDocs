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

<Callout icon="⚠️" theme="warn">
  **Important**: This node requires a globalId to be set in the operationReference for provider authentication:
</Callout>

```json
operationReference: {
    methodId: "standard_api_call",
    globalId: "your-provider-global-id", // Required for authentication
    providerId: "your-provider-id" // Also required if globalId present
}
```

# Parameters

<br />

* url (required) - Full URL of the API endpoint, INCLUDING path parameters and query parameters
  * Examples: https://api.openai.com/v1/chat/completions
* method (required) - HTTP method to use
  * Examples: "GET", "POST", "PUT", "DELETE"
* headers (optional) - HTTP headers as JSON object
  * Default: `{"Content-Type": "application/json"}`
    * Examples:
      * `{"Content-Type": "application/json"}`
      * `{"Authorization": "Bearer token"}`
* body (optional) - Request body data (for POST/PUT requests)
  * Examples:
    * `{"name": "value"}`
    * `{{previousNode.result.data}}`

# Raw Usage Example

```json
{
    name: "Fetch User Data", 
    description: "API Call Node - retrieve user information from external service",
    nodeId: "n",
    operationReference: {
        methodId: "standard_api_call",
        globalId: "my-api-provider", // Required for provider authentication
        providerId: "my-provider-123"
    },
    parameters: [
        {
            name: "url",
            value: "https://jsonplaceholder.typicode.com/users/1?include=[name,age]" // Fully built URL including parameters!
        },
        { name: "method", value: "GET" }, // HTTP GET request
        {
            name: "headers", 
            value: {"Accept": "application/json"} // Request headers
        }
    ]
}
```

# Capabilities

* All HTTP methods (GET, POST, PUT, DELETE, etc.)
* Custom headers and authentication
* Path parameter substitution
* JSON and form data payloads
* Response parsing and error handling

# Advanced Features

* Dynamic path parameter substitution
* Query string building from arrays/objects
* Response caching and retry logic
* Error handling with status code checks

# Result Access

`{{nodeId.result.data}}` - Response data/body (**Always run the node first to see actual output structure!**)
`{{nodeId.result.status}}` - HTTP status code
`{{nodeId.result.headers}}` - Response headers
