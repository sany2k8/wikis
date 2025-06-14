## Step-by-Step Guide to Set Up and Use GitHub Actions

### 1. Understand What GitHub Actions Are

GitHub Actions let you automate workflows in your GitHub repository. You define workflows in YAML files that run on specific events like pushes, pull requests, or on a schedule. Each workflow contains jobs made of steps that run scripts or reusable actions[^3][^4].

---

### 2. Create the Workflow Directory and File

- In your GitHub repository, create a directory named `.github/workflows`.
- Inside this directory, create a YAML file for your workflow, e.g., `ci.yml` or `github-actions-demo.yml`[^1][^6].

---

### 3. Define Your Workflow in the YAML File

Copy and paste the following example to get started quickly:

```yaml
name: GitHub Actions Demo
run-name: ${{ github.actor }} is testing out GitHub Actions 🚀
on: [push]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v4
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: ls ${{ github.workspace }}
      - run: echo "🍏 This job's status is ${{ job.status }}."
```

- `name:` sets the workflow name.
- `on:` defines the event that triggers the workflow (here, on every push).
- `jobs:` defines one or more jobs; each job runs on a GitHub-hosted runner.
- `steps:` are individual commands or actions run sequentially within a job[^1][^3][^4].

---

### 4. Commit and Push the Workflow File

- Commit the `.github/workflows/ci.yml` file to your repository’s default branch or a feature branch.
- This commit triggers the workflow automatically if the event condition matches (e.g., a push event)[^1].

---

### 5. Monitor Workflow Runs

- Go to the **Actions** tab in your GitHub repository.
- You will see your workflow runs listed with status indicators (queued, in progress, completed).
- Click a run to see detailed logs for each step.

---

### 6. Customize Your Workflow

- Modify the `on:` section to trigger on other events like `pull_request`, `schedule`, or manually via `workflow_dispatch`.
- Add jobs to build, test, or deploy your code.
- Use community or custom actions from the [GitHub Actions Marketplace](https://github.com/marketplace/actions) to extend functionality[^2][^4].

---

### 7. Example: Trigger Workflow on Push to Main Branch Only

```yaml
name: CI
on:
  push:
    branches: [ "main" ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: echo "Building on main branch"
```


---

### Summary

| Step                           | Description                              |
| :----------------------------- | :--------------------------------------- |
| Create `.github/workflows` dir | Store workflow YAML files                |
| Write workflow YAML            | Define triggers, jobs, and steps         |
| Commit workflow file           | Push to repo to trigger workflow         |
| Monitor runs                   | Use GitHub Actions tab to track progress |
| Customize workflows            | Add jobs, steps, and triggers as needed  |


---

This guide helps you get started with GitHub Actions by creating your first automated workflow triggered on code pushes, enabling automation of builds, tests, and deployments directly within your GitHub repository[^1][^2][^3][^4].

**⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂ References *⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂**

[^1]: https://docs.github.com/en/actions/writing-workflows/quickstart

[^2]: https://www.learnenough.com/blog/git-actions-tutorial

[^3]: https://docs.github.com/articles/getting-started-with-github-actions

[^4]: https://graphite.dev/guides/github-actions-beginner-guide

[^5]: https://spacelift.io/blog/github-actions-tutorial

[^6]: https://dev.to/sre_panchanan/hello-world-in-github-actions-a-beginners-guide-to-your-first-workflow-1mbh

[^7]: https://www.youtube.com/watch?v=zH8hz_21x_0

