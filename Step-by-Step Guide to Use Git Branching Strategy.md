## Step-by-Step Guide to Use Git Branching Strategy: GitFlow

GitFlow is a popular branching model designed to manage feature development, releases, and hotfixes in a structured way. It uses multiple long-lived branches and supporting branches to organize work.

---

### 1. Initialize GitFlow in Your Repository

If you have an existing Git repository, initialize GitFlow using the extension:

```bash
git flow init
```

- You will be prompted to confirm branch names.
- Default branches:
    - Production releases branch: `main` (or `master`)
    - Development branch: `develop`
- Default prefixes:
    - Feature branches: `feature/`
    - Release branches: `release/`
    - Hotfix branches: `hotfix/`
    - Support branches: `support/`

If you don’t have the GitFlow extension, you can create the `develop` branch manually:

```bash
git branch develop
git push -u origin develop
```


---

### 2. Understand the Main Branches

- **`main` (or `master`)**: Stores official release history. Only stable, production-ready code is here.
- **`develop`**: Integration branch where features are merged. Represents the latest delivered development changes.

---

### 3. Create and Work on Feature Branches

Feature branches are for developing new features without affecting `develop` or `main`.

- Start a feature branch from `develop`:

```bash
git flow feature start <feature-name>
```

- Work on your feature, commit changes as usual.
- Push the feature branch if collaborating:

```bash
git push origin feature/<feature-name>
```

- When finished, merge the feature back into `develop`:

```bash
git flow feature finish <feature-name>
```

- Alternatively, create a Pull Request from `feature/<feature-name>` into `develop` for code review before merging.

---

### 4. Create and Finish Release Branches

Release branches prepare a new production release without blocking ongoing development.

- Start a release branch from `develop`:

```bash
git flow release start <version-number>
```

- Use this branch to finalize version numbers, fix bugs, update docs, and changelogs.
- When ready, finish the release:

```bash
git flow release finish <version-number>
```

This merges the release branch into both `main` and `develop`, tags the release on `main`, and deletes the release branch.

- Push changes and tags:

```bash
git push origin main develop --tags
```


---

### 5. Create and Finish Hotfix Branches

Hotfix branches are for urgent fixes on production (`main` branch).

- Start a hotfix branch from `main`:

```bash
git flow hotfix start <version-number>
```

- Apply fixes and commit.
- Finish the hotfix:

```bash
git flow hotfix finish <version-number>
```

This merges the fix into both `main` and `develop`, tags the fix on `main`, and deletes the hotfix branch.

- Push changes and tags:

```bash
git push origin main develop --tags
```


---

### 6. Best Practices for GitFlow

- **Consistent branch naming**: Use default prefixes (`feature/`, `release/`, `hotfix/`).
- **Small, frequent changes**: Keep feature branches short-lived and focused.
- **Regularly sync with `develop`**: Rebase or merge `develop` into your feature branch often to avoid conflicts.
- **Use Pull Requests** for code review before merging features or releases.
- **Tag releases** on the `main` branch for clear version history.

---

### Summary Table

| Branch Type | Purpose | Base Branch | Merge Into | Commands Example |
| :-- | :-- | :-- | :-- | :-- |
| `feature/*` | Develop new features | `develop` | `develop` | `git flow feature start <name>` |
| `release/*` | Prepare release (versioning, fixes) | `develop` | `main` \& `develop` | `git flow release start <version>` |
| `hotfix/*` | Urgent production fixes | `main` | `main` \& `develop` | `git flow hotfix start <version>` |
| `develop` | Integration branch for features | N/A | N/A | Created manually or by `git flow init` |
| `main` | Production-ready code | N/A | N/A | Stable releases only |


---

GitFlow provides a clear, structured workflow ideal for projects with scheduled releases and multiple developers, helping isolate development, releases, and urgent fixes effectively.

---

**References:**

- Atlassian GitFlow Tutorial [^1]
- DataCamp GitFlow Tutorial [^2]
- Original GitFlow Model by Vincent Driessen [^4]

*⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂ References ⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂*

[^1]: https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow

[^2]: https://www.datacamp.com/tutorial/gitflow

[^3]: https://www.youtube.com/watch?v=gQVUCTVt39o

[^4]: https://nvie.com/posts/a-successful-git-branching-model/

[^5]: https://dev.to/karmpatel/git-branching-strategies-a-comprehensive-guide-24kh

[^6]: https://docs.aws.amazon.com/prescriptive-guidance/latest/choosing-git-branch-approach/gitflow-branching-strategy.html

[^7]: https://www.gitkraken.com/learn/git/git-flow

[^8]: https://www.youtube.com/watch?v=Aa8RpP0sf-Y

