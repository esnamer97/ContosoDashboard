# Tasks: Document Upload & Management

**Input**: Design documents from `/specs/001-document-management/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

**Tests**: Tests are OPTIONAL - not explicitly requested in the feature specification, so no test tasks included.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Path Conventions

- **Single project**: `ContosoDashboard/` at repository root
- Paths shown below assume Blazor Server project structure

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and basic structure

- [ ] T001 Create project structure per implementation plan
- [ ] T002 Initialize C# .NET 8 project with ASP.NET Core Blazor Server dependencies
- [ ] T003 [P] Configure linting and formatting tools

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core infrastructure that MUST be complete before ANY user story can be implemented

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

- [ ] T004 Setup database schema and EF Core migrations for new entities
- [ ] T005 [P] Implement file storage abstraction (IFileStorageService)
- [ ] T006 [P] Setup API routing and middleware structure for document endpoints
- [ ] T007 Create base document entities (Document, DocumentShare, DocumentAuditLog)
- [ ] T008 Configure error handling and logging infrastructure for file operations
- [ ] T009 Setup environment configuration for file storage paths

**Checkpoint**: Foundation ready - user story implementation can now begin in parallel

---

## Phase 3: User Story 1 - Upload & Manage Own Documents (Priority: P1) 🎯 MVP

**Goal**: Enable users to upload documents with metadata and view them in a personal list

**Independent Test**: Upload a file, see it in "My Documents" with correct metadata, and verify access controls

### Implementation for User Story 1

- [ ] T010 [P] [US1] Create Document model in ContosoDashboard/Models/Document.cs
- [ ] T011 [P] [US1] Create DocumentShare model in ContosoDashboard/Models/DocumentShare.cs
- [ ] T012 [P] [US1] Create DocumentAuditLog model in ContosoDashboard/Models/DocumentAuditLog.cs
- [ ] T013 [US1] Update ApplicationDbContext to include new document entities
- [ ] T014 [US1] Implement IFileStorageService interface in ContosoDashboard/Services/IFileStorageService.cs
- [ ] T015 [US1] Implement LocalFileStorageService in ContosoDashboard/Services/LocalFileStorageService.cs
- [ ] T016 [US1] Create DocumentService in ContosoDashboard/Services/DocumentService.cs
- [ ] T017 [US1] Create upload endpoint in ContosoDashboard/Pages/Documents/Upload.cshtml.cs
- [ ] T018 [US1] Create "My Documents" page in ContosoDashboard/Pages/Documents/MyDocuments.razor
- [ ] T019 [US1] Add file validation (type, size) in ContosoDashboard/Services/DocumentService.cs
- [ ] T020 [US1] Implement authorization checks for document access in DocumentService
- [ ] T021 [US1] Add progress indicator for uploads in ContosoDashboard/Pages/Documents/Upload.razor
- [ ] T022 [US1] Create error handling for upload failures in DocumentService
- [ ] T023 [US1] Add metadata editing functionality in ContosoDashboard/Pages/Documents/EditDocument.razor
- [ ] T024 [US1] Implement document deletion for owners in DocumentService
- [ ] T025 [US1] Add audit logging for upload/delete actions in DocumentService
- [ ] T026 [US1] Create download endpoint with authorization in ContosoDashboard/Pages/Documents/Download.cshtml.cs

**Checkpoint**: At this point, User Story 1 should be fully functional and testable independently

---

## Phase 4: User Story 2 - Browse, Search, and Filter Documents (Priority: P2)

**Goal**: Allow users to find documents through search and filtering

**Independent Test**: Search for documents and apply filters, verifying results appear quickly

### Implementation for User Story 2

- [ ] T027 [US2] Implement search by title/tags/uploader in DocumentService.cs
- [ ] T028 [US2] Add category and project filters to document list in MyDocuments.razor
- [ ] T029 [US2] Create project documents view in ContosoDashboard/Pages/Projects/ProjectDocuments.razor
- [ ] T030 [US2] Optimize database queries for search performance in DocumentService
- [ ] T031 [US2] Add sorting options (date, title, size) to document lists in MyDocuments.razor
- [ ] T032 [US2] Implement pagination for large document lists in DocumentService
- [ ] T033 [US2] Add date range filtering in MyDocuments.razor
- [ ] T034 [US2] Create search UI component in ContosoDashboard/Shared/DocumentSearch.razor
- [ ] T035 [US2] Ensure search respects authorization (only accessible documents) in DocumentService

**Checkpoint**: At this point, User Stories 1 AND 2 should both work independently

---

## Phase 5: User Story 3 - Share, Preview, and Manage Document Access (Priority: P3)

**Goal**: Enable document sharing, preview, and access management

**Independent Test**: Share a document, verify recipient notification and access

### Implementation for User Story 3

- [ ] T036 [US3] Implement document sharing in DocumentService.cs
- [ ] T037 [US3] Create "Shared with Me" view in ContosoDashboard/Pages/Documents/SharedDocuments.razor
- [ ] T038 [US3] Add notification system for shared documents in NotificationService.cs
- [ ] T039 [US3] Implement preview for PDF/images in ContosoDashboard/Pages/Documents/Preview.razor
- [ ] T040 [US3] Add file replacement functionality in EditDocument.razor
- [ ] T041 [US3] Extend authorization for project managers to delete project documents in DocumentService
- [ ] T042 [US3] Create share UI component in ContosoDashboard/Shared/DocumentShare.razor
- [ ] T043 [US3] Add audit logging for share/preview actions in DocumentService
- [ ] T044 [US3] Implement team sharing (if teams exist) in DocumentService

**Checkpoint**: All user stories should now be independently functional

---

## Phase 6: User Story 4 - Integrate Documents with Tasks & Dashboard (Priority: P3)

**Goal**: Connect documents to existing task and dashboard workflows

**Independent Test**: Attach document to task and see recent documents on dashboard

### Implementation for User Story 4

- [ ] T045 [US4] Add document attachment to task model in Models/TaskItem.cs
- [ ] T046 [US4] Create task document attachment UI in ContosoDashboard/Pages/Tasks/TaskDetails.razor
- [ ] T047 [US4] Implement "Recent Documents" dashboard widget in ContosoDashboard/Pages/Index.razor
- [ ] T048 [US4] Update task detail page to show attached documents in TaskDetails.razor
- [ ] T049 [US4] Add document count to dashboard summary in DashboardService.cs
- [ ] T050 [US4] Ensure attachments associate documents with task's project in DocumentService

**Checkpoint**: Full integration complete

---

## Phase 7: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect multiple user stories

- [ ] T051 [P] Documentation updates in README.md and quickstart.md
- [ ] T052 Code cleanup and refactoring across document-related files
- [ ] T053 [P] Security review and hardening for file operations
- [ ] T054 Performance optimization for document queries
- [ ] T055 Run quickstart.md validation and update as needed

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories
- **User Stories (Phase 3+)**: All depend on Foundational phase completion
  - User stories can then proceed in parallel (if staffed)
  - Or sequentially in priority order (P1 → P2 → P3)
- **Polish (Final Phase)**: Depends on all desired user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational (Phase 2) - No dependencies on other stories
- **User Story 2 (P2)**: Can start after Foundational (Phase 2) - May integrate with US1 but should be independently testable
- **User Story 3 (P3)**: Can start after Foundational (Phase 2) - May integrate with US1/US2 but should be independently testable

### Within Each User Story

- Models before services
- Services before endpoints
- Core implementation before integration
- Story complete before moving to next priority

### Parallel Opportunities

- All Setup tasks marked [P] can run in parallel
- All Foundational tasks marked [P] can run in parallel (within Phase 2)
- Once Foundational phase completes, all user stories can start in parallel (if team capacity allows)
- Models within a story marked [P] can run in parallel
- Different user stories can be worked on in parallel by different team members

---

## Parallel Example: User Story 1

```bash
# Launch all models for User Story 1 together:
Task: "Create Document model in ContosoDashboard/Models/Document.cs"
Task: "Create DocumentShare model in ContosoDashboard/Models/DocumentShare.cs"
Task: "Create DocumentAuditLog model in ContosoDashboard/Models/DocumentAuditLog.cs"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational (CRITICAL - blocks all stories)
3. Complete Phase 3: User Story 1
4. **STOP and VALIDATE**: Test User Story 1 independently
5. Deploy/demo if ready

### Incremental Delivery

1. Complete Setup + Foundational → Foundation ready
2. Add User Story 1 → Test independently → Deploy/Demo (MVP!)
3. Add User Story 2 → Test independently → Deploy/Demo
4. Add User Story 3 → Test independently → Deploy/Demo
5. Each story adds value without breaking previous stories

### Parallel Team Strategy

With multiple developers:

1. Team completes Setup + Foundational together
2. Once Foundational is done:
   - Developer A: User Story 1
   - Developer B: User Story 2
   - Developer C: User Story 3
3. Stories complete and integrate independently

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to specific user story for traceability
- Each user story should be independently completable and testable
- Commit after each task or logical group
- Stop at any checkpoint to validate story independently
