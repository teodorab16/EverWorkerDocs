---
title: API input/output schema
deprecated: false
hidden: true
icon: fad fa-code-simple
metadata:
  robots: index
---
**Agent execute (POST) request input schema**:

* agentId is the ID of the agent you are trying to execute.
* sessionId (optional) can be a random string (i.e. "new_session") if you explicitly want to start a new session, or it can be an ID of previously started session.
* inputParams is a JSON-encoded list of all input variables you have created in the agent Input node.
* bypassCache: if set to true, it forces a fresh execution bypassing any cached result for identical inputs.
