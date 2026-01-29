# Release Notes - January 19, 2026

## New Features

### PostgreSQL Vector Search Support
You can now use PostgreSQL with pgvector as an alternative vector search provider. This gives you more flexibility in choosing your infrastructure, especially if you're already using PostgreSQL in your stack.

### Provider Mapping for Workers
Workers can now use different AI providers dynamically when called. This allows the same worker to be executed with different provider configurations, giving you more flexibility in how you deploy and use your workers.

### Group Ownership for Providers & Connectors
Providers and Connectors now support group-based ownership with three visibility levels:
- **Own**: Private to you
- **Group**: Shared within your team/group
- **Global**: Available system-wide

This makes it easier to manage and share integrations across your organization.

### Internationalization (i18n) Support
The platform now includes i18n infrastructure, laying the groundwork for future multi-language support.

### Analytics Enhancements
Subworker node execution now includes detailed metadata, giving you better visibility into how your workflows execute.

---

## Improvements

### Universal Workers
- **Better Error Messages**: Rate limit errors now show clearer information including time-based guidance on when you can retry
- **Improved Description Field**: The worker description field is now a larger text area, making it easier to write detailed descriptions
- **Smoother Editing Experience**: Fixed visual glitches when switching between different connector types

### Canvas Editor
- **Nested JSON Field Editor**: You can now edit nested JSON objects directly in API node parameters with a visual editor
- **Step Validation**: Form steps now include validation to catch errors before execution

### Chat Interface
- **Multiple File Uploads**: Fixed an issue where uploading multiple files at once wasn't working correctly
- **Cleaner UI**: Removed the unnecessary "Sessions Loaded" notification message

### Memory & File Handling
- **Add Files via URL**: You can now add database and text files to memory directly via URL links
- **Improved Excel Parsing**: Excel file parsing is now more reliable

### Profile Settings
- **Avatar Upload**: Improved experience for uploading and previewing your profile photo

### LLM Model Selection
- The model selector now shows all available LLMs from your configured providers

### Error Messages
- **Microsoft SSO**: Better error messages when Microsoft credentials are misconfigured
- **Connector Authentication**: More informative error messages when token refresh fails or authentication expires

---

## Bug Fixes

- Fixed keyboard shortcuts not working in the raw JSON editor
- Fixed spacing issues in the JSON editor
- Fixed scheduled tasks getting stuck when cron locks become stale
- Fixed configuration reset issues in one-click deployments

---

## Security

- **89% Vulnerability Reduction**: Reduced known security vulnerabilities from 54 to 6 through comprehensive dependency updates and patching
- Updated MCP SDK to version 1.25.2 with security fixes

---

## For Administrators

- Improved logging for Microsoft SSO user synchronization
- Workers can now be sorted in the backend
- Fixed handling of users with null userType in certain authentication scenarios
