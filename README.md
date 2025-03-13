# Code Clarity Documentation Conventions

Welcome to the Code Clarity documentation conventions repository. This guide outlines best practices for writing clear and purposeful documentation across various programming languages and tools.

## Core Principles

- **Brevity ≠ Vagueness**: Provide enough information without overwhelming details.
- **Structure**: Use scoped, purposeful, and consistent documentation similar to git commits.
- **Why > What**: Focus on documenting the intent behind code, not just the mechanics.

## Per-Language Rules

### Go
- Use `//` comments to describe the role and intent of functions and structs.

### Scripts/Automation
- Include a header block at the top of files to define scope, synopsis, risk, and safety.

### IaC (Infrastructure as Code)
- Document resource intent and security considerations.

### Frontend (Svelte, TypeScript)
- Use comments to explain component purpose and function intent.

### Taskfiles (go-task)
- Define task purpose and dependencies clearly.

## Syncing with Git Commits

Enhance Conventional Commits with documentation impact tags to flag changes needing doc updates.

## Why Bother?

- Faster onboarding with documentation explaining system quirks.
- Reduce "Why?" comments in PRs by self-documenting intent.
- Easily searchable documentation for triaging issues.

## Git Commits Style

Adopt Conventional Commits to ensure clear and informative commit messages.

## Full Documentation

For more detailed information, please refer to the [Code Clarity Documentation](CODE_CLARITY.md).

---

*"Documentation is a love letter you write to your future self."* – Some dev who avoided a 3am outage.
