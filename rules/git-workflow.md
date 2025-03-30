# Git Workflow Guide

## Overview

This document outlines Git workflow for the project.

## Branch Strategy

### Main Branch

- `main`: Production-ready code
  - Protected branch: Direct pushes are prohibited
  - Must require pull request review
  - Must pass CI/CD checks

### Development Branches

- Feature branches
  - Format: `<username>/feature/issue-<number>-<description>`
  - Example: `lyohe/feature/issue-234-add-error-logging`
- Bugfix branches
  - Format: `<username>/bugfix/issue-<number>-<description>`
- Hotfix branches
  - Format: `<username>/hotfix/issue-<number>-<description>`

## Development Flow

1. Issue Creation

   - Create a new issue for each task
   - Add labels
   - Assign to team member

2. Branch Creation

   ```bash
   git checkout main
   git pull origin main
   git switch -c lyohe/feature/issue-<number>-<description>
   ```

3. Development

   - Follow coding standards
   - Maintain 75% or higher test coverage
   - Commit messages in plain English

4. Pull Request

   - Create PR using template
   - Link related issues
   - Request review from team members
   - Address review comments

5. Review Process

   - Code review by at least one team member
   - Check coding standards compliance
   - Verify test coverage
   - Ensure documentation is updated

6. Merge

   - Squash and merge to main
   - Delete feature branch after merge

## Commit Messages

### Format

```
<type>: <description>

Reason or background for the change (why this change is necessary)

- Specific change 1
- Specific change 2 (optional)
- Specific change 3 (optional)

Issue #<number>
```

#### Types

- `feat`: add a new feature
- `fix`: fix a bug or issue (bugfix or hotfix)
- `docs`: update documentation only
- `style`: make formatting or stylistic changes (no code behavior affected)
- `refactor`: restructure code without changing behavior
- `test`: add or modify tests only
- `chore`: update build processes or development tools

### Examples

```
feat: add CSV export functionality

Users requested an option to export reports for offline analysis.

- Implemented export button on the reports page
- Added backend CSV generation endpoint
- Included unit tests for export service

Issue #58
```

```
chore: update Node.js version to 20.x

To ensure compatibility with updated dependencies.

- Updated Node.js version in Dockerfile and CI workflow
- Updated development guidelines in README.md

Issue #75
```

## Branch Protection Rules

### Main Branch Protection

- Require pull request reviews before merging
- Require status checks to pass before merging
- Include administrators in restrictions
- Require linear history
- Require signed commits

### Pull Request Requirements

- At least one approving review
- All discussions resolved
- All status checks passing
- Up-to-date with main branch
- Must not rebase after code reviewed

#### Rebase Guideline

- Regularly rebase while your branch is in active development, before requesting reviews
- Once reviews have started, avoid rebasing or rewriting commit history
- Use squash and merge to combine commits neatly when merging the PR

## CI/CD Integration

### Continuous Integration

- Run on pull requests
- Lint checks
- Run unit tests
- Generate test coverage report
- Build verification

### Continuous Deployment

- Automated deployment to staging
- Manual approval for production
- Deployment status checks

## Best Practices

1. Keep branches short-lived
2. Regular rebasing with main
3. Squash commits before merge
4. Write descriptive commit messages
5. Link issues and pull requests
6. Regular cleanup of merged branches

## Tools and Commands

### Branch Management

```bash
# Update main
git checkout main
git pull origin main

# Create feature branch
git checkout -b <username>/feature/issue-<number>-<description>

# Update feature branch
git fetch origin
git rebase origin/main

# Push changes
git push origin <username>/feature/issue-<number>-<description>
```

### Branch Cleanup

```bash
# Delete local branch
git branch -d <branch-name>

# Delete remote branch
git push origin --delete <branch-name>
```

### GitHub CLI

```bash
# Create pull request
gh pr create --title "<title>" --body "<description>"

# Check pull request status
gh pr status

# Review pull request
gh pr review [<number>] --approve
```
