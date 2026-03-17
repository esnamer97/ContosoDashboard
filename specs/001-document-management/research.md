# Research: Document Upload & Management

## Decision: Local Filesystem Storage with Pluggable Abstraction

**Decision:** Implement document storage using the local filesystem for initial delivery, with a pluggable `IFileStorageService` abstraction to allow swapping to Azure Blob Storage (or another cloud provider) later.

**Rationale:**

- The project requirement explicitly calls for offline-only operation without cloud services for the initial release.
- A pluggable abstraction keeps business logic (upload, metadata, permissions) independent of storage implementation, making future migration straightforward.
- Local file storage is simplest to implement, debug, and test in the current environment.

**Alternatives Considered:**

- **Direct database storage (BLOB fields)**: Rejected due to complexity and potential database bloat; file systems are better suited for large binary files.
- **In-memory storage (for demo only)**: Insufficient for real usage and violates persistence requirements.

## Decision: Store Files Outside `wwwroot` with Authorization Checks

**Decision:** Store uploaded files in a directory outside of `wwwroot` (e.g., `%LOCALAPPDATA%/ContosoDashboard/uploads` or configurable path) and expose downloads via a secure endpoint that enforces authorization.

**Rationale:**

- Prevents direct URL guessing or unauthorized download via static file serving.
- Enables consistent authorization checks aligned with application role/project rules.
- Aligns with the security requirement that files must be stored securely and access-controlled.

**Alternatives Considered:**

- **Storing in `wwwroot` with ACLs**: Not feasible in Blazor Server without complex server configuration and risks accidental exposure.

## Decision: Metadata in SQL Server via EF Core

**Decision:** Persist document metadata in the existing SQL Server database using EF Core alongside current entities (User, Project, Task).

**Rationale:**

- Existing application already uses EF Core and SQL Server; adding new entities fits the current architecture.
- Makes it simple to query and join documents with users/projects/tasks.

**Alternatives Considered:**

- **NoSQL/document store**: Overkill for current scale and would introduce a new technology.

## Decision: Authorization Model

**Decision:** Use existing role-based authorization policies (`Employee`, `TeamLead`, `ProjectManager`, `Administrator`) and project membership rules to determine access to documents.

**Rationale:**

- Keeps security model consistent with the current app.
- Enables enforcing requirements (e.g., project managers can manage all project documents, owners can manage their own content).

**Alternatives Considered:**

- **Custom ACL per document**: Adds complexity; we can achieve required behavior with existing role/project membership model.

## Decision: User Experience

**Decision:** Provide Blazor pages/components for:

- Uploading documents (single/multi upload + metadata form)
- Viewing "My Documents" (sortable/filterable list)
- Viewing project documents (project page integration)
- "Shared with Me" view for shared documents
- Document detail page for preview/download/edit/delete

**Rationale:**

- Aligns with current Blazor Server UI pattern.
- Keeps navigation consistent with existing app.

**Alternatives Considered:**

- **Implement API-only and rely on separate SPA**: Not aligned with current architecture (Blazor Server) and would increase scope.

---

## Open Questions (No unresolved clarifications found)

No outstanding clarifications remain; requirements are sufficiently detailed to proceed with design and implementation.
