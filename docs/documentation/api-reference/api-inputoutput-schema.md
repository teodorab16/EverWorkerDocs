---
title: API input/output schema
deprecated: false
hidden: true
icon: fad fa-code-simple
metadata:
  robots: index
---
**Agent execute (POST) request output schema**:

```
{
  "success": boolean,
  "data": {
    "sessionId": string,
    "executionId": string,
    "promptTokens": integer
  }
}
```
