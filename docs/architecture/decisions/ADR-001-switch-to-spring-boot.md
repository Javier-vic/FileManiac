# ADR-001: Use Spring Boot as the Application Framework

## Status
Accepted

## Date
2026-08-18

## Context
The project was initially planned and partially structured using
.NET as the application framework.

During the initial project planning, the framework choice was
reconsidered in order to align the project more closely with the
developer's current learning objectives and target technology
stack.

Spring Boot was evaluated as an alternative to .NET for the
implementation of FileManiac.

## Decision Drivers
- Improve practical experience with Spring Boot.
- Build a portfolio project using Java and Spring Boot.
- Evaluate Spring Boot through a real-world application rather than isolated exercises.
- Maintain a modular and maintainable architecture.
- Preserve the project's privacy-focused local processing model.

## Considered Options

### .NET
**Advantages**
- Existing experience with C# and .NET.
- Familiar development environment.
- Strong ecosystem for desktop applications.

**Disadvantages**
- Provides less opportunity to develop practical experience with Spring Boot and the Java ecosystem.

### Spring Boot
**Advantages**
- Provides practical experience with Spring Boot.
- Strong ecosystem for enterprise application development.
- Allows the project to be used as a practical portfolio project for Java/Spring positions.

**Disadvantages**
- Requires adapting the project to a different ecosystem.
- Some parts of the initial project structure must be redesigned.

## Decision
Spring Boot will be used as the primary application framework for
FileManiac.

The existing .NET project structure will be adapted rather than
considered a direct implementation of the final architecture.

## Consequences

### Positive
- The project provides practical experience with Spring Boot.
- The project can demonstrate knowledge of Java and Spring concepts.
- The architecture can be evaluated using a different technology stack.

### Negative
- Previous .NET setup work will no longer be used directly.
- Some project documentation and structure will need to be updated.
- Additional time will be required to become familiar with the Spring ecosystem.
