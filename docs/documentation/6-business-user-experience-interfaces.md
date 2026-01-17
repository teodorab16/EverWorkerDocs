---
title: Business User Experience & Interfaces
excerpt: This section covers the business user-facing interfaces and experience design.
deprecated: false
hidden: false
icon: fad fa-square-6
metadata:
  robots: index
---
### Topics Covered:

* Worker Chat: Text, image, URL input and chat export (PDF/DOCX)
* Workers Launchpad: Central hub for users
* Session Management: Auto-titled sessions, history, context, and persistence
* File Upload & Management: Temporary vs persistent file handling
* Search & Filtering: Tag-based and semantic search

***

# Worker Chat

The primary interaction interface where Users communicate with AI Workers.

* Supports **text, image, and URL input**
* Users can **view the Worker's skills** and **knowledge** sources
* Displays the **Worker's thinking trace** (collapsed chain-of-thought) for transparency
* **Custom welcome messages** can be configured per Worker to greet users
* Chat controls:
  * Enter to send
  * Shift + Enter for new lines
  * Paste URLs inline
  * Attach files and images in chat

### Chat Export

Export your conversation history in multiple formats:

* **PDF Export**: Download the chat as a formatted PDF document
* **DOCX Export**: Download the chat as a Microsoft Word document

Exports include the full conversation history with messages, responses, and formatting preserved.

***

# Session Management

Each new conversation with a Worker creates a **dedicated session** with its own memory, settings, and context.

* All sessions are **automatically titled** (based on summary + timestamp)
* Users can:
  * **Rename**, **search**, or **delete** sessions
  * Enable/disable memory or skills for a specific session
  * See a list of previous sessions in the left-hand panel
* Planned: **Graph-based session navigation** (jump from old message threads into new sessions)

***

# File Upload & Management

Users can upload documents to provide additional context during conversations.

* **In-chat uploads** are temporary (valid only during the session)
* **Persistent files** are uploaded via the Session Settings panel, becoming part of session memory
* **Supported formats** : You can upload the following file types in chat or session context:
  > .pdf, .docx, .doc, .txt, .md, .rtf, .xlsx, .csv
  :warning: Only text-based PDF files are supported. Images and scanned PDFs cannot be processed at this time.
* Files are embedded into vector memory and used for response generation when enabled

***

# Search & Filtering

Users can easily discover and navigate content through search and tag systems.

* **Tag-based filters** on the Worker list (customizable by Builder)
* **Semantic search** in memory items, session names, and chat logs
* Planned enhancements:
  * Search by Worker capabilities (e.g., "find Workers that connect to Salesforce")
  * Combined filters (e.g., tags + activity status)

***

# Summary

EverWorker's user experience is built around **clarity, control, and context continuity**. From rich, multi-modal chat to evolving session intelligence and personalized launchpads, the interface aims to make advanced AI interactions **feel familiar, productive, and trustworthy** - especially for non-technical users.
