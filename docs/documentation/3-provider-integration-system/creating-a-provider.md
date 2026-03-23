---
title: Creating a Provider
deprecated: false
hidden: false
icon: far fa-angles-down
metadata:
  robots: index
---
A Provider in Everworker is your configuration template for connecting to any external API or service. Creating a Provider sets up all access, authentication, and basic structural information for future connectors and workflow nodes.

This guide describes parameters and fields you’ll find in the Provider creation screen.

1. **Choose File:** (OpenAPI Specs, optional)

   _Purpose:_
   `Allows you to import the API schema automatically via OpenAPI/Swagger file.`

   _How To:_
   `Click the file picker and upload the .json or .yaml file provided by the API owner.`
2. **Title**

   _Purpose:_
   `Friendly name for this Provider, easily readable and unique within your workspace.`

   _Example:_
   `Salesforce Prod, HubSpot Demo, Custom Private API`
3. **Summary**
   Purpose:
   A one-line summary or tag-line for the Provider’s function.
   Example:
   “Main integration with HubSpot for contacts and deals.”
4. **Description**
   Purpose:
   Longer-form detail on the Provider, use it to explain usage, scope, or internal notes.
   Example:
   “This Provider handles all core CRM object endpoints for our marketing automation workflows. Use only with admin-scoped secrets.”
5. **Global ID**
   Purpose:
   A unique machine-readable identifier for this Provider.
   Used by connectors and code—usually lowercase, no spaces.
   Example:
   hubspot.crm, mycompany.privateapi
6. **Version**
   Purpose:
   String to track API/provider versioning for upgrade and compatibility control.
   Example:
   v1.0, 2023-04, beta
7. **Servers (Add Server)**
   Purpose:
   Add one or more base URLs ("servers") that your API uses.
   How To:
   Click “Add Server” and enter each base URL (e.g., https://api.hubapi.com).
   If the API is available in multiple regions or for different environments (test/prod), add all needed.
8. **OAuth Configuration**
   If you select OAuth-based authentication, you’ll configure these specific fields:

   Default Authentication Mode

   * App token: Uses a global credential for all calls (no per-user auth flow).
   * User OAuth: Each user completes OAuth and gets their token.
   * Hybrid: Combines app credentials (client_id/client_secret) with per-user tokens (sometimes required for enterprise APIs).
   **OAuth Scopes**

   * The permissions explicitly requested from the API (comma or space separated).
   * Example: contacts.read deals.write
   **Custom Authorization URL (Optional)**

   * If API provider uses a non-standard authentication initiation URL, specify here.
   **Custom Token URL (Optional)**

   * If exchanging a code/token is done via a non-standard endpoint.

_If using OAuth: Fill out all above, and be sure your secrets include client_id and client_secret as appropriate._
