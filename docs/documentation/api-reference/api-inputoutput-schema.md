---
title: API output schema
excerpt: Part of the results are controlled by the worker builder/node type.
deprecated: false
hidden: true
icon: fad fa-code-simple
metadata:
  robots: index
---
**Agent execute (POST) request output schema** :

```json Success: True
{
	"success": true, // Indicates that platform received and processed the request
	"data":
	{
		"sessionId": string, // ID of the session, can be used to send another execution to the same session
		"executionId": string, // Execution ID to query the result
		"promptTokens": integer // Number of tokens used in prompt
	}
}
```
```json Success: False
{
  "success": false,		// Indicates that platform completely failed the request
  "error": string 		// Human-readable message. No data object is included on failures.
}
```

***

**Get execution logs (GET) request output schema - execution in progress** :

```json Success: True
{
	"success": true,
	"data":
	{
		"_id": string, // Internal ID
		"executionStarted": datetime,	// Start time
		"nodeResults": [	
			null,	// For each node
			...,
			null // For each node
		],
		"ctx":
		{
			"userId": string, // ID of the user calling the agent
			"agentId": string, // ID of the agent
			"sessionId": string, // ID of the session
			"executionId": string // Same as the one in GET URL
		}
	}
}
```
```json Success: False
{
  "success": false,		// Indicates that platform completely failed the request
  "error": string 		// Human-readable message. The HTTP status code reflects the error type (e.g., 400 validation, 401 auth, 403 permission, 429 rate limit, 500 server). No data object is included on failures.
}
```

***

**Get execution logs (GET) request output schema - execution finished** :

```json Success: True
{
  "success": true,
	"data":
	{
		"_id": string,
		"executionStarted": datetime,	// Worker execution start time
		"executionEnded": datetime,	// Worker execution end time
		"nodeResults": [	
			inputParams?: object,	// All input parameters for the worker in JSON format
			{	// FOR EACH NODE
				"ok": boolean,	// True/false
				"status": number,	// The HTTP status code reflects the error type (e.g., 200 OK, 400 validation, 401 auth, 403 permission, 429 rate limit, 500 server).
				"statusText": string,	// Human-readable status text
				"error": string,	// (OPTIONAL: Only if OK is false) Human-Readable error text
				"result": any,	// Node-specific output object / array
				"nodeId": number,	// ID of the node
				"executionStarted": datetime,	// Time of node execution start
				"executionFinished": datetime	// Time of node execution end
			},
			...
		],
		"ctx":
		{
			"userId": string,
			"agentId": string,
			"sessionId": string,
			"executionId": string
		},
		"time": number, // Executon time
		"finalResult":
		[	// This is an array because API supports agents with multiple output nodes, but the Web UI allows to create single output nodes manually only, so in most of scenarios this array contains only one element.
			{
				"ok": boolean,
				"status": number,	// The HTTP status code reflects the error type (e.g., 200 OK, 400 validation, 401 auth, 403 permission, 429 rate limit, 500 server). 
				"statusText": string,	// Human-readable status text
				"error":	 string, 			// (OPTIONAL: Only if OK is false) Human-Readable error text
				"result": object,	// Output of the final worker OUTPUT node outputParams in JSON format
				"nodeId": number,	// Node ID of the final workr OUTPUT node
				"executionStarted": datetime,	// ??
				"executionFinished": datetime	// Worker execution stop time
			},
		],
	},
}
```
```json Success: false
{
  "success": false,		// Indicates that platform completely failed the request
  "error": string 		// Human-readable message. The HTTP status code reflects the error type (e.g., 400 validation, 401 auth, 403 permission, 429 rate limit, 500 server). No data object is included on failures.
}
```

***

**Examples** of node-specific RESULT outputs in different format:

```json
// NB! Code worker nodes, Universal API nodes have output schema built into the node (that you can change during building)
// NB! LLM nodes and other nodes that come from configured providers have provider-specific and sometimes model-specific output schema
// You must always run these nodes first at least once to generate and be able to connect/see the output/output schema.

// PDF to image node
[
	{
		image: 'URL1',
		description: '',
	},
	{
		image: 'URL2',
		description: '',
	},
	{
		image: 'URL3',
		description: '',
	},
]

// Browser node output
{
    error?: string | null,
    sessionID: string,
    requestID: string,
    timestamp: Date,
    downloadedFile?: string, // base64
    downloadedFileName?: string // example: 7e0ed06c-01ea-4e71-a9e3-bfe0ab8517d2
    meta: BrowserMeta,
    generationInfo?: BrowserGenerationInfo,
    value?: string,
    screenshots: Record<string, string>,
}

// Fold worker
{
    finalAccumulator: any, // Final accumulator result
    processedItems: number, // Total items processed
    totalItems: number, // Total items (processed + skipped)
    skippedItems?: number, // only in safe mode
    earlyTermination?: boolean,
    memoryWarnings?: number, // count of memory warnings
}

// Map worker
{
    results: any[],
    totalItems: number,  // number of inputs
    successCount: number,
    errorCount: number,
    effectiveConcurrency: number,  // max number of items that were processed in parallel
    errors?: Array<{ index: number, error: string }>,
}

// Render-markdown
string // File URL in string format

// Read URL
{
  content: string, // Clean markdown content
  title: string, // Page title
  url: string, // URL that was read
}

// Storage upload
{
  url: string, // Public URL of uploaded file
  filename: string, // Final stored filename
  secret: string, // Secret key for secure access
  size: string, // File size in bytes
  contentType: string, // MIME type of the file
}

// Switch worker
{
    matchedCases: [{	// Array
        caseIndex: number,
        value: any,
        workerId: string,
        result: any,
        success: boolean,
        error?: string,
    }],
    defaultExecuted?: boolean,
    totalCases: number,
    switchValue: any,
    hasAnyMatch: boolean, // Whether any case matched
    executionStopped?: boolean, // Whether stopped due to break
}

// Until worker
{
    finalState: any,
    iterations: number,
    maxIterations: number,
    conditionMet: boolean,
    terminationReason:
        | 'condition_met'
        | 'initial_condition_met'
        | 'max_iterations'
        | 'timeout'
        | 'error',
    executionTimeMs: number,
    memoryWarnings?: number,
    timeoutWarnings?: number,
    consecutiveErrors?: number,
}

// Vector save
{
    docId: string
}

// Vector search
{
    success: boolean,
    results: IVectorSearchResult[],
    count: number,
    embedder: string,
    searchIndex: string,
}
```

<br />
