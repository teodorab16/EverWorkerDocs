---
title: ● Render Markdown
excerpt: >-
  A node used to convert Markdown content into HTML, PDF, or DOCX formats and
  return a public URL to the rendered file.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Document rendering node that converts Markdown content into HTML, PDF, or DOCX formats. This node delegates rendering to the Browser-as-a-Service (BaaS) backend and returns a public URL to the rendered file.

# When to Use

Use this node when your workflow needs to convert Markdown text into a polished document format. Ideal for report generation, document export, creating downloadable deliverables from AI-generated content, or any scenario where Markdown output from an LLM node needs to be converted into a shareable file.

# Parameters

* markdownContent (required) - The Markdown text to render
  * Type: textarea
  * Default: `# Hello World\nThis is a sample markdown.`
  * Placeholder: "Enter markdown content..."
  * Supports full Markdown syntax including headings, lists, tables, code blocks, and inline formatting
  * Example: `{{1.result.content}}`
* outputFormat (required) - The target document format
  * Type: select
  * Default: `html`
  * Options: `html` (HTML file), `pdf` (PDF document), `docx` (Microsoft Word document)
  * Placeholder: "Select output format"

# Raw Usage Example

```json
{
    name: "Generate PDF Report",
    description: "Render Markdown to HTML/PDF/DOCX",
    nodeId: "n",
    operationReference: {
        methodId: "render_markdown"
    },
    parameters: [
        { name: "markdownContent", value: "{{1.result.content}}" },
        { name: "outputFormat", value: "pdf" }
    ]
}
```

# Capabilities

* Converts Markdown to three output formats: HTML, PDF, and DOCX
* Returns a public URL to the rendered file for download or sharing
* Supports full Markdown syntax (headings, tables, code blocks, images, etc.)
* Integrates with the BaaS rendering service for high-fidelity output
* Can chain with Storage Upload or API Call nodes for further processing

# Advanced Features

* Template-driven rendering via the BaaS backend
* Execution context tracking for monitoring and debugging
* 30-second rendering timeout (configurable at the service level)
* Error handling with descriptive error messages on failure

# Result Access

`{{nodeId.result}}` - Public URL to the rendered file (string)

For example, if this is node 2:

```
{{2.result}}  →  "https://baas-service.example.com/files/rendered-abc123.pdf"
```

The returned URL can be:

* Passed to a **Storage Upload** node for persistent storage
* Sent via email or messaging integrations
* Returned through an **Output Node** as a workflow deliverable
* Fetched programmatically by downstream nodes

# Common Patterns

**LLM → Render → Output:**

```
Input Node (0) → Universal LLM (1) → Render Markdown (2) → Output Node (3)
                                        markdownContent: {{1.result.content}}
                                        outputFormat: pdf
```

**LLM → Render → Storage Upload:**

```
Universal LLM (1) → Render Markdown (2) → Storage Upload (3)
                      markdownContent: {{1.result.content}}    fileData: {{2.result}}
                      outputFormat: docx                       fileName: "report.docx"
```
