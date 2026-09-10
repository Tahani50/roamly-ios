# Contributing to Roamly iOS

Thank you for contributing to **Roamly iOS**.

This document defines the development workflow, branch naming rules, commit message convention, pull request process, and basic code-quality expectations for this repository.

The goal is to keep the project history clean and make collaboration across the Roamly repositories predictable.

---

## Repository

**Repository:** `roamly-ios`

**Main branch:** `main`

Do not develop features directly on `main`. Create a separate branch for every feature, fix, refactor, or maintenance task.

---

## Git Workflow

Use this workflow for normal development:

```bash
# 1. Switch to main
git switch main

# 2. Get the latest changes
git pull origin main

# 3. Create a new branch
git switch -c <branch-name>

# 4. Make your changes

# 5. Check changed files
git status

# 6. Stage the changes
git add .

# 7. Commit
git commit -m "<type>: <short description>"

# 8. Push the branch
git push -u origin <branch-name>
```

After pushing, open a Pull Request from your branch into `main`.

---

## Branch Naming Convention

Use lowercase names and separate words with hyphens.

| Type | Format | Example |
|---|---|---|
| Feature | `feature/<name>` | `feature/trip-details` |
| Bug fix | `fix/<name>` | `fix/login-validation` |
| Refactor | `refactor/<name>` | `refactor/trip-repository` |
| Chore | `chore/<name>` | `chore/update-dependencies` |
| Documentation | `docs/<name>` | `docs/update-readme` |
| Tests | `test/<name>` | `test/trip-service` |

### Good examples

```text
feature/create-trip
feature/authentication
fix/profile-image-loading
refactor/network-layer
chore/update-dependencies
docs/api-documentation
test/trip-repository
```

### Avoid

```text
new-branch
my-branch
test123
trip-stuff
changes
final-version
```

---

## Commit Message Convention

Roamly uses a simplified **Conventional Commits** style.

Format:

```text
<type>: <short description>
```

Allowed commit types:

| Type | Use for |
|---|---|
| `feat` | New feature |
| `fix` | Bug fix |
| `refactor` | Code restructuring without changing behavior |
| `chore` | Tooling, configuration, dependency, or maintenance work |
| `docs` | Documentation only |
| `test` | Adding or updating tests |
| `style` | Formatting or style-only changes |
| `perf` | Performance improvements |

### Examples

```text
feat: add trip creation flow
fix: handle empty destination response
refactor: simplify authentication repository
chore: update project dependencies
docs: add setup instructions
test: add trip repository tests
```

Keep commit messages:

- Short and clear.
- Written in the imperative style.
- Focused on one logical change.
- Lowercase after the colon unless a proper noun requires capitalization.

Avoid messages such as:

```text
update
changes
fix stuff
final
done
new code
```

---

## Keeping Your Branch Updated

Before opening or updating a Pull Request, bring the latest `main` changes into your branch.

Preferred approach:

```bash
git switch main
git pull origin main

git switch <your-branch>
git merge main
```

If conflicts occur:

1. Resolve each conflict carefully.
2. Verify that both your changes and the required `main` changes are preserved.
3. Stage the resolved files:

```bash
git add .
```

4. Complete the merge:

```bash
git commit
```

5. Push the branch:

```bash
git push
```

Do not blindly accept all changes from one side when resolving conflicts. Review the final code before committing.

---

## Pull Request Guidelines

Before creating a Pull Request:

- Make sure the project builds successfully.
- Run relevant tests.
- Remove debugging code, temporary comments, and unused files.
- Check that no secrets or credentials are committed.
- Update documentation when behavior or setup changes.
- Confirm the branch contains only changes related to the task.

### Pull Request title

Use the same style as commit messages:

```text
feat: add trip creation flow
fix: handle failed login response
refactor: improve network layer
```

### Pull Request description

Include:

```markdown
## What changed?
Briefly describe the implementation.

## Why?
Explain why the change was needed.

## How was it tested?
Describe the tests or manual checks performed.

## Screenshots
Add screenshots for UI changes when applicable.
```

---

## Code Review

A Pull Request should be reviewed before it is merged when working with other contributors.

Reviewers should check:

- Correctness.
- Readability.
- Architecture consistency.
- Error handling.
- Naming.
- Tests.
- Security concerns.
- Unnecessary duplication.
- UI consistency, when applicable.

Do not merge a Pull Request with unresolved review comments.

---

## Secrets and Sensitive Files

Never commit:

- API keys.
- Access tokens.
- Passwords.
- Private certificates.
- Production credentials.
- Local environment files containing secrets.

Store local secrets in ignored configuration files or environment variables.

Before committing, always check:

```bash
git status
git diff --staged
```


## iOS Development Guidelines

This repository contains the native **Roamly iOS** application.

Follow the existing Swift/SwiftUI architecture and naming conventions.

### Development requirements

Use the Xcode and Swift versions documented by the project.

Open the project using the appropriate `.xcodeproj` or `.xcworkspace` file.

If the project uses Swift Package Manager, allow Xcode to resolve package dependencies before building.

### Swift and SwiftUI conventions

- Prefer clear Swift naming that follows Apple's API design guidelines.
- Keep SwiftUI views focused on UI responsibilities.
- Keep business logic outside large view bodies.
- Reuse shared components rather than duplicating UI.
- Use dependency injection where the existing architecture expects it.
- Avoid force-unwrapping unless the value is guaranteed by design.
- Handle loading, empty, success, and failure states where applicable.
- Keep navigation consistent with the project's router/navigation approach.

### New feature structure

Follow the existing repository structure. A feature may contain layers such as:

```text
Feature/
├── Presentation/
├── Domain/
└── Data/
```

Do not introduce a different architecture for a single feature unless the project architecture is intentionally being changed.

### Testing

Before opening a Pull Request:

- Build the app successfully in Xcode.
- Run relevant unit tests.
- Run UI tests when the changed feature has them.
- Manually test the affected flow on a simulator or device.

For UI changes, test:

- Small and large supported screen sizes.
- Loading and error states.
- Navigation/back behavior.
- Dynamic content.
- Light/dark mode if supported by the app.

### iOS branch examples

```text
feature/trip-list
feature/create-trip
fix/profile-navigation
refactor/network-service
chore/update-ios-deployment-target
test/trip-view-model
```

### iOS commit examples

```text
feat: add trip list screen
feat: add create trip view model
fix: correct profile navigation
refactor: simplify network service
chore: update minimum iOS deployment target
test: add trip view model tests
```

---

## Documentation

Update `README.md` or other documentation when a change affects:

- Installation.
- Project setup.
- Environment configuration.
- Architecture.
- API usage.
- User-visible behavior.
- Developer workflow.

---

## Definition of Done

A task is considered complete when:

- The requested behavior is implemented.
- The project builds successfully.
- Relevant tests pass.
- No known regression was introduced.
- Code follows the repository conventions.
- Secrets and local configuration are not committed.
- Documentation is updated when needed.
- The branch is pushed.
- A Pull Request is ready for review.

---

## Questions

If a requirement or architecture decision is unclear, discuss it before introducing a large structural change.

Keep changes focused, readable, and easy to review.
