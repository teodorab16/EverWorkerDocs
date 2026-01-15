---
title: Skills & Capabilities
excerpt: >-
  This section covers how Workers gain capabilities through Skills, including API integrations, AI Workflows, and MCP servers.
deprecated: false
hidden: false
icon: fad fa-square-4
metadata:
  robots: index
---
### Topics Covered:

* **Skills Overview**: How Workers acquire and use capabilities
* **API Integrations**: Using Providers and Connectors as skills
* **AI Workflows as Skills**: Embedding workflows within AI Workers
* **MCP (Model Context Protocol)**: Connecting to external tool servers

***

# Skills Overview

**Skills** are the capabilities that enable Workers to interact with external systems, execute specialized logic, and perform actions beyond basic conversation. Skills transform AI Workers from simple chat interfaces into powerful automation agents.

### Types of Skills:

* **API Integrations**: External services accessed via Providers and Connectors (e.g., Microsoft 365, Salesforce, GitHub)
* **AI Workflows**: Canvas-built workflows embedded as callable tools within AI Workers
* **MCP Tools**: Tools discovered from external MCP (Model Context Protocol) servers

### How Skills Work:

1. **Configuration**: Builders add skills to Workers in the AI Worker Builder's **Skills tab**
2. **Discovery**: The Worker learns what actions are available through skill definitions
3. **Invocation**: During conversations, the LLM decides when to use a skill based on user intent
4. **Execution**: The platform executes the skill and returns results to the conversation
5. **Session Control**: Users can enable/disable specific skills per session

***

# API Integrations

API integrations allow Workers to interact with external services through **Providers** and **Connectors**.

### Adding API Skills:

1. Navigate to the **Skills tab** in the AI Worker Builder
2. Select from available Connectors (configured in the Provider system)
3. Choose specific operations (endpoints) to expose as skills
4. Configure any default parameters or constraints

### Skill Behavior:

* Workers automatically understand when to call API skills based on conversation context
* Authentication is handled transparently via Connectors
* Results are formatted and presented naturally in the conversation
* Failed calls are handled gracefully with appropriate error messages

### Best Practices:

* Only add skills that are relevant to the Worker's purpose
* Use descriptive operation names to help the LLM understand when to use them
* Configure appropriate rate limits and timeouts
* Test skills thoroughly before deploying to users

***

# AI Workflows as Skills

**AI Workflows** built in Canvas can be embedded as skills within AI Workers, enabling complex multi-step operations to be triggered from natural conversation.

### Benefits:

* **Encapsulation**: Complex logic is packaged into a single callable skill
* **Reusability**: One workflow can be used across multiple Workers
* **Maintainability**: Update the workflow once, all Workers using it get the update
* **Separation of Concerns**: Business logic lives in workflows, conversation logic in Workers

### Configuring Workflow Skills:

1. Build and test your AI Workflow in Canvas
2. In the AI Worker Builder, go to the **Skills tab**
3. Select "Add AI Workflow" and choose from available workflows
4. Map input/output parameters as needed
5. Provide a clear description to help the LLM understand when to invoke it

### Execution Flow:

1. User makes a request in chat
2. LLM determines the workflow skill is needed
3. Worker extracts parameters from the conversation
4. Workflow executes with those parameters
5. Results return to the conversation

***

# MCP (Model Context Protocol)

**Model Context Protocol (MCP)** is an open standard that enables Workers to discover and use tools from external servers. MCP provides a standardized way to extend Worker capabilities without building custom integrations.

### What is MCP?

MCP defines how AI systems can:
* **Discover** available tools, prompts, and resources from external servers
* **Invoke** tools with structured parameters
* **Receive** results in a consistent format

This allows EverWorker to connect to any MCP-compatible server and immediately gain access to its capabilities.

### Key Concepts:

| Concept | Description |
|---------|-------------|
| **MCP Server** | An external service that exposes tools via the MCP protocol |
| **MCP Tools** | Individual capabilities exposed by a server (e.g., "search_database", "send_email") |
| **MCP Prompts** | Pre-defined prompt templates provided by the server |
| **MCP Resources** | Data or content URIs that can be accessed via the server |

### Connecting to MCP Servers

Builders can connect to external MCP servers to expand Worker capabilities:

1. **Navigate to MCP Settings**: Access MCP server configuration in the platform
2. **Add Server**: Provide the server URL and authentication details
3. **Sync Tools**: Discover available tools, prompts, and resources
4. **Assign to Workers**: Add MCP tools as skills in AI Workers

### Authentication Options:

MCP servers can be configured with different authentication methods:

* **None**: For public or localhost servers
* **Bearer Token**: Standard token-based authentication
* **API Key**: Key-based authentication via headers

### Using MCP Tools in Workers:

Once an MCP server is connected and synced:

1. Go to the **Skills tab** in AI Worker Builder
2. Select "Add MCP Tools"
3. Browse available tools from connected servers
4. Select tools to enable for this Worker
5. Tools appear as callable skills during conversations

### Multi-Provider Compatibility:

EverWorker automatically converts MCP tool definitions to work with different LLM providers:

* **OpenAI**: Converted to function calling format
* **Anthropic**: Converted to Claude tool format
* **Google**: Converted to Gemini function declarations

This means the same MCP tools work regardless of which LLM powers your Worker.

### Internal MCP Server:

EverWorker also exposes its own capabilities via an internal MCP endpoint (`/mcp`), allowing external systems to interact with the platform using the MCP protocol.

### Best Practices for MCP:

* **Verify Server Trust**: Only connect to MCP servers you trust
* **Review Tool Permissions**: Understand what each tool can do before enabling
* **Monitor Usage**: Track MCP tool invocations for security and debugging
* **Keep Synced**: Periodically re-sync to discover new or updated tools

***

# Skill Management

### Session-Level Control:

Users can enable or disable skills per session, allowing them to:
* Focus the Worker on specific tasks
* Prevent certain actions when not needed
* Troubleshoot by isolating skill behavior

### Visibility:

When chatting with a Worker, users can view:
* Which skills are currently enabled
* What each skill does (descriptions)
* When skills are being invoked (thinking trace)

### Permissions:

* **Builders** configure which skills are available to a Worker
* **Users** can toggle enabled skills within their session
* **Admins** can restrict certain skills organization-wide

***

# Summary

Skills are what transform AI Workers from conversational assistants into powerful automation tools. Whether through API integrations, embedded AI Workflows, or MCP-connected external tools, skills enable Workers to take action in the real world. The modular skill system ensures that capabilities can be added, updated, and managed independently - keeping Workers flexible, maintainable, and secure.
