## Step-by-Step Guide to Set Up and Use GitHub CLI with More Examples

### 1. Install GitHub CLI

- **macOS:**

```bash
brew install gh
```

- **Windows:**

```powershell
winget install --id GitHub.cli
```

- **Linux (Ubuntu/Debian):**

```bash
sudo apt update
sudo apt install gh
```

- Or download from [cli.github.com](https://cli.github.com/).

---

### 2. Verify Installation

```bash
gh --version
```


---

### 3. Authenticate GitHub CLI

```bash
gh auth login
```

- Follow prompts to authenticate via browser or token.

---

### 4. Common Usage Examples

#### Clone a Repository

```bash
gh repo clone owner/repo
```

Or using a URL:

```bash
gh repo clone https://github.com/cli/cli
```


---

#### Check Out a Pull Request Locally

By pull request number:

```bash
gh pr checkout 12
```

By branch name or URL:

```bash
gh pr checkout feature-branch
```


---

#### Create a New Repository

Interactively create a new repo:

```bash
gh repo create
```

Or create with flags:

```bash
gh repo create my-new-repo --public --source=. --remote=origin
```


---

#### Create a Pull Request

```bash
gh pr create --title "Add new feature" --body "Description of the feature" --base main --head feature-branch
```


---

#### List and View Issues

List open issues:

```bash
gh issue list
```

View a specific issue with comments:

```bash
gh issue view 123 --comments
```


---

#### View Pull Request Status and Checks

Check PR status:

```bash
gh pr status
```

View checks for a PR:

```bash
gh pr checks 12
```


---

#### Create a Release

Create a new release and upload assets:

```bash
gh release create v1.0.0 ./dist/*.zip --title "Version 1.0.0" --notes "Release notes here"
```


---

### 5. Advanced Usage

#### Set Aliases for Commands

```bash
gh alias set co 'pr checkout'
gh alias set iv 'issue view --comments'
```

Now you can run:

```bash
gh co 12
gh iv 123
```


---

#### Use GitHub CLI API for Custom Requests

Get team members via API:

```bash
gh api -X GET 'orgs/MYORG/teams/TEAM/members' -F per_page=100 --paginate
```


---

#### Use GitHub CLI in Scripts or CI/CD

Example GitHub Actions step to auto-merge PRs:

```yaml
- name: Auto-merge PR
  run: gh pr merge --auto --merge "$PR_URL"
  env:
    PR_URL: ${{ github.event.pull_request.html_url }}
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```


---

### 6. Configure GitHub CLI

Set default editor:

```bash
gh config set editor nano
```

Set default pager (e.g., use `less` or `delta` for diffs):

```bash
gh config set pager 'less'
```


---

### Summary Table

| Task | Command Example |
| :-- | :-- |
| Install GitHub CLI | `brew install gh` / `winget install GitHub.cli` |
| Authenticate | `gh auth login` |
| Clone repo | `gh repo clone owner/repo` |
| Checkout PR | `gh pr checkout 12` |
| Create repo | `gh repo create` |
| Create PR | `gh pr create --title "..." --body "..."` |
| List issues | `gh issue list` |
| View issue | `gh issue view 123 --comments` |
| Create release | `gh release create v1.0.0 ./dist/*.zip --notes "..."` |
| Set alias | `gh alias set co 'pr checkout'` |
| Use API | `gh api -X GET 'orgs/MYORG/teams/TEAM/members'` |


---

GitHub CLI empowers you to perform almost all GitHub operations from your terminal, streamlining workflows like cloning repos, managing pull requests, issues, releases, and automating tasks with scripts and CI/CD.

For more examples, see the official GitHub CLI examples page: https://cli.github.com/manual/examples[^1].

*⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂ References ⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂*

[^1]: https://cli.github.com/manual/examples

[^2]: https://github.com/cli/cli

[^3]: https://github.com/advanced-security/gh-add-files

[^4]: https://github.blog/engineering/engineering-principles/scripting-with-github-cli/

[^5]: https://docs.github.com/en/github-cli

[^6]: https://cli.github.com

[^7]: https://github.com/TechPrimers/github-cli-example

[^8]: https://www.youtube.com/watch?v=j5zUoyPaQqc

