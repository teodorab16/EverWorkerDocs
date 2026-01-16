---
title: Business Analytics
excerpt: >-
  This section covers the analytics. monitoring and settings capabilities of the
  platform.
deprecated: false
hidden: false
icon: fad fa-square-8
metadata:
  robots: index
---
<br />

### Topics Covered:

* **Execution Analytics Dashboard**: Worker performance and usage metrics
* **Success/Failure Tracking**: Error rates and execution statistics
* **Resource Utilization**: Time tracking, cost calculation, and savings metrics
* **Logging & Debug**: Execution troubleshooting and error analysis

***

# Execution Analytics Dashboard

The central dashboard for **monitoring all Worker activity** - both Universal and AI Workflows.

### Key metrics include:

* Total Workers (created)
* Workers Used (actively interacted with)
* Utilization Rate (% of Workers in use)
* Worker Types: Universal vs. AI Workflows breakdown
* Filters: Date range, Worker type, user, tags

### Success & Failure Tracking

Track how Workers perform across executions to identify quality, stability, and reliability.

* Two-level failure metrics:
  a. **% of Workers that failed** (out of all active Workers)
  b. **% of Executions that failed** (out of all executions)
* Filterable by:
  * Worker type (Universal/Specialized)
  * Individual user
  * Execution time window
* Visualized via **stacked line charts**

### Resource Utilization & ROI

Provides business visibility into the impact and cost-effectiveness of automation.

* **Estimated Hours Saved** with Workers
* **Cost Saved**: Based on builder-provided time-per-task × hourly rate
* Driven by manual config at Worker creation level

### Debugging & Execution Logging

Deep-dive tools to trace and troubleshoot performance.

* **Execution Table View**:
  * Worker Name, Type
  * Who ran it
  * Date/time, duration
  * Status: Success / Fail
* Sortable and filterable — designed for Admins/Builders
* Used to quickly identify problem patterns (e.g., misconfigured agents, failing logic)

***

# Summary

EverWorker’s analytics and monitoring tools give both **business and technical users** what they need: from high-level automation impact and usage trends to low-level debugging and system health. Designed for **clarity, drill-down, and operational awareness**, the platform's analytics unlock both ROI insights and engineering precision.
