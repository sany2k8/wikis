## Step-by-Step Guide to Create and Use Poetry Package Manager

### 1. Install Poetry

The recommended way to install Poetry is by running the official installation script:

```bash
curl -sSL https://install.python-poetry.org | python3 -
```

- This installs Poetry to your user directory (e.g., `~/.local/bin` on Unix systems).
- After installation, add Poetry to your PATH if it's not already:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

- Verify installation:

```bash
poetry --version
```

Alternatively, you can install Poetry using `pipx` for isolated environment management:

```bash
pipx install poetry
```


---

### 2. Initialize a New Poetry Project

Navigate to your project directory or create a new one:

```bash
mkdir my-project
cd my-project
```

Initialize a new Poetry project interactively:

```bash
poetry init
```

- You will be prompted to enter project details such as name, version, description, author, license, and dependencies.
- You can accept defaults or specify your own.
- This generates a `pyproject.toml` file which manages your project metadata and dependencies.

---

### 3. Add Dependencies

To add packages as dependencies, use:

```bash
poetry add <package-name>
```

For example:

```bash
poetry add pandas requests
```

This updates `pyproject.toml` and installs the packages in an isolated virtual environment managed by Poetry.

---

### 4. Install Dependencies

To install all dependencies listed in `pyproject.toml` (including those added manually or from version control):

```bash
poetry install
```

This will create and manage a virtual environment automatically.

---

### 5. Use the Virtual Environment

To run commands inside the Poetry-managed virtual environment, use:

```bash
poetry shell
```

This activates the environment in your shell.

Alternatively, run a command directly inside the environment without activating it:

```bash
poetry run python script.py
```


---

### 6. Manage Project Scripts and Build

- Define scripts in `pyproject.toml` under `[tool.poetry.scripts]` to create CLI commands.
- To build your package for distribution:

```bash
poetry build
```

- To publish your package to PyPI:

```bash
poetry publish
```

You will need PyPI credentials configured or use an API token.

---

### 7. Additional Useful Commands

| Command         | Purpose                                            |
| :-------------- | :------------------------------------------------- |
| `poetry update` | Update all dependencies to latest allowed versions |
| `poetry lock`   | Generate or update `poetry.lock` file              |
| `poetry show`   | List installed packages and versions               |
| `poetry config` | Configure Poetry settings                          |


---

### Summary

| Step                 | Command/Action                               |
| :------------------- | :------------------------------------------- |
| Install Poetry       | `curl -sSL https://install.python-poetry.org | python3 -` or `pipx install poetry` |
| Initialize Project   | `poetry init`                                |
| Add Dependencies     | `poetry add <package>`                       |
| Install Dependencies | `poetry install`                             |
| Activate Environment | `poetry shell`                               |
| Run Commands in Env  | `poetry run <command>`                       |
| Build Package        | `poetry build`                               |
| Publish Package      | `poetry publish`                             |


---

This guide helps you set up Poetry as a modern Python dependency and packaging manager, simplifying project setup, dependency resolution, and publishing. For detailed documentation, visit [python-poetry.org](https://python-poetry.org/docs/)[^1][^2][^3][^4].

<div style="text-align: center">⁂</div>

[^1]: https://python-poetry.org/docs/

[^2]: https://python-poetry.org/docs/basic-usage/

[^3]: https://www.digitalocean.com/community/tutorials/how-to-install-poetry-to-manage-python-dependencies-on-ubuntu-22-04

[^4]: https://realpython.com/dependency-management-python-poetry/

[^5]: https://www.youtube.com/watch?v=U_cPHzfdqPU

[^6]: https://betterstack.com/community/guides/scaling-python/poetry-explained/

[^7]: https://flexiple.com/python/poetry-python

[^8]: https://www.youtube.com/watch?v=bTaqePEky6Q

[^9]: https://www.jetbrains.com/help/dataspell/poetry.html

