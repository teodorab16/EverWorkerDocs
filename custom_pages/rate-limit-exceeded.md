---
title: >-
  KB003: Rate limit exceeded (429) — causes, limits, and how to request an
  increase
fullscreen: false
hidden: false
---
This article explains what causes `429 Rate limit exceeded` errors, the current platform limits, how to design workflows that stay within them, and how to request a limit increase.

<br />

# Issue description

An execution, API call, or sub-worker call fails with a `429` error. Common signatures:

API response:

```json
{
  "ok": false,
  "status": 429,
  "statusText": "Rate limit exceeded",
  "error": "Rate limit exceeded – retry later [429]"
}
```

Inside a `Run AI Workflow` or `Run AI Worker` node, the same failure surfaces in node results:

```json
{
  "ok": false,
  "status": 500,
  "statusText": "Sub-worker execution failed",
  "error": "Rate limit exceeded – retry later [429]",
  "nodeId": 12
}
```

The error is most commonly seen when running batches of leads in parallel (SDR-type agents), processing inbound webhooks at high frequency (Clay, Zapier, custom apps), or when scheduled and manual runs overlap.

# Cause

EverWorker enforces platform-wide rate limits to protect deployment stability and ensure fair allocation across users. When any limit is exceeded, the request is **rejected immediately** with `429`. The platform does **not** queue or auto-retry overflow requests.

Limits are evaluated per **rolling 60-second window**.

| Limit | Default | What it counts |
|-------|---------|----------------|
| **Max concurrent executions** | 30 | AI Workers, AI Workflows, and sub-workers running **at the same time** across the entire deployment. Sub-workers count toward the same pool as their parents. |
| **Per-user requests / minute** | 60 | API requests and execution starts initiated by a single user (or a single API token). |
| **Global requests / minute** | 800 | Total API requests and execution starts across all users in the deployment. |
| **Per-provider requests / minute** | 600 | Calls routed to a single LLM provider (e.g. OpenAI, Anthropic, Google). |

Three notes:

1. **LLM providers and external APIs enforce their own limits** in addition (OpenAI, Anthropic, Salesforce, HubSpot, Clay, etc.). A `429` returned from a downstream LLM call is separate from the platform limits above.
2. **Retries count.** Every execution start consumes capacity, including retries triggered by your own logic.
3. **Scheduled and manual runs share the same pool.** There is no separate quota for scheduled vs. on-demand executions.

# Solution

## A. Diagnose which limit you hit

Check the orchestrator health endpoint to see current concurrent activity:

```bash
curl -H "Authorization: bearer <token>" \
  https://<account>.everworker.ai/api/v1/agents/health
```

Look at `orchestrator.activeExecutions` and `orchestrator.maxConcurrentExecutions`. If `activeExecutions` is at or near the max when the `429` occurred, you're hitting the **concurrent executions** limit. If it's well below, the failure is likely from the per-user or per-provider per-minute limit.

## B. Design the workflow to stay within limits

Most rate-limit issues fall into one of three patterns:

**1. High-volume batch processing (e.g. SDR over thousands of leads)**

* Cap parallelism inside `Repeat Workflow` to a value below the concurrent-execution limit, leaving headroom for other workflows running on the deployment.
* Process in **batches** rather than firing all leads at once. A batch of 25 with a small delay between batches is far more reliable than 1,000 in parallel.
* Combine with `Repeat Workflow Until` and an `iterationDelay` to throttle sustained throughput.

**2. External webhook into EverWorker (Clay, Zapier, custom apps)**

* If the upstream sends faster than the per-user limit (60/min) allows, write incoming events into a **collection** first, then process them on a schedule with a controlled poll cadence.
* Don't process inline in the webhook handler at high volume.

**3. Tight loops calling sub-workers**

* Each `Run AI Workflow` or `Run AI Worker` call counts toward concurrent-execution capacity for the duration of the sub-workflow.
* Long-running sub-workflows (≥ 1 minute) called in parallel will drain capacity quickly. Reduce parallelism or split work across time.

## C. Add client-side retry with backoff

Because the platform does not queue, your client (or the upstream system calling EverWorker) should implement **exponential backoff** on `429` responses. A typical pattern: wait 1s on the first retry, doubling up to 30–60s, with a small random jitter, and a cap on total retries.

## D. Request a limit increase

If your workload genuinely needs higher capacity (high-volume SDR, real-time webhook processing, large-scale enrichment), limit increases are available on request.

Contact your EverWorker representative or open a support ticket with:

1. **Use case** — what workflow is hitting the limit, and why higher capacity is required.
2. **Target throughput** — peak concurrent executions, peak requests/minute, expected duration (one-off batch vs. sustained).
3. **Batch frequency** — how often you'll run at peak (daily, hourly, continuous).
4. **Latency expectations** — is this user-facing (seconds matter) or background (minutes are fine)?

Increases are evaluated against deployment capacity and your plan. Most requests can be approved within a few business days. Very large increases may require provisioning additional resources and an updated commercial agreement.