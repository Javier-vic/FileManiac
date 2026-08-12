# FileManiac

A privacy-focused desktop application for managing PDF documents locally, without uploading files to external services.

## Overview

FileManiac is a desktop application designed to provide common PDF management and conversion tools while keeping user documents on the local computer.

Many online PDF tools require users to upload their documents to third-party servers. This can be unsuitable when working with confidential, sensitive, or private information.

This project aims to provide a local alternative where PDF processing is performed directly on the user's computer.

## Goals

* Process documents locally.
* Avoid uploading user files to external services.
* Provide common PDF management operations through a simple desktop interface.
* Work without requiring an Internet connection for core functionality.
* Provide a free and privacy-focused alternative to online PDF tools.
* Maintain a modular and testable codebase.

## Features

### PDF Management

* [ ] Merge multiple PDF files
* [ ] Split PDF documents
* [ ] Reorder pages
* [ ] Remove pages
* [ ] Rotate pages
* [ ] Extract pages
* [ ] View PDF metadata
* [ ] Remove PDF metadata

### File Conversion

* [ ] Convert supported file formats to PDF
* [ ] Convert images to PDF

### User Experience

* [ ] Drag and drop files
* [ ] PDF preview
* [ ] Operation progress
* [ ] Operation cancellation
* [ ] Clear error messages
* [ ] Prevent accidental file overwrites

### Privacy

* [ ] Local document processing
* [ ] No document uploads
* [ ] No user account required
* [ ] No collection of document contents
* [ ] Offline support for core functionality

> Features marked with `[ ]` are planned or under development.

## Privacy

Privacy is one of the main design principles of this project.

FileManiac is designed to process documents locally. The application does not require users to upload their files to a remote service in order to perform its core operations.

The project does not intentionally collect or transmit the contents of user documents.

## Project Status

🚧 **In development**

The project is currently under active development. Features, architecture, and documentation may change before the first stable release.

## Architecture

The project follows a layered architecture designed to separate the user interface, application logic, domain logic, and infrastructure concerns.

```text
┌─────────────────────────────┐
│       Presentation          │
│        WPF / Avalonia       │
└──────────────┬──────────────┘
               │
┌──────────────▼──────────────┐
│        Application          │
│      Use Cases / Logic      │
└──────────────┬─────────────▲┘
               │             |
┌──────────────▼───────────┐ |
│        Domain            │ |
│  Business Rules / Models │ |
└──────────────▲───────────┘ |
               │             |
┌─────────────────────────────┐
│        Infrastructure       │
│ PDF / File System / Logging │
└─────────────────────────────┘
```

More detailed architectural information can be found in [`docs/architecture`](docs/architecture/).

## License

This project is licensed under the **MIT License**.

See [`LICENSE`](LICENSE) for the complete license text.

## Disclaimer

FileManiac is an open-source personal software project intended to provide local PDF management functionality.

Users are responsible for verifying that the application meets the security, privacy, and compliance requirements applicable to their specific environment.
