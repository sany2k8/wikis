## Step-by-Step Guide to Install and Use Pre-Commit Hooks

### 1. Install Pre-Commit

Install the `pre-commit` tool using pip (recommended):

```bash
pip install pre-commit
```

Verify the installation:

```bash
pre-commit --version
```

You should see the installed version printed[^1][^2].

---

### 2. Add a Pre-Commit Configuration

At the root of your project, create a file named `.pre-commit-config.yaml`.
You can generate a basic sample configuration with:

```bash
pre-commit sample-config > .pre-commit-config.yaml
```

Or create your own, for example:

```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
  - repo: https://github.com/psf/black
    rev: 24.4.2
    hooks:
      - id: black
```

This configuration adds some common Python formatting and linting hooks[^1][^2].

---

### 3. Install the Git Hook Scripts

Run the following command at your project root:

```bash
pre-commit install
```

This sets up the git hook scripts in your `.git/hooks` directory. From now on, the hooks will run automatically every time you make a commit[^1][^2][^4].

---

### 4. (Optional) Install Hook Environments Immediately

To pre-install all hook environments (instead of waiting for the first commit):

```bash
pre-commit install-hooks
```

Or combine with install:

```bash
pre-commit install --install-hooks
```

This can make the first commit faster[^1][^2].

---

### 5. Using Pre-Commit Hooks

- **On Every Commit:**
Hooks will automatically run when you execute `git commit`. If a hook fails, the commit will be blocked until you fix the issues[^1][^2][^4].
- **Manually Run All Hooks:**
To run all hooks on all files:

```bash
pre-commit run --all-files
```

- **Run a Specific Hook:**

```bash
pre-commit run <hook_id>
```


---

### 6. Updating Hooks

To update your hooks to their latest versions:

```bash
pre-commit autoupdate
```

This updates the hook versions in your `.pre-commit-config.yaml`[^1].

---

### 7. (Optional) Customize and Explore More Hooks

- You can add or remove hooks by editing `.pre-commit-config.yaml`.
- Explore more available hooks at [pre-commit.com](https://pre-commit.com)[^1][^2].

---

### Summary Table

| Step | Command/Action |
| :-- | :-- |
| Install pre-commit | `pip install pre-commit` |
| Add config | Create `.pre-commit-config.yaml` |
| Install hooks | `pre-commit install` |
| Run all hooks | `pre-commit run --all-files` |
| Update hooks | `pre-commit autoupdate` |


---

Pre-commit hooks help catch issues early and enforce code quality automatically before every commit[^2][^4].

<div style="text-align: center">⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂ Always Sany ⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂</div>

[^1]: https://pre-commit.com

[^2]: https://pre-commit.com/index.html

[^3]: https://lorenzwalthert.github.io/precommit/

[^4]: https://stefaniemolin.com/articles/devx/pre-commit/setup-guide/

[^5]: https://verdantfox.com/blog/how-to-use-git-pre-commit-hooks-the-hard-way-and-the-easy-way

[^6]: https://equinor.github.io/appsec/guidelines/FAQ/pre-commit-faq/

[^7]: https://github.com/pre-commit/pre-commit.github.io/issues/255

[^8]: https://dev.to/vaiolabs_io/amazing-pre-commit-and-how-to-use-it-5enb

[^9]: https://www.youtube.com/watch?v=fNtPWNsmuew

[^10]: https://www.linkedin.com/pulse/mastering-code-quality-step-by-step-guide-setting

[^11]: https://madewithml.com/courses/mlops/pre-commit/

[^12]: http://tezos.gitlab.io/developer/pre_commit_hook.html

[^13]: https://mokacoding.com/blog/pre-commit-hooks/

[^14]: https://git-scm.com/book/ms/v2/Customizing-Git-Git-Hooks

[^15]: https://fig.io/manual/pre-commit/run

