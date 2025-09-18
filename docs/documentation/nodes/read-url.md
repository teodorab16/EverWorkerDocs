---
title: ● Read URL
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Universal URL reader for web content that extracts and converts web page content to clean, structured text using Readability algorithms. Perfect for processing articles, documents, and web pages for AI analysis.

# When to Use

Use this node to extract clean text content from web pages for further processing by AI or other nodes. Ideal for content analysis, summarization, or when you need to process web articles in your workflow.

# Parameters

* url (required) - URL of the web page to read and extract content from
  * Examples:
    * `https://example.com/article`
    * `{{0.websiteUrl}}`
    * `{{previousNode.result.link}}`

# Raw Usage Example

```json
{
    name: "Extract Article Content",
    description: "Read URL Node - extract clean text from web article", 
    nodeId: "n",
    operationReference: {
        methodId: "read_url"
    },
    parameters: [
        {
            name: "url",
            value: "https://blog.example.com/article" // Article URL to extract
        }
    ]
}
```

<br />
