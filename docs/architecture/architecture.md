# Architecture

## 1. Overview
FileManiac is a **local-first application**: a Spring Boot backend (embedded server, bound to `localhost` only) paired with an Angular frontend, packaged as a single executable JAR. Spring Boot serves the built Angular static files directly (`ng build` output copied into `src/main/resources/static`), so there is no separate deployment, no external network exposure, and no Electron/Tauri wrapper needed. The application follows Clean Architecture principles: business logic stays independent from the UI, the API layer, PDF processing libraries, the file system, and other external dependencies.

## 2. Architectural Goals
- Separation of concerns
- Testability
- Maintainability
- Low coupling
- Replaceable infrastructure components
- **Local processing**: the embedded server binds only to `127.0.0.1`; no PDF or file data ever leaves the user's machine, and no data is sent to any external/cloud service

## 3. Architecture Style
```
                 ┌──────────────────────┐
                 │   Frontend (Angular) │   <- SPA, served locally by Spring Boot
                 └──────────┬───────────┘
                            │ HTTP (localhost only)
                            ▼
                 ┌──────────────────────┐
                 │   API (Controllers)  │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌───────────────────────┐
                 │     Application       │
                 └──────────┬────────────┘
                            │            ▲
                            ▼            │
                 ┌────────────────────┐  │
                 │       Domain       │  │
                 └────────────────────┘  │
                             ▲           │
                             │           │
                 ┌───────────┴───────────┐
                 │    Infrastructure     │
                 └───────────────────────┘
```

## 4. System Components
Frontend (Angular)
    Components
    Angular services (HTTP calls to the local API)
    User interaction

API (Controllers)
    REST Controllers (e.g. `MergePdfController`)
    Request/Response DTOs
    Exception handling (`@ControllerAdvice`)

Application
    Use cases
    Application services
    Interfaces (Java naming: `PdfService`)
    DTOs

Domain
    Business rules
    Domain models
    Domain exceptions

Infrastructure
    PDF processing (e.g. Apache PDFBox)
    File system access
    Logging (SLF4J/Logback)
    External libraries

## 5. Dependency Rules
Domain
    must not depend on any other layer.

Application
    may depend on Domain.

API (Controllers)
    may depend on Application only (never directly on Infrastructure or Domain).

Infrastructure
    may depend on Application and Domain.

Frontend (Angular)
    depends on the API only via HTTP calls (no compiled/code dependency) — it is packaged and served by Spring Boot, but remains logically decoupled from the backend layers.

## 6. Data Flow
User
 ↓
Frontend (Angular, in browser at localhost)
 ↓ HTTP request
MergePdfController
 ↓
MergePdf Use Case
 ↓
PdfService (interface)
 ↓
PDF Infrastructure (Apache PDFBox)
 ↓
Output File
 ↓ HTTP response
Frontend (Angular) shows result to user

## 7. PDF Processing
Application
    ↓
PdfService (interface)
    ↑
PdfServiceImpl (Infrastructure)
    ↓
PDF Library (Apache PDFBox)

## 8. Error Handling
Invalid PDF
    ↓
Infrastructure
    ↓
Application exception/result
    ↓
API (`@ControllerAdvice` maps to a clean HTTP error response)
    ↓
Frontend (Angular)
    ↓
User-friendly message

## 9. Logging
Log:
- Operation started
- Operation completed
- Operation failed
- Processing duration
- Number of files

Do not log:
- PDF contents
- Sensitive metadata
- Full document paths when unnecessary

## 10. Testing Strategy
Domain
    → Unit tests (JUnit 5)

Application
    → Unit tests (JUnit 5)
    → Integration tests (Spring Boot Test)

API (Controllers)
    → Integration/contract tests (MockMvc / WebTestClient)

Infrastructure
    → Integration tests

Frontend (Angular)
    → Unit tests (Jasmine/Karma)
    → E2E tests (future)