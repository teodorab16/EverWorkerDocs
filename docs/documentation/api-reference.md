---
title: API reference
excerpt: This section explains how to execute agents via HTTPS API requests
deprecated: false
hidden: true
icon: fad fa-square-9
metadata:
  robots: index
---
# Terminology

**API request** - a web request executed via application capable of sending such requests. Example include but are not limited to browsers, POSTMAN, customer programs written in any language capable of executing https-based requests. Typical request types used with EverWorker platform are POST and GET type requests. API requests consist of headers and a body in JSON format (for POST requests). Authentication is done via using tokens in one of headers.

**Token (Bearer token)** - authentication method used to impersonate a certain user in order to access the platform. Each user can create their own tokens, and administrator can see each token and its expiration date in Settings.

**Agent** - a specific universal or specialized worked designed in the platform.

**AgentID** - Agents (workers) are executable using API via their agentID that can be found in the URL of any agent configuration. AgentID is a unique identifier for each worker.

**Execution** - A single run of an agent. Execution and its ID is important to query status and results for a certain run that was called using API.

# Authentication and token creation

In order to be able to execute API requests towards the platform, a user must access their profile (top right corner button with a dropdown), switch to "Api Tokens" tab and generate a new token with a custom name and expiration date.

Tokens can be revoked from the same interface where they are created

![](https://files.readme.io/d2dc437d49bf6cdaa159da6019665cb26c275f9f09413dcbe01280e5de394bf9-image.png)

During the token creation, you have 4 different permission types you can assign to the topic.

* `agent:execute` - allowing to use this token to execute agents (workers)
* `agent:logs` - allowing to use this token to read agent (worker) logs
* `agents:health` - allowing to use this token to view platform health
* `observatory:write` - allowing to use this token for superadmin operations not covered by this guide

Make sure to copy the token value to a secure vault/password manager/write it down, because you cannot access its value in web UI after it's created for security considerations.

In all future requests, this token will be used in headers of HTTP requests. Header name "Auhorization", header value "bearer `<token>`".
