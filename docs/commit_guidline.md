# Git Commit Message Guidelines

## 1. Purpose

This document defines the commit message conventions for the `online-retail-analytics-api` project.

Consistent commit messages make the Git history easier to read, improve collaboration, simplify code reviews, and help identify changes quickly.

This project follows the **Conventional Commits** format.

## 2. Commit Message Format

Every commit message should follow this structure:

```text
<type>(<scope>): <description>
```

- **type**: The category of change.
- **scope**: The part of the project affected (optional).
- **description**: A short summary of the change.

Example:

```text
feat(analytics): add customer sales summary
```

The scope may be omitted when the change affects the project generally.

Example:

```text
chore: initialize project structure
```

## 3. Commit Types

Use the following commit types consistently.

| Type | Description | Example |
|---|---|---|
| `feat` | Introduce a new feature | `feat(analytics): add sales analysis` |
| `fix` | Fix a bug or incorrect behavior | `fix(api): handle missing customer IDs` |
| `docs` | Add or update documentation | `docs: update project README` |
| `test` | Add or update tests | `test(analytics): add sales calculation tests` |
| `refactor` | Restructure code without changing its intended behavior | `refactor(ml): simplify preprocessing pipeline` |
| `perf` | Improve performance | `perf(analytics): optimize revenue aggregation` |
| `chore` | General maintenance or project configuration | `chore: add gitignore file` |
| `build` | Change dependencies or build configuration | `build: update project dependencies` |
| `ci` | Update continuous integration or delivery workflows | `ci: add GitHub Actions test workflow` |
| `style` | Apply formatting changes without changing behavior | `style: format Python source files` |
| `revert` | Revert a previous commit | `revert: undo customer segmentation change` |

## 4. Writing Good Commit Messages

Follow these rules when writing commit messages:

1. Use lowercase for the type, scope, and description where appropriate.
2. Keep the subject line concise, preferably under 72 characters.
3. Use the imperative mood: describe what the commit does.
4. Do not end the subject line with a period.
5. Describe the actual change, not just the files modified.
6. Make each commit focused on one logical change.
7. Avoid vague descriptions such as `update`, `changes`, `fix stuff`, or `misc`.
8. Do not commit unrelated changes together.
9. Never include passwords, API keys, access tokens, or other secrets in a commit.
10. Do not claim that functionality is implemented or tested unless it actually is.

### Good examples

```text
docs: add project setup instructions
feat(customers): add customer summary endpoint
fix(analytics): handle negative quantities correctly
test(ml): add clustering evaluation tests
refactor(api): separate route dependencies
chore: configure Ruff linting
ci: add automated test workflow
```

### Bad examples

```text
update files
fixed stuff
new code
changes
final version
working now
```

These messages do not clearly explain the purpose of the commit.

## 5. Using Scopes

Scopes identify the project area affected by a change. They are optional, but recommended when they make the message more informative.

Suggested scopes for this project include:

| Scope | Project area |
|---|---|
| `api` | FastAPI application and endpoints |
| `analytics` | Sales, customer, and product analytics |
| `customers` | Customer-related functionality |
| `products` | Product-related functionality |
| `ml` | Machine learning models and pipelines |
| `data` | Data loading, validation, and processing |
| `tests` | Testing infrastructure and test organization |
| `docs` | Project documentation |
| `config` | Project and tool configuration |
| `ci` | Continuous integration and delivery |
| `deployment` | Docker and AWS deployment configuration |

Examples:

```text
feat(api): add product analytics endpoint
feat(ml): implement customer clustering
fix(data): handle missing descriptions
docs(api): document analytics endpoints
chore(config): configure pytest
```

Use a scope only when it adds useful context. Do not invent a scope just to fill the format.

## 6. Initial Commit

The first commit establishes the project's initial structure and baseline files.

For this project, if the initial commit contains the README and `.gitignore`, use:

```text
chore: initialize project with README and gitignore
```

Other suitable examples include:

```text
docs: add initial project README
chore: add gitignore for project setup
chore: establish initial project structure
```

Choose the message that accurately describes the files included in the commit.

## 7. Commit Messages With a Body

For larger changes, add a body when more explanation is necessary.

Format:

```text
<type>(<scope>): <short description>

<additional explanation of the change>

<optional reference to an issue or task>
```

Example:

```text
feat(analytics): add customer revenue analysis

Calculate customer-level revenue and order statistics.
Handle cancelled invoices and invalid transaction quantities.

Refs: TASK-12
```

Keep the subject concise. Use the body to explain the motivation, important implementation decisions, or relevant limitations.

## 8. Breaking Changes

If a change introduces an incompatible API or behavior change, indicate it with `!` after the type or scope.

Example:

```text
feat(api)!: change customer endpoint response format
```

Explain the breaking change in the body:

```text
feat(api)!: change customer endpoint response format

Replace the previous response structure with the standardized
customer analytics schema.

BREAKING CHANGE: Clients must update their response parsing
to use the new schema.
```

Use breaking-change notation only when existing consumers may need to modify their code.

## 9. Recommended Workflow

Follow this workflow for each logical change:

1. Make a small, focused set of changes.
2. Review the changed files.
3. Run relevant tests and quality checks when applicable.
4. Check that secrets, local data, model artifacts, and unnecessary files are not included.
5. Stage only the files relevant to the change.
6. Write a clear commit message using the agreed format.
7. Review the commit before pushing it to the remote repository.

Example Git workflow:

```bash
git status
git diff
git add README.md .gitignore
git diff --cached
git commit -m "chore: initialize project with README and gitignore"
```

Replace the staged filenames and commit message according to the changes being committed.

## 10. Commit Frequency

Prefer small, meaningful commits over large commits that contain unrelated changes.

Examples of reasonable commit boundaries:

- Initialize the project configuration.
- Add data loading and validation.
- Implement sales analytics.
- Add customer analytics tests.
- Introduce customer segmentation.
- Add API endpoints.
- Configure automated testing.
- Prepare Docker deployment.

Do not create a commit for every individual line of code. Commit when a coherent unit of work is complete and can be described clearly.

## 11. Final Checklist

Before creating a commit, confirm the following:

- [ ] The changes represent one logical unit of work.
- [ ] The commit type accurately describes the change.
- [ ] The scope is useful and appropriate, if included.
- [ ] The description is clear, concise, and imperative.
- [ ] The message has no unnecessary trailing punctuation.
- [ ] Relevant tests and checks have been run when applicable.
- [ ] No secrets or unintended files are staged.
- [ ] The commit message accurately represents what changed.

## 12. Summary

Use this format for all project commits:

```text
<type>(<scope>): <short description>
```

Prioritize clarity, consistency, and accuracy. A good commit message should help another developer understand the