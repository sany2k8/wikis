## Step-by-Step Guide to Set Up and Use Git

### 1. Install Git

- **Windows:**
    - Download the latest version of Git for Windows installer.
    - Run the installer and follow the prompts. The default settings are suitable for most users.
    - During installation, you can choose a text editor (e.g., Vim or Nano).
    - After installation, launch Git Bash to start using Git.
- **macOS:**
    - The easiest way is to install the Xcode Command Line Tools.
    - Alternatively, use Homebrew:

```bash
brew install git
```

- **Linux:**
    - Use your distribution's package manager:
        - Debian/Ubuntu: `sudo apt-get install git`
        - Fedora: `sudo dnf install git`

**Verify Installation:**

- Open a terminal or Git Bash and run:

```bash
git --version
```

- This command should display the installed Git version.


### 2. Configure Git

- Set your username and email using the following commands:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

Replace `"Your Name"` and `"your.email@example.com"` with your actual name and email address.


### 3. Create a Local Repository

- Navigate to your project directory in the terminal using the `cd` command.
- Initialize a Git repository:

```bash
git init
```

This command creates a `.git` subdirectory in your project directory, which contains the repository metadata.


### 4. Basic Git Workflow

1. **Stage Changes:**
    - Add the files you want to commit using the `git add` command:

```bash
git add <file1> <file2> ...
git add .       # To add all changes in the directory
```

2. **Commit Changes:**
    - Commit the staged changes with a descriptive message:

```bash
git commit -m "Your commit message"
```

The commit message should briefly explain the changes you've made.
3. **View Status:**
    - Check the status of your repository:

```bash
git status
```

This command shows you the modified files, staged files, and untracked files.
4. **View History:**
    - View the commit history:

```bash
git log
```

This command displays a list of commits with their authors, dates, and messages.

### 5. Connect to a Remote Repository (e.g., GitHub)

1. **Create a Repository on GitHub:**
    - Go to GitHub and create a new repository.
2. **Add the Remote Repository:**
    - Connect your local repository to the remote repository using the `git remote add` command:

```bash
git remote add origin <repository_url>
```

Replace `<repository_url>` with the URL of your GitHub repository.  `origin` is a common alias for the remote repository.
3. **Push Changes:**
    - Push your local commits to the remote repository:

```bash
git push -u origin main
```

This command pushes the commits from your local `main` branch to the remote `origin` repository. The `-u` flag sets up tracking, so subsequent pushes can be done with just `git push`.
4. **Pull Changes:**
    - To retrieve changes from the remote repository, use the `git pull` command:

```bash
git pull origin main
```

This command fetches the latest changes from the remote `origin` repository and merges them into your local `main` branch.

### 6. Branching and Merging

1. **Create a New Branch:**
    - Create a new branch using the `git branch` command:

```bash
git branch <branch_name>
```

2. **Switch to a Branch:**
    - Switch to the new branch using the `git checkout` command:

```bash
git checkout <branch_name>
```

You can combine these two commands using:

```bash
git checkout -b <branch_name>
```

3. **Merge Branches:**
    - To merge changes from one branch into another, switch to the target branch and use the `git merge` command:

```bash
git checkout main
git merge <branch_name>
```

This command merges the changes from `<branch_name>` into the `main` branch.
4. **Resolve Conflicts:**
    - If there are conflicts during the merge, Git will mark the conflicting areas in the files.
    - Manually edit the files to resolve the conflicts.
    - After resolving the conflicts, stage and commit the changes.

This guide provides a basic overview of how to set up and use Git for version control. There are many more advanced features and commands available in Git, but these steps should get you started.

### References

- https://phoenixnap.com/kb/how-to-install-git-windows

- https://git-scm.com/book/en/v2/Getting-Started-Installing-Git

- https://www.youtube.com/watch?v=qrD3z9_9DXU

- https://github.com/git-guides/install-git

- https://www.simplilearn.com/tutorials/git-tutorial/git-installation-on-windows

- https://codefinity.com/blog/A-step-by-step-guide-to-Git-installation

- https://www.youtube.com/watch?v=3FTficFKzME

- https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners

