## Step-by-Step Guide to Set Up and Use GitHub Pages

### 1. Create a GitHub Account

If you don’t already have one, sign up at [github.com](https://github.com).

---

### 2. Create a New Repository for Your Website

- Click the **New repository** button on GitHub.
- Name the repository as `username.github.io` (replace `username` with your GitHub username). This is required for a user or organization site.
- Set the repository visibility to **Public** (GitHub Pages sites are public).
- Optionally, initialize the repository with a README file.
- Click **Create repository**.

---

### 3. Add Your Website Content

- Clone the repository locally:

```bash
git clone https://github.com/username/username.github.io.git
cd username.github.io
```

- Add your website files (`index.html`, CSS, JavaScript, images, etc.) to the repository folder.
- The root of the repository should contain your entry file, typically `index.html`.

---

### 4. Commit and Push Your Changes

```bash
git add .
git commit -m "Initial website content"
git push origin main
```


---

### 5. Enable GitHub Pages in Repository Settings

- On GitHub, navigate to your repository.
- Click the **Settings** tab.
- In the sidebar, click **Pages** (under "Code and automation").
- Under **Build and deployment > Source**, select **Deploy from a branch**.
- Choose the branch to publish from (usually `main`) and the folder (usually `/root` or `/docs`).
- Click **Save**.

---

### 6. Wait for Deployment and Access Your Site

- It may take a few minutes for GitHub to build and deploy your site.
- Your site will be available at:

```
https://username.github.io
```

- Visit this URL to see your live website.

---

### 7. Update Your Site

- Make changes to your website files locally.
- Commit and push the changes to the publishing branch (`main` or the branch you selected).
- GitHub Pages will automatically rebuild and redeploy your site.

---

### Optional: Use Project Sites Instead of User Sites

- For project-specific websites, create a repository with any name (not `username.github.io`).
- Add your site content and enable GitHub Pages from the repository settings as above.
- The site URL will be:

```
https://username.github.io/repository-name/
```


---

### Optional: Use a Custom Domain

- In the **Pages** settings, you can specify a custom domain you own.
- Configure your DNS provider to point your domain to GitHub Pages following GitHub’s instructions.

---

### Summary Table

| Step | Description |
| :-- | :-- |
| Create GitHub account | Sign up at github.com |
| Create repository | Name it `username.github.io` for user site |
| Add website files | Include `index.html` at root |
| Commit and push | Push changes to `main` branch |
| Enable GitHub Pages | Configure source branch and folder in Settings > Pages |
| Access your site | Visit `https://username.github.io` |
| Update site | Push changes to trigger automatic redeployment |


---

This guide helps you quickly launch a free static website hosted on GitHub Pages with automatic deployment on every push. It’s ideal for personal sites, portfolios, documentation, and project pages.

<div style="text-align: center">⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂ Always Sany ⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂</div>

[^1]: https://builtin.com/software-engineering-perspectives/github-pages

[^2]: https://docs.github.com/en/pages/quickstart

[^3]: https://docs.github.com/articles/creating-project-pages-manually

[^4]: https://www.youtube.com/watch?v=QyFcl_Fba-k

[^5]: https://www.youtube.com/watch?v=5XhxR9Vs6zc

[^6]: https://dzone.com/articles/launch-your-website-for-free-a-beginners-guide-to

[^7]: https://docs.github.com/en/pages/getting-started-with-github-pages

[^8]: https://www.linkedin.com/pulse/launch-your-website-free-beginners-guide-github-pages-omgmc

