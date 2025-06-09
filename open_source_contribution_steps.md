<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" class="logo" width="120"/>

## Step-by-Step Guide to Contribute to an Open Source Project on GitHub

### 1. Fork the Repository

- Find the repository you want to contribute to on GitHub.
- Click the **Fork** button at the top right of the repository page.
- This creates a copy of the repository under your GitHub account where you can freely make changes without affecting the original project[^1][^2][^3].


### 2. Clone Your Fork Locally

- Go to your forked repository on GitHub.
- Click the **Code** button and copy the repository URL.
- Open your terminal and run:

```
git clone <repository_url>
```

- Replace `<repository_url>` with the URL you copied.
- Navigate into the cloned directory:

```
cd <repository_name>
```


### 3. Set Up the Upstream Remote (Optional but Recommended)

- Add the original repository as a remote named `upstream` to keep your fork updated:

```
git remote add upstream https://github.com/original-owner/original-repo.git
git remote -v
```

- This helps you sync your fork with the original repository later[^4].


### 4. Create a New Branch

- Create and switch to a new branch for your feature or fix:

```
git checkout -b my-feature-branch
```

- Use a descriptive branch name related to your changes[^1][^2][^3][^4].


### 5. Make Your Changes

- Edit, add, or delete files as needed in your local repository.
- Follow the project's coding standards and guidelines.
- Test your changes locally to ensure they work correctly[^1][^3].


### 6. Stage and Commit Your Changes

- Stage the changed files:

```
git add .
```

- Commit your changes with a meaningful message:

```
git commit -m "Describe your changes here"
```


### 7. Push Your Branch to Your Fork

- Push the branch with your changes to your fork on GitHub:

```
git push origin my-feature-branch
```


### 8. Create a Pull Request (PR)

- Go to your forked repository on GitHub.
- Switch to your feature branch.
- Click **Compare \& pull request** or go to the **Pull Requests** tab and click **New pull request**.
- Select the original repository as the base and your branch as the compare branch.
- Provide a clear and detailed description of your changes.
- Submit the pull request[^1][^2][^4].


### 9. Respond to Feedback

- Project maintainers will review your PR and may request changes.
- Make any requested changes by committing to your branch and pushing again.
- Your PR will update automatically with your new commits[^4].


### 10. Keep Your Fork Updated (Optional)

- To sync your fork with the original repository:

```
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

- This keeps your fork’s main branch current[^4].

---

This workflow helps you contribute safely and efficiently to open source projects on GitHub, from forking to submitting your first pull request.

<div style="text-align: center">⁂</div>

[^1]: https://daily.dev/blog/how-to-contribute-to-open-source-github-repositories

[^2]: https://gun.io/news/2024/11/a-complete-guide-to-github-forks-from-setup-to-pull-requests/

[^3]: https://www.digitalocean.com/resources/articles/how-to-contribute-to-open-source

[^4]: https://github.com/susam/gitpr

[^5]: https://docs.github.com/en/get-started/exploring-projects-on-github/finding-ways-to-contribute-to-open-source-on-github

[^6]: https://github.com/firstcontributions/first-contributions

[^7]: https://docs.github.com/en/get-started/exploring-projects-on-github/contributing-to-a-project

[^8]: https://www.reddit.com/r/learnprogramming/comments/140gdp8/a_stepbystep_for_doing_your_first_open_source/

[^9]: https://learn.microsoft.com/en-us/training/modules/contribute-open-source/

[^10]: https://github.com/freeCodeCamp/how-to-contribute-to-open-source
