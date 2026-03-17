# Data Model: Document Upload & Management

This document captures the core entities and their relationships for the document management feature.

## Entity: Document

Represents an uploaded file and its metadata.

**Fields**

- `DocumentId` (int, PK)
- `Title` (string, required)
- `Description` (string, optional)
- `Category` (string, required) — one of: "Project Documents", "Team Resources", "Personal Files", "Reports", "Presentations", "Other"
- `Tags` (string, optional) — stored as a delimited string (e.g., comma-separated) or normalized into a separate table if needed later
- `UploadDate` (DateTime, required) — UTC timestamp
- `UploadedByUserId` (int, FK → User.UserId) — user who uploaded the document
- `ProjectId` (int?, FK → Project.ProjectId) — optional association to a project
- `FileSizeBytes` (long, required)
- `MimeType` (string, required, max 255)
- `StoragePath` (string, required) — full or relative path to the file in storage
- `OriginalFileName` (string, required) — the file name as uploaded by the user (for display)
- `IsDeleted` (bool, required) — soft delete marker (true once deleted)
- `DeletedAt` (DateTime?, optional) — timestamp when deleted (optional for audit/reporting)

**Indexes**

- Index on `UploadedByUserId` (for "My Documents")
- Index on `ProjectId` (for project document lists)
- Index on `Category` (filtering)
- Index on `UploadDate` (sorting)

## Entity: DocumentShare

Represents a sharing relationship from an owner to another user or team.

**Fields**

- `DocumentShareId` (int, PK)
- `DocumentId` (int, FK → Document.DocumentId)
- `SharedByUserId` (int, FK → User.UserId)
- `SharedWithUserId` (int?, FK → User.UserId)
- `SharedWithTeamId` (int?, FK → ProjectMember or a future Team entity) — optional
- `SharedDate` (DateTime, required)
- `ExpiresAt` (DateTime?, optional) — optional expiration

**Notes**

- If the app does not currently have a `Team` entity, sharing to teams can be represented via the existing `ProjectMember` relationships (e.g., share with all members of a project).

## Entity: DocumentAuditLog

Tracks actions performed on documents for reporting and compliance.

**Fields**

- `DocumentAuditLogId` (int, PK)
- `DocumentId` (int, FK → Document.DocumentId)
- `Action` (string, required) — e.g., "Upload", "Download", "Delete", "Share", "Preview", "MetadataUpdate"
- `PerformedByUserId` (int, FK → User.UserId)
- `PerformedAt` (DateTime, required)
- `Details` (string, optional) — free-text details such as reason for sharing, error details, or old/new values.

**Indexes**

- Index on `DocumentId`
- Index on `PerformedByUserId`
- Index on `PerformedAt`

## Relationships

- **Document → User (Uploader)**: Many-to-one (each document is uploaded by one user).
- **Document → Project**: Many-to-one (documents may optionally belong to a project).
- **Document → DocumentShare**: One-to-many (a document can be shared multiple times).
- **Document → DocumentAuditLog**: One-to-many (logs for a document appear in the audit log).

## Data Migrations

- Add new EF Core entities and configure model relationships in `ApplicationDbContext`.
- Add migrations to create `Documents`, `DocumentShares`, and `DocumentAuditLogs` tables.
- Ensure the `Documents` table has appropriate indexes for query performance.

## Notes

- For tags, start with a simple comma-separated string to reduce schema complexity and refactor later if tagging needs scale/advanced querying.
- `IsDeleted` is used to support recoverability and to avoid complex cascading deletes; physical deletion can be performed by a background cleanup job if needed.
