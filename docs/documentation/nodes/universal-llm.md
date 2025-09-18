---
title: ● Universal LLM
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Universal Large Language Model execution that supports any LLM vendor through a single interface. This stateless node provides universal access to OpenAI, Anthropic, Google, and other LLM providers using direct HTTP calls.

.

# When to Use

Use this node when you need a stateless, single-call LLM interaction with any vendor. Perfect for workflows that need tool_calls preserved in responses for downstream processing, or when you want direct HTTP API calls without tool execution overhead.

# Parameters

* connector (required)
  * Purpose: Specifies which LLM provider or integration connector to use for this LLM call.
  * How it Works:
    * The Universal LLM node will use this connector value to route the API request through the correct service integration.
    * If not set or set incorrectly, LLM calls will either fail or default to a platform-preferred provider, which may not match your expectations and could impact cost, performance, or availability.
* model (required) - Model name specific to the vendor
  * Placeholder: "e.g., gpt-4, claude-3-opus, gemini-pro"
  * Examples: "gpt-4", "claude-3-opus-20240229", "gemini-1.5-pro", "llama-3-70b"
* messages (required) - Chat messages in JSON format.
  * Type: textarea
  * Default: `[{"role": "system", "content": "You are a helpful assistant."}, {"role": "user", "content": "{{0.userMessage}}"}]`
* temperature (optional) - Controls randomness (min value = deterministic, max value = very creative)
  * Type: number
  * Default: 0.7
* maxTokens (optional) - Maximum tokens to generate (vendor-specific limits apply)
  * Type: number (1 - 128000)
  * Default: 4096
  * Examples: "1024", "4096", "8192"
* tools (optional) - Array of tools/functions in OpenAI format (preserved in response, not executed)
  * Type: textarea
  * Placeholder: "Tools/functions in OpenAI format (optional JSON array)"
  * Example: `[{"type": "function", "function": {"name": "search", "parameters": {...}}}]`
* responseFormat (optional) - Control output format (text, JSON, or structured with schema)
  * Type: textarea
  * Placeholder: `{"type": "json_object"}` or `{"type": "json_schema", "json_schema": {...}}`
  * Examples: `{"type": "text"}`, `{"type": "json_object"}`, `{"type": "json_schema", "json_schema": {"name": "response", "schema": {...}}}`

# Raw Usage Example

```json
{
    name: "Multi-vendor AI Assistant",
    description: "Universal LLM Node - works with any configured LLM provider",
    nodeId: "n",
    operationReference: {
        methodId: "generic_llm_universal"
    },
    parameters: [
        { name: "providerId", value: "{{select_from_providers}}" }, // Select provider
        { name: "model", value: "gpt-4" }, // Model name
        { 
            name: "messages", 
            value: "[{\"role\": \"system\", \"content\": \"You are a helpful assistant\"}, {\"role\": \"user\", \"content\": \"{{0.userMessage}}\"}]"
        }, // Chat messages
        { name: "temperature", value: 0.7 }, // Creativity level
        { name: "maxTokens", value: 2048 } // Max response length
    ]
}
```

# Capabilities

* Support for multiple LLM vendors through a single interface
* Automatic format conversion between vendors
* Tool/function calling format preservation (not execution)
* Structured output support (JSON mode and JSON schema)
* Stateless operation - no database storage
* Automatic authentication via configured providers

# Advanced Features

* Automatic vendor detection from provider configuration
* Direct HTTP calls with vendor-specific endpoints and headers
* Format conversion for all major LLM vendors
* Structured output with JSON schema (OpenAI only)
* Tool calling format normalization (preserved, not executed)
* Stateless operation for better performance and reliability
* Unified error handling and retry logic

# Result Access

`{{nodeId.result.content}}`- Generated text response
`{{nodeId.result.tool_calls}}` - Tool call requests (if any)
`{{nodeId.result}}` - Full message object

<br />
