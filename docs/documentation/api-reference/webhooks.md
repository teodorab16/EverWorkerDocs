---
title: Webhooks
excerpt: >-
  Configure webhooks to trigger AI Workers and AI Workflows from external
  systems
deprecated: false
hidden: false
icon: 🪝
metadata:
  robots: index
---

Webhooks allow external systems to trigger AI Workers and AI Workflows via HTTP POST requests. This enables seamless integration with third-party applications, automation platforms, and custom systems.

***

# Overview

A webhook in EverWorker is a unique URL endpoint that, when called, executes one or more workers with the provided payload data. Key features include:

* **Multiple Workers**: Execute multiple workers per webhook (sequentially or in parallel)
* **Flexible Authentication**: Five authentication methods to match your security requirements
* **Two Execution Modes**: Synchronous (wait for results) or asynchronous (immediate response)
* **Custom Headers**: Configure custom header names and prefixes for authentication
* **Call Statistics**: Track usage with call counts and timestamps

***

# Creating a Webhook

To create a webhook:

1. Navigate to **Settings** > **Webhooks**
2. Click **Create Webhook**
3. Configure the webhook:
   * **Name**: A descriptive name for the webhook
   * **Description**: Optional description of its purpose
   * **Workers**: Select one or more AI Workers or AI Workflows to execute
   * **Authentication Method**: Choose how external systems authenticate
   * **Execution Mode**: Sync (wait for results) or Async (immediate response)
4. Click **Create**
5. **Important**: Copy the generated secret immediately - it will only be shown once

After creation, you'll receive:
* **Webhook URL**: `https://your-domain.everworker.ai/api/v1/webhooks/wh_xxxxx`
* **Secret**: Used for authentication (store securely)

***

# Authentication Methods

EverWorker webhooks support five authentication methods:

### Secret Header (Recommended for simplicity)

Send a secret value in a header. Default header: `X-Webhook-Secret`

```bash
curl -X POST https://your-domain.everworker.ai/api/v1/webhooks/wh_xxxxx \
  -H "Content-Type: application/json" \
  -H "X-Webhook-Secret: your-webhook-secret" \
  -d '{"message": "Hello from external system"}'
```

### HMAC Signature (Recommended for security)

GitHub/Stripe-style HMAC-SHA256 signature validation. Default header: `X-Webhook-Signature`

```bash
# Generate signature
SIGNATURE=$(echo -n '{"message":"Hello"}' | openssl dgst -sha256 -hmac "your-secret" | cut -d' ' -f2)

curl -X POST https://your-domain.everworker.ai/api/v1/webhooks/wh_xxxxx \
  -H "Content-Type: application/json" \
  -H "X-Webhook-Signature: sha256=$SIGNATURE" \
  -d '{"message":"Hello"}'
```

### Bearer Token

OAuth-style bearer token authentication. Default header: `Authorization`

```bash
curl -X POST https://your-domain.everworker.ai/api/v1/webhooks/wh_xxxxx \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-webhook-secret" \
  -d '{"message": "Hello from external system"}'
```

### API Key

API key authentication. Default header: `X-API-Key`

```bash
curl -X POST https://your-domain.everworker.ai/api/v1/webhooks/wh_xxxxx \
  -H "Content-Type: application/json" \
  -H "X-API-Key: your-webhook-secret" \
  -d '{"message": "Hello from external system"}'
```

### Custom Header

Use your own header name for authentication.

```bash
curl -X POST https://your-domain.everworker.ai/api/v1/webhooks/wh_xxxxx \
  -H "Content-Type: application/json" \
  -H "X-My-Custom-Auth: your-webhook-secret" \
  -d '{"message": "Hello from external system"}'
```

***

# Execution Modes

### Synchronous Mode

The webhook waits for all workers to complete and returns the full results.

**Use when:**
* You need the worker's response immediately
* Your external system can wait for execution
* You want atomic behavior (all-or-nothing)

**Response (200):**
```json
{
  "success": true,
  "webhookId": "wh_xxxxx",
  "timestamp": "2025-01-15T12:00:00Z",
  "executionMode": "sync",
  "results": [
    {
      "workerId": "worker-123",
      "executionId": "exec-abc123",
      "success": true,
      "promptTokens": 1500,
      "result": {
        "role": "assistant",
        "content": "Worker response here..."
      }
    }
  ]
}
```

### Asynchronous Mode

The webhook starts executions and returns immediately with execution IDs.

**Use when:**
* Your external system cannot wait for long-running tasks
* You want to start multiple workers in parallel
* You'll poll for results separately

**Response (202):**
```json
{
  "success": true,
  "webhookId": "wh_xxxxx",
  "timestamp": "2025-01-15T12:00:00Z",
  "executionMode": "async",
  "results": [
    {
      "workerId": "worker-123",
      "executionId": "exec-abc123",
      "success": true
    }
  ]
}
```

To retrieve results later, use the [Get Execution Result](/docs/api-reference#get-execution-result) endpoint with the `executionId`.

***

# Request Format

Send a POST request with a JSON body. The body content is passed directly to the workers as `inputParams`.

```bash
POST /api/v1/webhooks/wh_xxxxx
Content-Type: application/json
X-Webhook-Secret: your-secret

{
  "userMessage": {
    "role": "user",
    "content": "Process this request from the external system"
  },
  "customData": {
    "orderId": "12345",
    "customerEmail": "user@example.com"
  }
}
```

The JSON structure depends on what your workers expect as input parameters.

***

# Response Status Codes

| Status | Description |
|--------|-------------|
| 200 | Sync mode: All workers executed successfully |
| 202 | Async mode: Executions started in background |
| 400 | Invalid webhook ID or malformed request |
| 401 | Authentication failed (invalid secret/signature) |
| 403 | Webhook is inactive |
| 404 | Webhook not found |
| 429 | Rate limit exceeded |
| 500 | Sync mode: One or more workers failed |

***

# Managing Webhooks

### View Webhook Secret

If you need to retrieve your webhook secret:

1. Go to **Settings** > **Webhooks**
2. Click the **View Secret** button on the webhook
3. The secret will be displayed (requires authorization)

### Regenerate Secret

To generate a new secret (invalidates the old one):

1. Go to **Settings** > **Webhooks**
2. Click the **Regenerate Secret** button
3. Copy the new secret immediately
4. Update your external systems with the new secret

### Test a Webhook

Use the built-in test feature:

1. Go to **Settings** > **Webhooks**
2. Click **Test** on the webhook
3. Edit the test payload if needed
4. Click **Execute Test**
5. View the response in the modal

The test modal also provides a ready-to-use cURL command.

### Deactivate a Webhook

Toggle the **Active** status to temporarily disable a webhook without deleting it.

***

# Use Cases

### CRM Integration
Trigger an AI Worker when a new lead is created in your CRM to automatically research and enrich the lead data.

### E-commerce Automation
Execute an AI Workflow when an order is placed to generate personalized thank-you emails or process refund requests.

### Support Ticket Processing
Automatically categorize and route support tickets by triggering an AI Worker when tickets are created in your helpdesk.

### Scheduled Reports
Connect with scheduling services to trigger report generation workflows at specific intervals.

### IoT and Monitoring
Trigger analysis workflows when sensors or monitoring systems detect anomalies.

***

# Security Best Practices

1. **Use HMAC Signature** for production integrations - it provides the strongest security by validating the entire request body
2. **Store secrets securely** - never commit webhook secrets to version control
3. **Rotate secrets periodically** - use the regenerate feature to create new secrets
4. **Use HTTPS only** - webhook URLs are always HTTPS
5. **Validate in your system** - verify webhook responses match expected formats
6. **Monitor usage** - check call statistics to detect unusual patterns

***

# Rate Limiting

Webhooks respect the platform's rate limits:

* Global rate limits apply
* Per-user rate limits are enforced
* Per-model rate limits for LLM operations

When rate limited, the webhook returns a `429` status code. Implement retry logic with exponential backoff in your external systems.