# API Contracts: Document Upload & Management

This document describes the public-facing interfaces that other systems or UI components rely on. In this project, the primary consumer is the Blazor Server UI, but these contracts can also support future API clients.

## Service Layer Contract (`IFileStorageService`)

### Interface

```csharp
public interface IFileStorageService
{
    Task<FileUploadResult> UploadAsync(Stream fileStream, string fileName, string contentType, CancellationToken cancellationToken);
    Task<Stream> DownloadAsync(string storagePath, CancellationToken cancellationToken);
    Task<bool> DeleteAsync(string storagePath, CancellationToken cancellationToken);
    Task<Uri> GetUrlAsync(string storagePath);
}
```

### Expected Behavior

- `UploadAsync` generates a unique storage path (e.g., `{userId}/{projectId}/{guid}.{ext}`) and returns the resulting path and metadata.
- `DownloadAsync` returns a readable stream for the requested file; caller is responsible for authorization checks.
- `DeleteAsync` removes the file from storage and returns `true` if it was deleted.
- `GetUrlAsync` returns a URL that can be used to download the file (used when using blob storage or signed URLs).

---

## Endpoint Contract: Document Management (REST-style)

### Upload Documents

- **URL**: `POST /api/documents/upload`
- **Request**: `multipart/form-data` with file(s) and JSON metadata envelope
- **Response**: `200 OK` with created document metadata (id, title, category, storage path, etc.)

### List My Documents

- **URL**: `GET /api/documents/my`
- **Query Parameters**: `search`, `category`, `projectId`, `sortBy`, `page`, `pageSize`
- **Response**: `200 OK` with paginated list of document summaries.

### Get Project Documents

- **URL**: `GET /api/projects/{projectId}/documents`
- **Response**: `200 OK` with list of documents for the project.

### Download Document

- **URL**: `GET /api/documents/{documentId}/download`
- **Response**: `200 OK` with file payload (requires authorization).

### Preview Document

- **URL**: `GET /api/documents/{documentId}/preview`
- **Response**: `200 OK` with inline content-disposition for browser preview.

### Update Document Metadata

- **URL**: `PUT /api/documents/{documentId}`
- **Body**: JSON with updated title/description/category/tags.
- **Response**: `204 No Content` on success.

### Delete Document

- **URL**: `DELETE /api/documents/{documentId}`
- **Response**: `204 No Content` on success.

### Share Document

- **URL**: `POST /api/documents/{documentId}/share`
- **Body**: JSON with `sharedWithUserId` or `sharedWithTeamId`.
- **Response**: `201 Created` with share record metadata.

---

## UI Contract (Blazor Components)

Components should communicate via a shared service interface (e.g., `IDocumentService`) that implements the API contract above and returns strongly typed models.

### Example Model: `DocumentSummary`

```csharp
public class DocumentSummary
{
    public int DocumentId { get; set; }
    public string Title { get; set; }
    public string Category { get; set; }
    public DateTime UploadDate { get; set; }
    public long FileSizeBytes { get; set; }
    public string MimeType { get; set; }
    public int? ProjectId { get; set; }
    public bool IsShared { get; set; }
}
```

---

## Notes

- The endpoints described above are a contract; the initial implementation can be a Blazor component-backed service (no separate Web API project). The core requirement is that the service abstraction provides these operations.
- If the project expands to include an external API, these contracts can be exposed by a dedicated controller layer.
