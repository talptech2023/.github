# Contributing Guidelines

This document defines our internal workflow. As an agile team, our goal is to maintain the perfect balance between development speed and production stability.

To achieve this, we use a Simplified GitFlow model and connect our code directly to our GitHub Issues.


## 1. Branch Structure

We have two main branches, and both are protected:

* **`main` (Production):** This branch is sacred. It only contains stable, production-ready code. Each merge into this branch represents a new official release (e.g., v1.0.0, v1.1.0). We never push directly here.
* **`develop` (Integration/Staging):** This is our primary collaborative working branch. We integrate all new features and fixes here before releasing them to production. Direct pushes are not allowed; everything must go through a Pull Request (PR).
 
## 2. Branch Naming Convention

All new branches must be created from `develop` (except for hotfixes). To maintain traceability, we always use lowercase, hyphens, and the corresponding Issue number.

**Mandatory format:** `type/issue_number-description`

* **`feature/...`**: For new functionalities. (e.g., `feature/12-stripe-integration`)
* **`bugfix/...`**: For fixing bugs found during development. (e.g., `bugfix/45-broken-login-button`)
* **`hotfix/...`**: **Exception:** Created directly from `main` to fix a critical error currently live in production. (e.g., `hotfix/99-server-crash`)

## 3. Issue Management

Before writing code, make sure an Issue exists. We classify them as follows:

* **Type:** The issue must clearly state if it is a Bug, a Feature, or a Task.
* **Labels:** We use labels to provide additional context such as the type again (bug, feature, hotfix),  priority (priority: high, priority: low) or affected component (frontend, backend, database).


## 4. Step-by-Step Workflow

1. **Update your local environment:**
   ```bash
   git checkout develop
   git pull origin develop
   ```
2. **Create your branch:**
    ```bash
    git checkout -b feature/12-my-new-task
    ```
3. **Code and commit:** Write clear and descriptive commit messages.
4. **Push your branch:**
    ```bash
    git push -u origin feature/12-my-new-task
    ```

5. **Open a Pull Request:** Go to GitHub and open a PR pointing to develop.
> Tip: In your PR description, you must write `Closes #12` (changing the number to match your issue). This tells GitHub to close the ticket automatically when we approve and merge the code.

## 5. Pull Request Rules (Code Review)

For a PR to be merged into develop, it must meet the following criteria:

- Approval: Requires at least 1 review and approval from another team member.
- Status Checks: If we have SonarCloud or automated tests, they must pass (green).
- Clean up: Once your PR is merged, delete your branch on GitHub to keep the repository clean.

## 6. Production Releases
When we determine that develop is stable and has the necessary features for a new version:
1. Open a PR from develop to main.
2. The team reviews and approves it.
3. Create a new Release associated with that merge and tag it with the corresponding version using GitHub Actions. See https://github.com/semantic-release/semantic-release
