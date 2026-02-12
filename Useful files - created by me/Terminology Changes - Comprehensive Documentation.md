# Terminology Changes - Comprehensive Documentation

> This document captures all user-facing and code-level terminology changes across the EVERWORKER platform as part of the EN-2407 initiative and related tickets. Use this as a reference for updating external documentation, help articles, API docs, and user guides.

---

## Table of Contents

1. [Summary of Terminology Mapping](#1-summary-of-terminology-mapping)
2. [PR #1568 — Universal Worker → AI Worker](#2-pr-1568--universal-worker--ai-worker)
3. [PR #1569 — Specialized Workers → AI Workflows](#3-pr-1569--specialized-workers--ai-workflows)
4. [PR #1778 — Code Node → Custom Node](#4-pr-1778--code-node--custom-node)
5. [PR #1483 — Failed Workers → Failed Worker Runs](#5-pr-1483--failed-workers--failed-worker-runs)
6. [EN-2407 — Canvas Node Names, Descriptions & i18n](#6-en-2407--canvas-node-names-descriptions--i18n)
7. [EN-2824 — Analytics Page Terminology (Unmerged)](#7-en-2824--analytics-page-terminology-unmerged)
8. [i18n Keys Reference](#8-i18n-keys-reference)
9. [New Enums and Types](#9-new-enums-and-types)
10. [Files Changed Summary](#10-files-changed-summary)

---

## 1. Summary of Terminology Mapping

### Core Renames

| Old Term | New Term | Scope | Status |
|----------|----------|-------|--------|
| **Universal Worker** | **AI Worker** | UI labels, routes, descriptions, metadata | Merged (PR #1568) |
| **Specialized Worker** | **AI Workflow** | UI labels, routes, sidebar, titles | Merged (PR #1569) |
| **Code Node / Custom Code** | **Custom Node** | UI labels, metadata, error messages, logs, dropdowns | Merged (PR #1778) |
| **Custom Code Nodes** (category) | **Foundation** (category) | Canvas dropdown category | Merged (PR #1778) |
| **Failed Workers** | **Failed Worker Runs** | Analytics metric card | Merged (PR #1483) |
| **AI Workflow Call** (node name) | **Run AI Workflow** | Canvas control flow node `worker_call` | EN-2407 |
| **AI Worker Call** (node name) | **Run AI Worker** | Canvas control flow node `universal_worker_call` | EN-2407 |
| **Map Worker** (node name) | **Repeat Workflow** | Canvas control flow node `map_worker` | EN-2407 |
| **Fold Worker** (node name) | **Combine Workflow Results** | Canvas control flow node `fold_worker` | EN-2407 |
| **Switch Worker** (node name) | **Route Workflow** | Canvas control flow node `switch_worker` | EN-2407 |
| **Until Worker** (node name) | **Repeat Workflow Until** | Canvas control flow node `until_worker` | EN-2407 |
| "Select a worker..." (various) | "Select a workflow..." | Canvas worker select dropdowns, placeholders | EN-2407 (i18n) |
| **Workers Available** | **Workforce Available** | Analytics metric card | Unmerged (EN-2824) |
| **Workers Used** | **Total Executions** | Analytics metric card | Unmerged (EN-2824) |
| **Workers Execution Performance** | **Workforce Performance** | Analytics chart title | Unmerged (EN-2824) |
| **Worker Name** (table header) | **Name** | Analytics execution table | Unmerged (EN-2824) |

### Canvas Node Renames (EN-2407)

| Node ID | Old Name | New Name | Old Description | New Description |
|---------|----------|----------|-----------------|-----------------|
| `worker_call` | AI Workflow Call | **Run AI Workflow** | Execute a single sub-workflow with parameters | Execute another workflow with specific inputs |
| `universal_worker_call` | AI Worker Call | **Run AI Worker** | Execute an AI worker | Prompt an AI Worker with your input and receive its response |
| `map_worker` | Map Worker | **Repeat Workflow** | Parallel array processing with sub-workers | Execute a workflow for each item in a list, in parallel |
| `fold_worker` | Fold Worker | **Combine Workflow Results** | Sequential accumulator processing | Combine results from multiple workflow executions into one |
| `switch_worker` | Switch Worker | **Route Workflow** | Conditional execution based on switch/case logic | Evaluate conditions and execute different workflows based on the result |
| `until_worker` | Until Worker | **Repeat Workflow Until** | Iterative execution until condition becomes true | Execute a workflow repeatedly until a condition is met |

---

## 2. PR #1568 — Universal Worker → AI Worker

**Commit:** `66e8bc0ba` | **PR:** #1568 | **Status:** Merged to main
**Title:** Rebranding: Universal Worker → AI Worker

### What Changed

All UI-facing references from "Universal Worker" to "AI Worker" across 17 files.

### Detailed Changes

#### Routes & Navigation (`imports/ui/routes/appRoutes.tsx`)
- Route name `'Universal'` → `'AI Workers'`
- Route title `'Universal Workers'` → `'AI Workers'`
- `'Create Universal Worker'` → `'Create AI Worker'`
- `'Edit Universal Worker'` → `'Edit AI Worker'`

#### Sidebar (`imports/ui/data/mainSidebarItems.ts`)
- Menu item title `'Universal worker'` → `'AI worker'`

#### Node Metadata (`imports/core/agentic/Agents/Functions/CustomNodes.ts`)
- `universal_worker_call` node:
  - name: `'Universal Worker Call'` → `'AI Worker Call'`
  - description: `'Execute a universal worker'` → `'Execute an AI worker'`
  - All parameter descriptions updated (e.g., "ID of the universal worker" → "ID of the AI worker")
  - Usage description and capabilities updated
  - Code example description updated

#### JSDoc Comments (`imports/core/agentic/Agents/Functions/ControlNodes.ts`)
- `EXEUniversalWorkerCall` function docs: "Universal Worker Call" → "AI Worker Call"
- All `@param` and `@returns` annotations updated

#### UI Select Field (`imports/core/canvas/ui/components/EditNode/ParameterFields/UniversalWorkerSelectField.tsx`)
- Placeholder: `'Select a universal worker...'` → `'Select an AI worker...'`
- No options: `'No universal workers found'` → `'No AI workers found'`
- Loading: `'Loading universal workers...'` → `'Loading AI workers...'`

#### Worker Pages
- **MyAgents.tsx:** Page titles `'My Universal Workers'` → `'AI Workers'`
- **StartingWorkersPage.tsx:** Card titles and descriptions completely rewritten:
  - Universal card: `firstTitle: 'Universal'` → `'AI'`, `secondTitle: 'Worker'` (unchanged)
  - Specialized card: `firstTitle: 'Specialized'` / `secondTitle: 'Worker'` → `firstTitle: 'AI'` / `secondTitle: 'Workflow'`
  - New description texts for both cards
- **CongratsModal.tsx:** `'Create Universal Worker'` → `'Create AI Worker'`, `'Your Worker is Ready'` → `'Your AI Worker is Ready'`
- **CreateWorker.tsx:** Modal title `'Edit/Create Universal Worker'` → `'Edit/Create AI Worker'`
- **WorkerSyncModal.tsx:** Badge `'Universal'` → `'AI Worker'`
- **EditBrain.tsx:** Debug labels updated (`'Universal workers count'` → `'AI workers count'`)
- **Skills.tsx:** `'your agent can actually do'` → `'your worker can actually do'`

#### Analytics
- **WorkerExecutionTable.tsx:** Type display `'Universal'` → `'AI Worker'`
- **WorkforceFilters.tsx:** Filter option `'Universal'` → `'AI Workers'`

#### Voice (`imports/ui/components/Voice/VoiceContextProvider.tsx`)
- Route context descriptions updated

#### Session Management (`imports/ui/pages/chat/SessionManagementPage.tsx`)
- Breadcrumb `'Universal Workers'` → `'AI Workers'`

---

## 3. PR #1569 — Specialized Workers → AI Workflows

**Commit:** `0e19f20b8` | **PR:** #1569 | **Status:** Merged to main
**Title:** EN-2084 rename specialized workers as AI workflows

### What Changed

Comprehensive rename of "Specialized Workers" to "AI Workflows" across 23+ files (including 35 new workflow avatar SVGs).

### Detailed Changes

#### Routes & Navigation (`imports/ui/routes/appRoutes.tsx`)
- Route name `'Specialized'` → `'AI Workflows'`
- Route title `'Specialized Workers'` → `'AI Workflows'`

#### Worker Pages
- **MyAgents.tsx:** Empty state uses `'AI Workers'` / `'Specialized'` based on `filterType`
- **WorkersToolbar.tsx:**
  - New `EWorkerType` and `EScopeFilter` enums used instead of string literals
  - Scope labels now dynamic: `{humanizeString(scopeFilter)} {WORKER_TYPE_LABELS[workersType]}`
  - Where `WORKER_TYPE_LABELS = { universal: 'workers', specialized: 'workflows' }`
  - Sort labels now use `humanizeString(sortBy)` instead of switch statement

#### Skills UI
- **SkillsModal.tsx:** Tab label `'Specialized Workers'` → `'AI Workflows'`
- **SkillsSummary.tsx:** Section title `'Specialized workers'` → `'AI Workflows'`
- **SkillsCard.tsx:** Avatar rendering uses `<Image>` with `roundedCircle` + `object-fit-cover`

#### Constants (`imports/ui/constants.ts`)
- New: `SPECIALIZED_WORKER_DEFAULT_AVATAR = '/images/avatars/workflow/workflow-avatar-21.svg'`
- New: `WORKFLOW_AVATARS_COUNT = 42`

#### Default Avatar Differentiation
- **AgentCardItem.tsx / AgentListItem.tsx:** Universal workers use `DEFAULT_AVATAR`, specialized workers use `SPECIALIZED_WORKER_DEFAULT_AVATAR`

#### Canvas UI
- **ExecutionControlPanel.tsx:** Import path updates, formatting
- **WorkerSettingsModal.tsx:** UI labels: `'Worker Settings'` → `'Workflow Settings'`, `'Worker Name'` → `'Workflow Name'`, `'Worker saved successfully!'` → `'Workflow saved successfully!'`
- **WorkerErrorAlert.tsx:** `'Worker Error'` text updates
- **ValidationErrorModal.tsx:** Self-closing JSX elements, formatting

#### Worker State Hook (`useWorkerState.ts`)
- `'Worker Sessions'` → `'Workflow Builder Sessions'`

#### Scheduler (`imports/ui/pages/Scheduler/ScheduleModal.tsx`)
- Import cleanup and formatting
- Schedule-related text references updated

#### Node Metadata (`CustomNodes.ts`)
- `worker_call` node: `'AI Workflow Call'` → remains (name set here)

#### New Types (`imports/ui/pages/workers/types.ts`)
- `EWorkerType` enum: `UNIVERSAL = 'universal'`, `SPECIALIZED = 'specialized'`
- `EScopeFilter` enum: `ALL = 'all'`, `GLOBAL = 'global'`, `GROUP = 'group'`, `OWN = 'own'`

#### SCSS Refactoring
- `_mixins.scss` split into `_status-ring.scss` and `_icons.scss`
- New `.icon-1` through `.icon-5` utility classes

#### Workflow Avatars
- 35 new SVG avatar files added in `public/images/avatars/workflow/`

---

## 4. PR #1778 — Code Node → Custom Node

**Commit:** `83d348f24` | **PR:** #1778 | **Status:** Merged to main
**Title:** Terminology Standardization: Custom Node

### What Changed

All user-facing references from "Code Node" to "Custom Node" across 17 files. Internal variable names, file names, collection names, and method names were left unchanged.

### Detailed Changes

#### Node Metadata (`CustomNodes.ts`)
- `code_node` entry:
  - name: `'Custom Code'` → `'Custom Node'`
  - description: `'Execute custom code node from collection'` → `'Execute custom node from collection'`
  - usageDescription updated
  - capabilities: `'Execute saved custom code nodes'` → `'Execute saved custom nodes'`
  - whenToUse: `'code node'` → `'custom node'`

#### Error Messages & Logs (`CustomNodes.ts`, `Tools.ts`)
- `'Executing custom code node'` → `'Executing custom node'`
- `'Code node {id} not found'` → `'Custom node {id} not found'`
- `'Code node {id} has compilation errors'` → `'Custom node {id} has compilation errors'`
- `'Code node updated successfully'` → `'Custom node updated successfully'`
- `'Error updating code node'` → `'Error updating custom node'`
- `'Code node compiled successfully'` → `'Custom node compiled successfully'`
- `'Code node executed successfully'` → `'Custom node executed successfully'`
- `'Error executing code node'` → `'Error executing custom node'`

#### Tool Descriptions (`Tools.ts`)
- Tool parameter descriptions: `'ID of the code node to update/compile/execute'` → `'ID of the custom node to update/compile/execute'`
- Tool descriptions: `'Update the code and metadata for a specific code node'` → `'...custom node'`

#### Server-Side (`Agents/Code/index.ts`, `helperWorkers.ts`)
- Meteor method auth error: `'You must be logged in to update code nodes'` → `'...custom nodes'`
- Log messages: `'Code node updated with IIAFNode format'` → `'Custom node updated...'`
- All method-level user-facing strings updated

#### UI Components
- **CodeNodeEditor.tsx:**
  - Default name: `'New Code Node'` → `'New Custom Node'`
  - Default description: `'Enter a description for your code node'` → `'...your custom node'`
- **CodeNodesList.tsx:**
  - Toast messages: `'New code node created successfully'` → `'New custom node created...'`
  - Error messages: `'Failed to create/delete new code node'` → `'...custom node'`
  - Console errors updated
  - Alt text: `'code node'` → `'custom node'`
- **CodeNodeHeader.tsx:**
  - Tab labels: `'Code Node Chat'` → `'Custom Node Chat'`
  - Header title: `'Code Node Builder'` → `'Custom Node Builder'`
- **CodeNodeChat.tsx:**
  - Placeholder: `'Ask the Code Node Builder...'` → `'Ask the Custom Node Builder...'`
- **CodeNodeTerminal.tsx:**
  - Tab label updates
- **CodeNodeCodeEditor.constants.ts:**
  - Code comment: `'Code Node Handler'` → `'Custom Node Handler'`

#### Canvas Dropdown (`AddNewNodeDropdown.tsx`)
- Category search: `'Custom Code Nodes'` → `'Custom Nodes'`
- Header: `'Custom Code Nodes'` → `'Custom Nodes'`
- CTA: `'Create New Code Node'` → `'Create New Custom Node'`

#### Select Field (`CodeNodeSelectField.tsx`)
- Placeholder: `'Select a code node...'` → `'Select a custom node...'`
- No options: `'No code nodes available'` → `'No custom nodes available'`
- Loading: `'Loading code nodes...'` → `'Loading custom nodes...'`
- Fallback labels: `'Unnamed Code Node'` → `'Unnamed Custom Node'`
- ID display: `'Code Node ID:'` → `'Custom Node ID:'`

#### Hooks
- **useCodeNodesData.ts:** `'Unknown Code Node'` → `'Unknown Custom Node'`, `'Unnamed Code Node'` → `'Unnamed Custom Node'`
- **useCustomCodeNodes.ts:** Category: `'Custom Code Nodes'` → `'Foundation'`, default description: `'Custom code node'` → `'Custom node'`
- **useNodeDataSync.ts:** Fallback name: `'Unnamed Code Node'` → `'Unnamed Custom Node'`

#### Parameter Config (`parameterFieldConfig.ts`)
- Label fallback: `'Unnamed Code Node'` → `'Unnamed Custom Node'`
- Placeholder: `'Select a code node to execute...'` → `'Select a custom node to execute...'`

#### Routes (`appRoutes.tsx`)
- Route name: `'Edit Code Node'` → `'Edit Custom Node'`

---

## 5. PR #1483 — Failed Workers → Failed Worker Runs

**Commit:** `a4496e4ec` | **PR:** #1483 | **Status:** Merged to main
**Title:** EN-2060 Rename "Failed Workers" to "Failed Worker Runs" and Track Execution-Level Failures

### What Changed

Analytics metric title rename plus a logic change to track execution-level failures.

### Detailed Changes

#### WorkforceMetrics.tsx
- Metric title: `'Failed Workers'` → `'Failed Worker Runs'`
- Now uses `failedExecutions` prop (execution count) instead of `metrics.failedWorkers` (unique worker count)
- Percentage calculation: now against `totalExecutions` (not `workersAvailable`)
- New `failedExecutions` prop added to component type
- New `getFailedExecutionsPercentage()` function

#### WorkforceOverview.tsx
- New `failedExecutions` computed via `useMemo` from chart series `'Failed'` data
- Passed as prop to `<WorkforceMetrics>`

#### utils.ts
- `isFinite`/`isNaN` → `Number.isFinite`/`Number.isNaN` (global → static methods)
- `subDays(nowDate, 7)` → `subWeeks(nowDate, 1)` for 7-day range
- `subDays(nowDate, 30)` → `subMonths(nowDate, 1)` for 30-day range
- Formatting/linting cleanups

---

## 6. EN-2407 — Canvas Node Names, Descriptions & i18n

**Branch:** `EN-2407_Change-all-Specialized-Worker-Nodes-name-and-terminology`
**Commits:** `4d3a0e4aa` (renamings in canvas), `a162b0f18` (node descriptions)

### What Changed

Updated canvas node names/descriptions to be more user-friendly and added i18n support for worker select fields.

### Detailed Changes

#### Node Metadata Renames (`CustomNodes.ts`)

| Node ID | Old Name → New Name | Old Description → New Description |
|---------|---------------------|-----------------------------------|
| `worker_call` | AI Workflow Call → **Run AI Workflow** | Execute a single sub-workflow with parameters → Execute another workflow with specific inputs |
| `universal_worker_call` | AI Worker Call → **Run AI Worker** | Execute an AI worker → Prompt an AI Worker with your input and receive its response |
| `map_worker` | Map Worker → **Repeat Workflow** | Parallel array processing with sub-workers → Execute a workflow for each item in a list, in parallel |
| `fold_worker` | Fold Worker → **Combine Workflow Results** | Sequential accumulator processing → Combine results from multiple workflow executions into one |
| `switch_worker` | Switch Worker → **Route Workflow** | Conditional execution based on switch/case logic → Evaluate conditions and execute different workflows based on the result |
| `until_worker` | Until Worker → **Repeat Workflow Until** | Iterative execution until condition becomes true → Execute a workflow repeatedly until a condition is met |

#### Parameter Field Placeholders (`parameterFieldConfig.ts`)
- `'Select a worker to call...'` → `'Select a workflow to call...'`
- `'Select a worker for map processing...'` → `'Select a workflow for map processing...'`
- `'Select a worker for fold processing...'` → `'Select a workflow for fold processing...'`
- `'Select a worker for switch processing...'` → `'Select a workflow for switch processing...'`
- `'Select a universal worker...'` → `'Select AI Worker...'`
- `'Select a worker for until loop...'` → `'Select a workflow for until loop...'`

#### i18n: New Locale Files

**`public/locales/en/canvas.json`** (new file):
```json
{
    "parameter-fields": {
        "specialized-worker-select": {
            "placeholder": "Select a workflow...",
            "loading-workers": "Loading available workflows...",
            "no-workers-available": "No workflows available",
            "workers-available_one": "{{count}} workflow available",
            "workers-available_other": "{{count}} workflows available",
            "workers-available_zero": "No workflows available",
            "worker-not-selected": "Workflow is not selected",
            "worker-has-no-inputs": "Workflow has no inputs"
        }
    },
    "nodes": {
        "switch_worker": {
            "case-placeholder": "Select workflow for this case...",
            "default-placeholder": "Select default workflow..."
        }
    }
}
```

#### WorkerSelectField.tsx — i18n Integration
- Default placeholder now uses `t('canvas:parameter-fields.specialized-worker-select.placeholder')` → "Select a workflow..."
- Loading message: `t('...loading-workers')` → "Loading available workflows..."
- No options: `t('...no-workers-available')` → "No workflows available"
- Helper text: `t('...workers-available', { count })` → "X workflow(s) available"
- Worker not selected: `t('...worker-not-selected')` → "Workflow is not selected"
- No inputs: `t('...worker-has-no-inputs')` → "Workflow has no inputs"

#### SwitchNodeCase.tsx — i18n Integration
- Placeholder for default case: `t('canvas:nodes.switch_worker.default-placeholder')` → "Select default workflow..."
- Placeholder for regular case: `t('canvas:nodes.switch_worker.case-placeholder')` → "Select workflow for this case..."

#### Build Config (`i18n.build.js`)
- Locale file glob: `imports/ui/**/locales/*.json` → `imports/**/locales/*.json` (now includes non-UI locale files)

#### CSS Fix (`AddNewNodeDropdown.tsx`)
- Added `text-wrap` class to description `<small>` elements for proper wrapping

---

## 7. EN-2824 — Analytics Page Terminology (Unmerged)

**Branch:** `EN-2824_Analytics-Page-Terminology`
**Status:** Not merged (2 unique commits: `2ed1b30dd`, `39ae5b2db`)

### What Changed

Comprehensive i18n integration for the Analytics page with updated terminology.

### Detailed Changes

#### EWorkerType Enum Values (`imports/core/agentic/Analytics/types.ts`)
- `ALL = 'All worker types'` → `ALL = 'all'`
- `UNIVERSAL = 'Universal'` → `UNIVERSAL = 'universal'`
- `SPECIALIZED = 'Specialized'` → `SPECIALIZED = 'specialized'`

#### WorkerType Type (`imports/ui/pages/Analytics/types.ts`)
- `'Universal' | 'Specialized'` → `'universal' | 'specialized'`

#### Metric Card Titles (`WorkforceMetrics.tsx`)
- `'Workers Available'` → `t('metrics.available-workers.title')` → **"Workforce Available"**
- `'Workers Used'` → `t('metrics.used-workers.title')` → **"Total Executions"**
- `'Failed Worker Runs'` → `t('metrics.failed-workers.title')` → **"Failed Executions"**
- `'Average Execution Time'` → `t('metrics.execution-time.title')` → **"Average Execution Time"** (unchanged)

#### Chart Title (`WorkforceCharts.tsx`)
- `'Workers Execution Performance'` → `t('charts.performance.title')` → **"Workforce Performance"**

#### Table Headers (`WorkerExecutionTable.tsx`)
- `'Worker Name'` → `t('analytics:lists.executions.name')` → **"Name"**
- `'Started by'` → `t('analytics:lists.executions.started-by')` → **"Started By"**
- `'Start Mode'` → `t('analytics:lists.executions.start-mode')` → **"Start Mode"**
- `'Date & Time'` → `t('analytics:lists.executions.date-time')` → **"Date & Time"**
- `'Duration'` → `t('analytics:lists.executions.duration')` → **"Duration"**
- `'Status'` → `t('analytics:lists.executions.status')` → **"Status"**
- CSV headers: `'Agent ID'` → `'Worker ID'`, `'Worker Name'` → `'Name'`
- Worker type display now uses `t('shared:worker.universal-short')` / `t('shared:worker.specialized-short')` → "Worker" / "Workflow"

#### Filter Labels (`WorkforceFilters.tsx`)
- `'All Workers'` → `t('worker-filter.worker-type.all')` → **"All workforce types"**
- `'Universal'` option → `t('worker-filter.worker-type.universal')` → **"AI Worker"**
- `'Specialized'` option → `t('worker-filter.worker-type.specialized')` → **"AI Workflow"**
- Worker select placeholder → `t('worker-filter.worker.all')` → **"All workforce"**
- Tag placeholder → `t('worker-filter.tag.all')` → **"All Tags"**
- Time period options all localized:
  - `'Last hour'`, `'Last 24 hours'`, `'Last 7 days'`, `'Last 30 days'`
- Unnamed workers now shown in italic font style

#### New i18n Files

**`public/locales/en/analytics.json`** and **`imports/ui/pages/Analytics/locales/en.json`**:
```json
{
    "worker-filter": {
        "worker-type": { "all": "All workforce types", "universal": "AI Worker", "specialized": "AI Workflow" },
        "worker": { "all": "All workforce", "no-name": "Unnamed worker" },
        "tag": { "all": "All Tags" },
        "users": { "all": "All Users" },
        "time-period": { "last-hour": "Last hour", "last-day": "Last 24 hours", "last-week": "Last 7 days", "last-month": "Last 30 days" }
    },
    "charts": { "performance": { "title": "Workforce Performance" } },
    "lists": { "executions": { "title": "Workforce Executions", "name": "Name", "started-by": "Started By", "start-mode": "Start Mode", "date-time": "Date & Time", "duration": "Duration", "status": "Status" } },
    "metrics": {
        "available-workers": { "title": "Workforce Available" },
        "used-workers": { "title": "Total Executions" },
        "failed-workers": { "title": "Failed Executions" },
        "execution-time": { "title": "Average Execution Time" }
    }
}
```

**`public/locales/en/shared.json`** — added worker display names:
```json
{
    "worker": {
        "universal": "AI Worker",
        "universal_many": "AI Workers",
        "universal-short": "Worker",
        "universal-short_many": "Workers",
        "specialized": "AI Workflow",
        "specialized_many": "AI Workflows",
        "specialized-short": "Workflow",
        "specialized-short_many": "Workflows"
    }
}
```

#### New Publication (`imports/core/agentic/Agents/publications.ts`)
- New: `core.agentic.workersByIds` — subscribes to multiple workers by array of IDs

---

## 8. i18n Keys Reference

### Shared Keys (`public/locales/en/shared.json`)

| Key | Value | Context |
|-----|-------|---------|
| `shared:worker.universal` | AI Worker | Full display name |
| `shared:worker.universal_many` | AI Workers | Plural |
| `shared:worker.universal-short` | Worker | Short form |
| `shared:worker.universal-short_many` | Workers | Short form plural |
| `shared:worker.specialized` | AI Workflow | Full display name |
| `shared:worker.specialized_many` | AI Workflows | Plural |
| `shared:worker.specialized-short` | Workflow | Short form |
| `shared:worker.specialized-short_many` | Workflows | Short form plural |

### Canvas Keys (`public/locales/en/canvas.json`)

| Key | Value |
|-----|-------|
| `canvas:parameter-fields.specialized-worker-select.placeholder` | Select a workflow... |
| `canvas:parameter-fields.specialized-worker-select.loading-workers` | Loading available workflows... |
| `canvas:parameter-fields.specialized-worker-select.no-workers-available` | No workflows available |
| `canvas:parameter-fields.specialized-worker-select.workers-available_one` | {{count}} workflow available |
| `canvas:parameter-fields.specialized-worker-select.workers-available_other` | {{count}} workflows available |
| `canvas:parameter-fields.specialized-worker-select.worker-not-selected` | Workflow is not selected |
| `canvas:parameter-fields.specialized-worker-select.worker-has-no-inputs` | Workflow has no inputs |
| `canvas:nodes.switch_worker.case-placeholder` | Select workflow for this case... |
| `canvas:nodes.switch_worker.default-placeholder` | Select default workflow... |

### Analytics Keys (`public/locales/en/analytics.json`)

| Key | Value |
|-----|-------|
| `analytics:worker-filter.worker-type.all` | All workforce types |
| `analytics:worker-filter.worker-type.universal` | AI Worker |
| `analytics:worker-filter.worker-type.specialized` | AI Workflow |
| `analytics:worker-filter.worker.all` | All workforce |
| `analytics:worker-filter.worker.no-name` | Unnamed worker |
| `analytics:metrics.available-workers.title` | Workforce Available |
| `analytics:metrics.used-workers.title` | Total Executions |
| `analytics:metrics.failed-workers.title` | Failed Executions |
| `analytics:metrics.execution-time.title` | Average Execution Time |
| `analytics:charts.performance.title` | Workforce Performance |
| `analytics:lists.executions.name` | Name |
| `analytics:lists.executions.started-by` | Started By |

---

## 9. New Enums and Types

### `EWorkerType` (UI — `imports/ui/pages/workers/types.ts`)
```typescript
export enum EWorkerType {
    UNIVERSAL = 'universal',
    SPECIALIZED = 'specialized',
}
```

### `EScopeFilter` (UI — `imports/ui/pages/workers/types.ts`)
```typescript
export enum EScopeFilter {
    ALL = 'all',
    GLOBAL = 'global',
    GROUP = 'group',
    OWN = 'own',
}
```

### `EWorkerType` (Analytics — `imports/core/agentic/Analytics/types.ts`) — Updated
```typescript
export enum EWorkerType {
    ALL = 'all',          // was 'All worker types'
    UNIVERSAL = 'universal',  // was 'Universal'
    SPECIALIZED = 'specialized', // was 'Specialized'
}
```

### `WorkerType` (Analytics — `imports/ui/pages/Analytics/types.ts`) — Updated
```typescript
export type WorkerType = 'universal' | 'specialized';  // was 'Universal' | 'Specialized'
```

---

## 10. Files Changed Summary

### Merged Changes

| PR | Files Changed | Insertions | Deletions |
|----|---------------|------------|-----------|
| #1568 (Universal Worker → AI Worker) | 17 | +54 | -54 |
| #1569 (Specialized Workers → AI Workflows) | 59 | +812 | -353 |
| #1778 (Code Node → Custom Node) | 17 | +90 | -90 |
| #1483 (Failed Workers → Failed Worker Runs) | 3 | +117 | -85 |

### Unmerged Changes

| Branch | Files Changed | Insertions | Deletions |
|--------|---------------|------------|-----------|
| EN-2407 (Canvas Node Names) | 8 | +136 | -72 |
| EN-2824 (Analytics Terminology) | 12 | +244 | -33 |

### Key Files Affected (Comprehensive List)

**Core/Backend:**
- `imports/core/agentic/Agents/Functions/CustomNodes.ts` (modified in 4 PRs)
- `imports/core/agentic/Agents/Functions/ControlNodes.ts`
- `imports/core/agentic/Agents/Functions/Tools.ts`
- `imports/core/agentic/Agents/Code/index.ts`
- `imports/core/agentic/Agents/Code/helperWorkers.ts`
- `imports/core/agentic/Agents/publications.ts`
- `imports/core/agentic/Analytics/types.ts`

**Canvas UI:**
- `imports/core/canvas/ui/components/AddNewNodeDropdown.tsx`
- `imports/core/canvas/ui/components/EditNode/ParameterFields/WorkerSelectField.tsx`
- `imports/core/canvas/ui/components/EditNode/ParameterFields/UniversalWorkerSelectField.tsx`
- `imports/core/canvas/ui/components/EditNode/ParameterFields/CodeNodeSelectField.tsx`
- `imports/core/canvas/ui/components/ConnectionModal/SwitchNodeParameterEditor/SwitchNodeCase.tsx`
- `imports/core/canvas/ui/components/ExecutionControlPanel.tsx`
- `imports/core/canvas/ui/components/WorkerSettingsModal.tsx`
- `imports/core/canvas/ui/components/ValidationErrorModal.tsx`
- `imports/core/canvas/ui/components/WorkerErrorAlert.tsx`
- `imports/core/canvas/ui/hooks/useWorkerState.ts`
- `imports/core/canvas/ui/hooks/useCodeNodesData.ts`
- `imports/core/canvas/ui/hooks/useCustomCodeNodes.ts`
- `imports/core/canvas/ui/hooks/useNodeDataSync.ts`
- `imports/core/canvas/ui/utils/parameterFieldConfig.ts`

**Code Node Editor:**
- `imports/core/agentic/Agents/Code/ui/pages/CodeNodeEditor.tsx`
- `imports/core/agentic/Agents/Code/ui/pages/CodeNodesList.tsx`
- `imports/core/agentic/Agents/Code/ui/components/CodeNodeChat.tsx`
- `imports/core/agentic/Agents/Code/ui/components/CodeNodeHeader.tsx`
- `imports/core/agentic/Agents/Code/ui/components/CodeNodeTerminal.tsx`
- `imports/core/agentic/Agents/Code/ui/components/CodeNodeCodeEditor.constants.ts`

**Workers/Pages:**
- `imports/ui/pages/workers/MyAgents.tsx`
- `imports/ui/pages/workers/StartingWorkersPage.tsx`
- `imports/ui/pages/workers/components/WorkersToolbar.tsx`
- `imports/ui/pages/workers/components/AgentCardItem.tsx`
- `imports/ui/pages/workers/components/AgentListItem.tsx`
- `imports/ui/pages/workers/components/EditBrain.tsx`
- `imports/ui/pages/workers/components/WorkerSyncModal.tsx`
- `imports/ui/pages/workers/createWorker/CreateWorker.tsx`
- `imports/ui/pages/workers/createWorker/CongratsModal.tsx`
- `imports/ui/pages/workers/createWorker/Skills/Skills.tsx`
- `imports/ui/pages/workers/createWorker/Skills/SkillsModal.tsx`
- `imports/ui/pages/workers/createWorker/Skills/SkillsCard.tsx`
- `imports/ui/pages/workers/createWorker/Skills/SkillsSummary.tsx`

**Analytics:**
- `imports/ui/pages/Analytics/components/WorkforceMetrics.tsx`
- `imports/ui/pages/Analytics/components/WorkforceCharts.tsx`
- `imports/ui/pages/Analytics/components/WorkforceFilters.tsx`
- `imports/ui/pages/Analytics/components/WorkforceOverview.tsx`
- `imports/ui/pages/Analytics/components/WorkerExecutionTable.tsx`
- `imports/ui/pages/Analytics/components/utils.ts`
- `imports/ui/pages/Analytics/types.ts`

**Routing & Navigation:**
- `imports/ui/routes/appRoutes.tsx` (modified in 3 PRs)
- `imports/ui/data/mainSidebarItems.ts`

**Locale/i18n Files:**
- `public/locales/en/shared.json`
- `public/locales/en/canvas.json` (new)
- `public/locales/en/analytics.json` (new)
- `imports/ui/locales/en.json`
- `imports/ui/pages/Analytics/locales/en.json` (new)
- `imports/ui/components/Common/locales/en.json`
- `imports/core/canvas/ui/components/EditNode/ParameterFields/locales/en.json` (new)

**Other:**
- `imports/ui/App.tsx`
- `imports/ui/constants.ts`
- `imports/ui/pages/workers/types.ts` (new)
- `imports/ui/pages/Scheduler/ScheduleModal.tsx`
- `imports/ui/pages/chat/SessionManagementPage.tsx`
- `imports/ui/components/Voice/VoiceContextProvider.tsx`
- `imports/styles/mixins/_icons.scss` (new)
- `imports/styles/mixins/_status-ring.scss` (new)
- `imports/styles/mixins/_mixins.scss`
- `imports/styles/style.scss`
- `i18n.build.js`
