## Step-by-Step Guide to Set Up and Use Pyenv

### 1. Install Pyenv

**On macOS (using Homebrew):**

```bash
brew install pyenv
```

**On Linux:**

- Clone the repository:

```bash
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

- Add Pyenv to your shell environment by adding these lines to your shell config file (`~/.bashrc`, `~/.zshrc`, etc.):

```bash
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
```

**On Windows:**

- Use [pyenv-win](https://github.com/pyenv-win/pyenv-win) or Windows Subsystem for Linux (WSL).

---

### 2. Restart Your Shell

Reload your shell configuration to apply changes:

```bash
exec "$SHELL"
```

or simply close and reopen your terminal.

---

### 3. Install Python Build Dependencies (Linux/macOS)

Before installing Python versions, ensure required build dependencies are installed. For example, on Ubuntu:

```bash
sudo apt-get update
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl git
```


---

### 4. List Available Python Versions

To see all Python versions you can install:

```bash
pyenv install --list
```

Use `grep` to filter, e.g., for Python 3.10:

```bash
pyenv install --list | grep " 3.10"
```


---

### 5. Install a Python Version

Install a specific Python version (e.g., 3.10.9):

```bash
pyenv install 3.10.9
```

You can add `-v` for verbose output:

```bash
pyenv install -v 3.10.9
```


---

### 6. Set the Global Python Version

Set the default Python version for your system:

```bash
pyenv global 3.10.9
```

Verify the version:

```bash
python --version
```

It should show the version you set.

---

### 7. Set Local Python Version (Per Project)

Inside a project directory, set a Python version specific to that directory:

```bash
pyenv local 3.10.9
```

This creates a `.python-version` file in the directory. Python commands run inside this directory will use the specified version.

---

### 8. Use Pyenv Shims

Pyenv works by inserting shims into your `PATH` that intercept Python commands and redirect them to the selected version.

Verify the shim path:

```bash
which python
```

It should point to something like `~/.pyenv/shims/python`.

---

### 9. Update Pyenv (Optional)

To update pyenv to the latest version:

```bash
cd $(pyenv root)
git pull
```


---

### Summary Table

| Step | Command / Action |
| :-- | :-- |
| Install pyenv | `brew install pyenv` or clone repo and configure PATH |
| Restart shell | `exec "$SHELL"` or reopen terminal |
| Install dependencies | OS-specific (e.g., `apt-get install ...`) |
| List Python versions | `pyenv install --list` |
| Install Python version | `pyenv install <version>` |
| Set global Python | `pyenv global <version>` |
| Set local Python | `pyenv local <version>` |
| Verify Python version | `python --version` |


---

This setup allows you to easily install and switch between multiple Python versions on your system using Pyenv.

<div style="text-align: center">⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂ Always Sany ⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂</div>

[^1]: https://github.com/pyenv/pyenv

[^2]: https://realpython.com/intro-to-pyenv/

[^3]: https://stackoverflow.com/questions/29687140/install-latest-python-version-with-pyenv

[^4]: https://mac.install.guide/python/install-pyenv

[^5]: https://realpython.com/videos/pyenv-install-python/

[^6]: https://treyhunner.com/2024/05/installing-a-custom-python-build-with-pyenv/

[^7]: https://ggkbase-help.berkeley.edu/how-to/install-pyenv/

