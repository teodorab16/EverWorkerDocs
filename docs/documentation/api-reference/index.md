---
title: API reference
excerpt: This section explains how to execute agents via HTTPS API requests
deprecated: false
hidden: false
icon: fad fa-code-simple
metadata:
  robots: index
---
# Terminology

**API request** - a web request executed via application capable of sending such requests. Example include but are not limited to browsers, POSTMAN, custom programs written in any language capable of executing https-based requests. Typical request types used with EverWorker platform are POST and GET type requests. API requests consist of headers and a body in JSON format (for POST requests). Authentication is done via using tokens in one of headers.

**Token (JWT token)** - authentication secret used to impersonate a certain user in order to access the platform. Each user can create their own tokens, and administrators can see each token (but not its value) and its expiration date in Settings.

**Agent** - a specific universal or specialized worker designed in the platform. Agents (workers) are executable using API via their agentID that can be found in the URL of any agent configuration. AgentID is a unique identifier for each worker.

**Execution** - A single run of an agent. Execution and its ID is important to query status and results for a certain run that was called using API. Executions are referenced using ExecutionID that is visible in a result response to an API call to execute an agent.

**Session** - A single chat/execution context that can be followed up with further queries. You can pass SessionID (see examples below) to continue previous conversations with workers instead of starting new ones.

# Authentication and token creation

In order to be able to execute API requests towards the platform, a user must access their profile (top right corner button with a dropdown), switch to "API Tokens" tab and generate a new token with a custom name and expiration date.

Tokens can be revoked from the same interface where they are created

<Image border={false} src="https://files.readme.io/d2dc437d49bf6cdaa159da6019665cb26c275f9f09413dcbe01280e5de394bf9-image.png" />

During the token creation, you have 4 different permission types you can assign to the topic.

* `agent:execute` - allowing to use this token to execute agents (workers)
* `agent:logs` - allowing to use this token to read agent (worker) logs
* `agents:health` - allowing to use this token to view platform health
* `observatory:write` - allowing to use this token for superadmin operations not covered by this guide

Make sure to copy the token value to a secure vault/password manager/write it down, because you cannot access its value in web UI after it's created for security considerations.

In all future requests, this token will be used in headers of HTTP requests. Header name "Auhorization", header value "bearer `<token>`".

# Finding AgentID

AgentID can be found in URL of a worker.

* When you chat with an AI Worker, its URL will look like [https://agi.everworker.ai/universal/chat/FbAfoT2ecyPnFZC4K](https://agi.everworker.ai/universal/chat/FbAfoT2ecyPnFZC4K). Here `FbAfoT2ecyPnFZC4K` is AgentID.
* When you edit an AI Workflow in Canvas, its URL will look like [https://agi.everworker.ai/specialized/canvas/ofim7r2az6dxgSDte](https://agi.everworker.ai/specialized/canvas/ofim7r2az6dxgSDte). Here `ofim7r2az6dxgSDte` is AgentID.

# Finding SessionID

`SessionID` allows to continue previous conversation with an AI Worker. You can only obtain it after executing an agent at least once. The execution result will contain the sessionID. You can also set the history limit in each request to control the amount of chat history used for further executions.

For an example, check the "Execute Agent" -> "Example execution result" below.

# Base URL

HTTPS executions are called against Base URL for your organization, that looks like `account_name`.everworker.ai.  So if your account name is "test", then a target URL for a call with the URL path "api/v1/agents/health" would be `https://test.everworker.ai/api/v1/agents/health`.

<br />

# API call types

## Health Check

* URL path: `api/v1/agents/health`
* Method: `GET`
* Headers: `Authorization: bearer <token>`

Typical response:

```json
{
    "success": true,
    "data": {
        "service": "agents-api",
        "status": "healthy",
        "timestamp": "2025-09-01T01:42:33.786Z",
        "orchestrator": {
            "available": true,
            "activeExecutions": {},
            "maxConcurrentExecutions": 0
        }
    }
}
```

<br />

## Execute Agent

* URL path: `api/v1/agents/execute`
* Method: `POST`
* Header: `Authorization: bearer <token>`
* Header: `Content-Type: application/json`
* Body: `Body in JSON format with agentID, sessionID and input parameters in JSON format`

Input parameters depend on what input parameters were configured in the actual worker.

* For AI Worker, it is typically "userMessage" that consists of "role" (user) and "content".
* For AI Workflow, it will be a list of input parameters used in Input node, with the names given to them in Canvas.

"**bypassCache**" is an optional boolean that forces a fresh execution, skipping any cached result for identical inputs. If omitted or set to false, the platform may return a cached result when available.

### Example body usage when executing AI Worker.

```
{
	"agentId": "{{agentId}}",
	"sessionId": "new_session",
		"inputParams":
    {
      "userMessage":
      {
        "role": "user",
        "content": "Hello, please tell me which licenses does the user testc@everworker.ai have?"
      },
      "messageHistoryLimit": 10
    },
    "bypassCache": false
}
```

### Example execution result

```json
{
    "success": true,
    "data": {
        "sessionId": "pjk6AumJnByJrJdTQ",
        "executionId": "3b0b49e4-4b63-4a45-9d9a-bb59cece5650",
        "promptTokens": 1248
    }
}
```

From this execution result you can find two important variables:

* **SessionID** - allows you to continue this conversation in the next POST request to the same worker.
* **ExecutionID** - allows you to actually GET the execution status/result.

<br />

## Get Execution Logs

* URL path: `api/v1/execution-logs?executionId={{ExecutionId}}`
* Method: `GET`
* Header: `Authorization: bearer <token>`

Substitute `{{ExecutionID}}` with the ID returned by "Execute" POST request.

### Example execution log retrieval result

```json
{
    "success": true,
    "data": {
        "_id": "W3B6ZPGqWzy9PcASs",
        "executionStarted": "2025-09-22T07:01:19.758Z",
        "executionEnded": "2025-09-22T07:01:36.494Z",
        "nodeResults": [{
            "userMessage": {
                "role": "user",
                "content": "Hello, please tell me which licenses does the user testc@everworker.ai have?"
            },
            "messageHistoryLimit": 10
        }, {
            "ok": true,
            "result": {
                "role": "assistant",
                "content": "### Licenses for testc@everworker.ai\n\n| User (UPN) | Assigned licenses |\n|---|---|\n| test@everworker.ai | - Power BI (Free)  \n- Microsoft Power Automate Free  \n- Microsoft 365 Business Basic |",
                "refusal": null,
                "annotations": []
            },
            "nodeId": 1,
            "executionStarted": "2025-09-22T07:01:19.761Z",
            "executionFinished": "2025-09-22T07:01:36.494Z"
        }],
        "ctx": {
            "userId": "BXBH9cs77TsvhjjsH",
            "agentId": "ZbAfoT2ecydnFZC4K",
            "sessionId": "pZk6AumJnByJrJdTQ",
            "executionId": "3b0b49e4-4b63-4a45-9d9a-bb59cece5650"
        },
        "time": 16736,
        "finalResult": []
    }
}
```

From this answer in JSON format you can easily extract LLM response, as well as check other parameters, such as the amount of time it took.
