# Development

## GitHub Workflows

Bloom uses GitHub Actions for automated workflows.

The workflow files are located in:

```text
.github/
|
\-- workflows/
    |
    |-- backend.yml
    |-- mobile.yml
    \-- frontend.yml
```

The workflows are separated by project area so that backend, mobile, and frontend changes can be handled independently.

## Issues

The repository includes templates for reporting bugs and requesting features.

```text
.github/
|
\-- ISSUE_TEMPLATE/
    |
    |-- bug_report.md
    \-- feature_request.md
```

These templates help keep issue reports consistent.

## Pull Requests

The repository has a pull request template:

```text
.github/
\-- pull_request_template.md
```

The template provides a consistent format when submitting changes for review.

## Code Ownership

The repository also contains a `CODEOWNERS` file:

```text
.github/
\-- CODEOWNERS
```

This file defines code ownership and can be used to identify the appropriate reviewers for changes.

## Development Workflow

A typical change follows this process:

```text
Make Changes
|
|-- Run Tests
|
|-- Create Pull Request
|
|-- Review
|
\-- Merge
```

The GitHub workflows help automate checks for the different parts of the project.