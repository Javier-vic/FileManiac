# Architecture

## 1. Overview
FileManiac will use a layered architecture based on Clean Architecture principles. The main goal is to separate the application's business logic from the user interface, PDF processing libraries, file system, and other external dependencies.

## 2. Architectural Goals
- Separation of concerns
- Testability
- Maintainability
- Low coupling
- Replaceable infrastructure components
- Local processing

## 3. Architecture Style
                 ┌──────────────────────┐
                 │      Presentation    │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │     Application      │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │        Domain        │
                 └──────────────────────┘
                            ▲
                            │
                 ┌──────────┴───────────┐
                 │    Infrastructure    │
                 └──────────────────────┘

## 4. System Components
UI
    User interface
    ViewModels
    User interaction

Application
    Use cases
    Application services
    Interfaces
    DTOs

Domain
    Business rules
    Domain models
    Domain exceptions

Infrastructure
    PDF processing
    File system
    Logging
    External libraries

## 5. Dependency Rules
Domain
    must not depend on any other project.

Application
    may depend on Domain.

Infrastructure
    may depend on Application and Domain.

UI
    may depend on Application.

## 6. Data Flow
User
 ↓
UI
 ↓
MergePdf Use Case
 ↓
IPdfService
 ↓
PDF Infrastructure
 ↓
Output File

## 7. PDF Processing
Application
    ↓
IPdfService
    ↑
PdfService
    ↓
PDF Library

## 8. Error Handling
Invalid PDF
    ↓
Infrastructure
    ↓
Application exception/result
    ↓
UI
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
    → Unit tests

Application
    → Unit tests
    → Integration tests

Infrastructure
    → Integration tests

UI
    → UI tests (future)