# ContosoDashboard Development Guidelines

Auto-generated from all feature plans. Last updated: 2026-03-16

## Active Technologies
- C# 12 / .NET 8 (net8.0) + ASP.NET Core Blazor Server, Entity Framework Core (SQL Server), Microsoft.AspNetCore.Authentication.Cookies, Microsoft.Identity.Web (for identity patterns), MudBlazor (UI library if already used) or internal components. (001-document-management)
- SQL Server via EF Core for metadata; Local filesystem storage for document files (outside `wwwroot`, e.g., `%LOCALAPPDATA%/ContosoDashboard/uploads` or an appsetting-defined path). (001-document-management)

- [e.g., Python 3.11, Swift 5.9, Rust 1.75 or NEEDS CLARIFICATION] + [e.g., FastAPI, UIKit, LLVM or NEEDS CLARIFICATION] (001-document-management)

## Project Structure

```text
backend/
frontend/
tests/
```

## Commands

cd src; pytest; ruff check .

## Code Style

[e.g., Python 3.11, Swift 5.9, Rust 1.75 or NEEDS CLARIFICATION]: Follow standard conventions

## Recent Changes
- 001-document-management: Added C# 12 / .NET 8 (net8.0) + ASP.NET Core Blazor Server, Entity Framework Core (SQL Server), Microsoft.AspNetCore.Authentication.Cookies, Microsoft.Identity.Web (for identity patterns), MudBlazor (UI library if already used) or internal components.

- 001-document-management: Added [e.g., Python 3.11, Swift 5.9, Rust 1.75 or NEEDS CLARIFICATION] + [e.g., FastAPI, UIKit, LLVM or NEEDS CLARIFICATION]

<!-- MANUAL ADDITIONS START -->
<!-- MANUAL ADDITIONS END -->
