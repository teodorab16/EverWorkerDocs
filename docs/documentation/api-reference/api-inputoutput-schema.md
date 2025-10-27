---
title: API input/output schema
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

<br />

**Get execution logs (GET) request output schema - execution in progress** :

```json Success: True
{
	"success": boolean,
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
				"status": int,	// The HTTP status code reflects the error type (e.g., 200 OK, 400 validation, 401 auth, 403 permission, 429 rate limit, 500 server).
				"statusText": string,	// Human-readable status text
				"error": string,	// (OPTIONAL: Only if OK is false) Human-Readable error text
				"result": object,	// Output object / array of objects of the node in JSON format
				"nodeId": int,	// ID of the node
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
		"time": int,
  	"finalResult":
		[	// This is an array because API supports agents with multiple output nodes, but the Web UI allows to create single output nodes manually only, so in most of scenarios this array contains only one element.
			{
				"ok": boolean,
				"status": int,	// The HTTP status code reflects the error type (e.g., 200 OK, 400 validation, 401 auth, 403 permission, 429 rate limit, 500 server). 
				"statusText": string,	// Human-readable status text
				"error":	 string, 			// (OPTIONAL: Only if OK is false) Human-Readable error text
				"result": object,	// Output of the final worker OUTPUT node outputParams in JSON format
				"nodeId": int,	// Node ID of the final workr OUTPUT node
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

<br />

Examples of node outputs for nodes with "Result" object = **JSON ** vs "Result" object = **Array of JSON objects**:

```
// Nodes that produce single output (i.e. LLM node)
                {
                    ok: true,
                    result: { role: 'assistant', content: '{ "response": "This is worker response" }' },
                    nodeId: 4,
                    executionStarted: '2025-10-23T18:39:33.968Z',
                    executionFinished: '2025-10-23T18:39:34.702Z',
                }
// Nodes that produce an array of outputs (i.e. PDF to image)
                {
                    ok: true,
                    status: 200,
                    result: [
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
                    ],
                    nodeId: 5,
                    executionStarted: '2025-10-23T18:39:26.534Z',
                    executionFinished: '2025-10-23T18:39:28.641Z',
                },
```
