---
title: ● Run AI Worker
excerpt: >-
  Prompt an AI Worker with your input and receive its response,
  enabling dynamic AI-powered interactions within workflows.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Prompt an AI Worker with your input and receive its response. AI Workers are conversational AI agents with tool-calling capabilities, enabling dynamic interactions and complex task delegation.

> **Note:** This is different from the Run AI Workflow node which executes AI Workflows. Use this node when you want to call conversational AI agents.

# When to Use

Use this node to integrate AI conversational agents into your workflows, delegate tasks to AI Workers with tool-calling capabilities, or when you need dynamic AI-powered decision making and processing within an AI Workflow.

# Parameters

<br />

* workerId (required) - ID of the AI Worker to execute
  * Examples: `chatbot-assistant`, `ai-analyzer`, `{{0.selectedAIWorker}}`
* userPrompt (required) - User message/prompt to pass to the AI Worker
  * Examples:
    * `Analyze this data and provide insights`
    * `{{0.userInput}}`
    * `{{previousNode.result.generatedPrompt}}`
* sessionId (optional) - Session ID for conversation continuity (null = new session, string = continue existing)
  * Examples: `null`, `{{1.result.sessionId}}`
* messageHistoryLimit (optional) - Number of previous messages to include in conversation context
  * Default: 10
  * Examples: `10`, `20`
* maxWaitTime (optional) - Maximum time in seconds to wait for AI Worker response
  * Default: 30
  * Examples: `30`, `60`, `120`
* bypassCache (optional) - Whether to bypass template cache and force fresh worker execution
  * Default: false
  * Examples: `true`, `false`

# Capabilities

* Execute any AI Worker
* Pass user prompt to AI Workers
* Session context inheritance for conversation history (enabled by default)
* Multi-turn conversation support
* Error handling and result capture

# Result Access Patterns

* `{{nodeId.result.content}}` - AI response text
* `{{nodeId.result.sessionId}}` - Session ID for conversation continuity
* `{{nodeId.result.executionId}}` - Execution ID for tracking

# Usage Example

```json
{
    name: "Multi-turn Conversation",
    description: "Run AI Worker Node - multi-turn conversation with session continuity",
    nodeId: "n",
    operationReference: {
        methodId: "universal_worker_call"
    },
    parameters: [
        {
            name: "workerId",
            value: "ai-assistant-worker" // AI Worker ID
        },
        {
            name: "userPrompt",
            value: "{{0.userInput}}" // User prompt from input node
        },
        {
            name: "sessionId",
            value: "{{1.result.sessionId}}" // Continue from previous conversation (or null for new)
        },
        {
            name: "messageHistoryLimit",
            value: 10 // Include last 10 messages
        },
        {
            name: "maxWaitTime",
            value: 30 // Wait up to 30 seconds for response
        }
    ]
}
```

<br />
