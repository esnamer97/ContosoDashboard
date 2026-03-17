# Quickstart: Document Upload & Management Feature

This guide helps developers run the ContosoDashboard app locally and validate the new document upload and management feature.

## Prerequisites

- .NET 8 SDK installed (https://dotnet.microsoft.com/download)
- A supported database (SQL Server / LocalDB) accessible via the `DefaultConnection` connection string in `ContosoDashboard/appsettings.json`
- (Optional) A browser (Chrome, Edge, Firefox, Safari) for UI testing

## Setup

1. **Ensure the feature branch is checked out**

```powershell
git checkout 001-document-management
```

2. **Restore dependencies**

```powershell
dotnet restore ContosoDashboard/ContosoDashboard.csproj
```

3. **Configure the uploads directory**

By default, the feature will store documents in a local directory outside `wwwroot`. Ensure the folder exists and is writable.

Example path (Windows):

```powershell
$env:LOCALAPPDATA\ContosoDashboard\uploads
New-Item -ItemType Directory -Path $env:LOCALAPPDATA\ContosoDashboard\uploads -Force
```

If the app supports a configuration setting (e.g., `DocumentStorage:BasePath`), ensure it is set in `appsettings.Development.json`.

4. **Run the application**

```powershell
dotnet run --project ContosoDashboard/ContosoDashboard.csproj
```

5. **Open the app in a browser**

Navigate to `https://localhost:5001` (or the URL printed in the console).

6. **Log in with a seeded user**

The app seeds sample users; use one of the seeded emails (e.g., `admin@contoso.com`) and the mock login flow.

## Validating Document Upload

1. Navigate to the new **Documents** section in the app (a page may be added under the main navigation).
2. Use the **Upload** form to select one or more files (PDF, DOCX, XLSX, PNG, JPG, TXT) and provide required metadata.
3. Confirm you see a progress indicator and a success message.
4. Verify the uploaded file appears in **My Documents** with correct metadata.

## Validating Authorization

- Confirm that users only see their own documents unless they are project managers or explicitly shared with them.
- Try downloading a file and confirm the content matches the uploaded file.

## Validating Search & Filtering

1. Upload multiple documents with different titles/categories.
2. Use the search bar to search by title, tags, or uploader.
3. Apply category/project filters and confirm the list updates correctly.

## Notes

- If the local database is reset, uploaded files remain on disk but will no longer be referenced by metadata until re-uploaded.
- Use the audit log feature (if implemented) to verify upload/download/delete events are recorded.
