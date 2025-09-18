---
title: 10. Observatory
deprecated: false
hidden: false
metadata:
  robots: index
---
<br />

This section covers the internal observability system used to monitor platform activity, troubleshoot issues, and manage multi-tenant deployments.

**Observatory** enables full visibility into logs, system metrics, and customer-level configurations across all licensed instances, and is designed exclusively for internal use — not visible to end users or customers.

# Topics covered

* **Customer-App-Instance Hierarchy**: Scoped navigation and access structure
* **Log Monitoring**: Execution and system logs with filters and JSON detail
* **Performance Dashboard**: Visual metrics on logs, modules, and system behavior
* **System Monitoring**: CPU, memory, session tracking (optional per app)
* **Log Cleanup Configuration**: Retention rules and aggregation controls
* **Remote Logging & Client-Side Logging**: Toggle and manage data flow
* **App & Customer Management**: Creation, update, and license assignment

***

# Purpose

Observatory provides multi-tenant visibility into the operations of all registered apps under a customer’s license. It allows for:

* Log monitoring and filtering
* Execution statistics and error tracking
* System status and performance cleanup configuration
* Admin-level setup and license-based scoping

# Key Components

1. ## Customer → App → Instance Cascade
   * Users must first select a **Customer**, then choose an **App**, and finally an **Instance** (license/deployment)
   * Only after an instance is selected do **Logs, Dashboard**, and **Settings** become visible
   * Enables scoped monitoring for multi-instance deployments
2. ## Logs Tab
   Provides a detailed table of **system and execution logs**.
   * Filter by: log level, user, time range, and instance
   * View full metadata (timestamp, IP, module, message, structured data)
   * Supports JSON expansion and export for debugging
   * Error types tracked: INFO, WARN, ERROR, DEBUG, TRACE
3. ## Dashboard Tab
   A visual summary of app and system performance over time.
   * Key Metrics:
     * Total Logs
     * Error Rate (%)
     * Average Logs/Day
     * Active Modules
   * Includes:
     * Log levels over time
     * Top emitting modules
     * Live System Monitoring (CPU, memory, session count)
4. ## Settings Tab
   Configure system behavior at the app level.
   * **Log Cleanup**:
     * Retention hours (e.g., delete TRACE logs after 48h)
     * Enable automatic cleanup
     * Aggregation interval (e.g., hourly averages)
   * **System Monitoring**:
     * Enable/disable
     * Set collection interval (e.g., 30s)
   * **Core Settings**:
     * Log level control
     * Client-side logging toggle
     * Remote logging control (to centralized hub)
5. ## Management View
   Used to:
   * Create new customers and apps
   * Assign admin emails, domains, and app IDs
   * Track creation date and license linkage
   * Modify or delete apps

***

# Summary

Observatory enables deep operational transparency across the EverWorker platform. With scoped customer-app-instance navigation, detailed logs, cleanup automation, and performance dashboards, it gives Admins full control over health, debugging, and governance — especially in complex, multi-tenant environments.
