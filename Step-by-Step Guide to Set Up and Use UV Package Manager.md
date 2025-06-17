## Step-by-Step Guide to Set Up UV Package Manager

### 1. Install UV

UV can be installed on Linux, macOS, and Windows using several methods. The recommended approach is the official installation script:

**For macOS and Linux:**

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Or, if you don’t have `curl`:

```bash
wget -qO- https://astral.sh/uv/install.sh | sh
```

**For Windows (PowerShell):**

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

You can also specify a particular version by including it in the URL, e.g.:

```bash
curl -LsSf https://astral.sh/uv/0.7.12/install.sh | sh
```

or

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/0.7.12/install.ps1 | iex"
```

**Alternative methods:**

- Via Homebrew (macOS): `brew install uv`
- Via pip: `pip install uv` (not recommended, but possible)
- Via pipx: `pipx install uv` 

---

### 2. Verify Installation

After installation, check that UV is available:

```bash
uv --version
```

You should see the installed version printed in your terminal.
You can also run:

```bash
uv
```

to see the help menu and available commands.

---

### 3. First Steps with UV

**Initialize a new project (optional):**

```bash
uv init my-project
cd my-project
```

This creates a project directory with:

- `.gitignore`
- `.python-version`
- `README.md`
- `pyproject.toml`
- Example Python file (e.g., `hello.py`)


**Create a virtual environment:**

```bash
uv venv
```

- Activate the environment:
    - On macOS/Linux: `source .venv/bin/activate`
    - On Windows: `.\.venv\Scripts\activate.ps1`


---

### 4. Installing Packages

**Add a package:**

```bash
uv add <package-name>
```

Example:

```bash
uv add numpy pandas
```

This installs the packages and updates `pyproject.toml` and `uv.lock`.

**Install from requirements file:**

```bash
uv pip install -r requirements.txt
```

**Install current project in editable mode:**

```bash
uv pip install -e .
```


---

### 5. Managing Python Versions (Optional)

UV can also manage Python versions:

```bash
uv python install 3.10 3.11 3.12
uv venv --python 3.12.0
uv python pin 3.11
```


---

### 6. Get Help

For more information on commands and options:

```bash
uv --help
```

or visit the official documentation.

---

UV is now set up and ready to use as your fast, modern Python package and project manager!

### References

- https://docs.astral.sh/uv/getting-started/installation/

- https://www.saaspegasus.com/guides/uv-deep-dive/

- https://realpython.com/python-uv/

- https://ubuntushell.com/install-uv-python-package-manager/

- https://www.datacamp.com/tutorial/python-uv

- https://docs.astral.sh/uv/getting-started/first-steps/

- https://www.digitalocean.com/community/conceptual-articles/uv-python-package-manager

- https://www.youtube.com/watch?v=JtR7EyMcaWU

- https://www.youtube.com/watch?v=JeiCxJP7IK4

- https://www.youtube.com/watch?v=AMdG7IjgSPM

