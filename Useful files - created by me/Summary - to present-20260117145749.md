# Summary - to present

### The Problem
❌ No departmental boundaries
→ Marketing sees Finance's sensitive workers
→ HR data visible to everyone

❌ Binary access control only
→ Private (only me) OR Public (everyone)
→ No "Marketing team only" or "Marketing + Sales only"

❌ Cannot replicate company structure
→ Can't organize by teams, departments, projects
→ No isolation between organizational units

❌ Blocks enterprise adoption
→ Large companies need proper access control
→ Compliance requirements (SOX, HIPAA, etc.)
→ Can't sell to enterprise without this

❌ No cross-team collaboration control
→ Either everyone sees it or only creator
→ No "Sales + Marketing collaboration" option

BOTTOM LINE:
Platform built for individuals, not organizations
Needed team-based access control to grow
* * *
### The Naming![](https://t9015421689.p.clickup-attachments.com/t9015421689/94b0d47b-3358-408f-b334-eed32b83e140/groups-teams.png)
* * *
### The Current Status

What We Have Today: "Groups" (Incomplete)

✅ WHAT WE BUILT (Foundation ~60%):
*   Group creation & management
*   Multi-group membership with roles
*   Group switching capability
*   Basic visibility: Private/Public to group
*   Worker filtering: All/Global/Group/Own
*   Knowledge can be Private/Public (company-wide)

❌ WHAT'S INCOMPLETE:

UX PROBLEMS:
*   No visible indicator of current group
*   Confusing terminology (Global group vs Global workers)
*   Users don't understand new behaviour
*   "Public" meaning changed (was company-wide, now group-only)
*   Filters unclear

MISSING FEATURES:
*   Proper UX
*   Share with "Group(s)"
*   No "Shared" visibility (can't share to specific groups)
*   No Company-Wide Management (Platform Admin only)
*   **Connectors NOT scoped**
*   **Analytics NOT scoped**
*   **Knowledge NOT scoped**
*   **Providers**
*   **Data Source for EKE**
*   Connector → OAuth → ??
*   No dependency validation (workers can fail silently)
*   No admin role distinction (any admin manages any group)
*   Default is Private (should be Team/Organization)

RESULT: Half-finished feature confusing users, blocking adoption

* * *
### The Solution

Complete "Teams" Feature - What We're Building

CORE CONCEPT:
Teams = logical containers grouping users + entities
(Workers, Connectors, Knowledge) by department

STRUCTURE:
Acme Corp (Company)
├── Marketing Team (24 users, 61 workers)
├── Sales Team (18 users, 45 workers)
├── Finance Team (12 users, 28 workers)
└── Engineering Team (31 users, 89 workers)

KEY CAPABILITIES:
✅ Team isolation (Marketing ≠ Sales by default)
✅ Multi-team membership (Alice: Builder in Marketing, User in Sales)
✅ Flexible sharing (share specific workers to specific teams)
✅ Always-visible context (users know where they are)
✅ 4 visibility levels (Private, Team, Shared, Company-Wide)
✅ Dependency validation (prevent failures)
✅ Team-scoped connectors (Marketing HubSpot Connector ≠ Sales HubSpot Connector)
✅ Role distinction (Team Admin vs Platform Admin)
✅ Clear errors & guidance

FIXES ALL CURRENT PROBLEMS + ADDS MISSING FEATURES

* * *
### To be decided

1. **Providers (OpenAPI Specs) Scoping**
    *   Are Providers team-scoped or company-wide?
    *   Who can upload/manage Providers? (Integrations Manager? Platform Admin only?)
    *   Current spec covers Connectors (instances) but not clear on Provider definitions
2. **Shared Entity Editing Rights**
    *   When Marketing shares worker to Sales, who can edit it?
    *   Option A: Only owner team (Marketing) can edit
    *   Option B: All teams with access can edit (conflicts?)
    *   Option C: Read-only for shared teams, must duplicate to edit
3. **Entity Ownership When User Removed**
    *   User is removed from Marketing team
    *   What happens to their Private entities?
    *   Option A: Stay with user (follow them to other teams)
    *   Option B: Become orphaned / deleted
    *   Option C: Transferred to team admin
4. **Platform Admin Entity Creation**
    *   When Platform Admin creates worker, which team does it belong to?
    *   Must they be "in" a team context?
    *   Or can they create "unassigned" entities?
5. **Default Team for New Users**
    *   New user signs up - which team do they join?
    *   Is there a "Default" team?
    *   Or must admin assign them before they can do anything?

1. **Guest Users / External Collaborators**
    *   Can external users (contractors, agencies) join teams?
    *   If yes, what restrictions? (User role only? No Private entities?)
    *   How do they authenticate? (SSO, invite-only?)
2. **Knowledge Collections - Shared Editing**
    *   When knowledge shared between Marketing + Sales:
    *   Option A: Single source (both edit same collection)
    *   Option B: Duplicated (each team has copy)
    *   Option C: Owner team edits, others read-only
3. **Schedulers - Team Scoping**
    *   Are scheduled tasks team-scoped?
    *   When scheduled task runs, which team context?
    *   Can scheduler trigger workers in different team?
4. **MCP Servers - Team Scoping**
    *   Are MCP servers team-scoped or company-wide?
    *   Each team configures own MCP servers?
    *   Or Platform Admin configures for all teams?