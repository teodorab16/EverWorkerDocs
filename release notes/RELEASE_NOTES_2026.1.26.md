# Release Notes - January 26, 2026

## New Features

### Improved Worker Builder Interface
- **Separate Brain & Summary Tabs**: The worker builder now has dedicated tabs for Brain Instructions and Summary settings, making it easier to configure your workers
- **Advanced Settings**: New advanced settings section for more granular control

### Enhanced Memory Search
- Memory search now supports searching by both chunk ID and document ID, giving you more flexibility when looking up specific content

---

## Improvements

### Chat Experience
- **Better Auto-Scroll**: Completely redesigned chat scrolling behavior for more predictable and smoother experience, especially with large messages
- **Improved Rate Limit Handling**: Better detection and handling of rate limit errors with clearer retry guidance

### Canvas & Workflow Editor
- **GPT-5 Support**: Fixed an issue preventing GPT-5 models from being used in canvas workflows
- **Multimodal LLM Node**: Fixed generic fields configuration for multimodal LLM nodes
- **Chart Rendering**: Vega/Vega-Lite charts now properly respect width and height settings

### Worker Builder
- **Consistent Button Widths**: All primary action buttons in the worker builder now have consistent widths for a cleaner look
- **Fixed Double Saving**: Resolved an issue where workers could be saved twice unintentionally
- **LLM Node Parameters**: Fixed an issue with hardcoded LLM node parameters not saving correctly

### API Testing
- **OpenAPI Modal**: Empty values are now properly stripped from the test OpenAPI modal, preventing unnecessary errors

---

## Bug Fixes

- Fixed webhook crashes that could occur under certain conditions
- Fixed "Create a provider" link incorrectly redirecting to AI Workers instead of Providers
- Fixed UI flickering issues
- Fixed form validation behavior
- Fixed page reload issues
- Fixed padding inconsistencies
- Fixed i18n builder search pattern matching
- Fixed locale loading issues

---

## Performance & Stability

### Memory Leak Prevention
Comprehensive refactoring of MongoDB cursor management across the platform to prevent memory leaks. This includes:
- Proper cursor lifecycle handling
- Explicit cleanup using helper utilities
- Better error handling and resource management

### PostgreSQL Vector Search
- Fixed compatibility issues when using PostgreSQL as the vector search provider alongside standard MongoDB (non-Atlas). The system now gracefully handles environments without MongoDB Atlas Search enabled.

### Improved Retry Logic
- Fixed edge cases where retry counts could become invalid (NaN), ensuring more reliable execution recovery

---

## For Administrators

- Improved agent subscription performance by replacing reactive subscriptions with optimized list queries
- User message IDs are now properly tracked from the client for better traceability
