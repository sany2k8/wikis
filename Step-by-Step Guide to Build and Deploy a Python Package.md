## Step-by-Step Guide to Build and Deploy a Python Package to PyPI Using UV

### 1. Install UV

Choose one of these installation methods:

```bash
# Standalone installer (macOS/Linux)
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows
irm https://astral.sh/uv/install.ps1 | iex

# Via pip
pip install uv

# Homebrew
brew install uv
```


### 2. Initialize Project Structure

```bash
uv init <PACKAGE_NAME>  # Creates basic package structure 
cd <PACKAGE_NAME>
```


### 3. Configure Project Metadata

Edit `pyproject.toml` to include:

```toml
[build-system]
requires = ["uv"]
build-backend = "uv"

[project]
name = "<PACKAGE_NAME>"
version = "0.1.0"
description = "Your package description"
classifiers = ["Private :: Do Not Upload"]  # For private packages 
```


### 4. Build Package Distributions

```bash
uv build  # Creates .whl and .tar.gz in dist/ 
```

Optional flags:

- `--no-sources`: Ensure compatibility with other build tools 
- `--package <SPECIFIC_PACKAGE>`: Build specific workspace package 


### 5. Create PyPI API Token

1. Log in to [pypi.org](https://pypi.org)
2. Navigate to Account Settings → API tokens
3. Create token with "Entire account" scope (for first publish) 

### 6. Publish to TestPyPI (Recommended)

```bash
uv publish --token pypi-xxxx-xxxx-xxxx \
  --publish-url https://test.pypi.org/legacy/ 
```


### 7. Verify Test Installation

```bash
uv pip install --index-url https://test.pypi.org/simple/ <PACKAGE_NAME>
uvx --from <PACKAGE_NAME> your-cli-command  # Test CLI tools 
```


### 8. Publish to PyPI

```bash
uv publish --token pypi-xxxx-xxxx-xxxx  # Uses default PyPI endpoint 
```


### 9. Final Verification

1. Check package page on [pypi.org](https://pypi.org)
2. Install globally:
```bash
uv pip install <PACKAGE_NAME>
```


### Additional Tips

**Version Management:**

```bash
uv version <NEW_VERSION>  # Bump version automatically 
```

**CI/CD Pipeline:**

```yaml
# Example GitHub Action
- name: Publish
  run: uv publish --token ${{ secrets.PYPI_TOKEN }}
```

**Security Best Practices:**

- Replace initial account-wide token with project-scoped token after first publish 
- Use `UV_PUBLISH_TOKEN` environment variable instead of CLI argument for production 

---

This workflow leverages UV's fast Rust-based tooling for efficient Python package distribution. The process ensures compatibility with PyPI's modern token authentication system while maintaining flexibility for testing via TestPyPI.

---

### References

- https://docs.astral.sh/uv/guides/package   
- https://pypi.org/project/uv/
- https://pydevtools.com/handbook/tutorial/publishing-your-first-python-package-to-pypi/  
- https://mathspp.com/blog/til/publishing-a-python-package-with-uv  
- https://www.youtube.com/watch?v=WKc2BdgmGZE  
- https://thisdavej.com/packaging-python-command-line-apps-the-modern-way-with-uv/  
- https://sarahglasmacher.com/how-to-build-python-package-uv/  
- https://packaging.python.org/tutorials/packaging-projects/  
- https://dev.to/lovestaco/how-to-create-and-publish-a-python-package-on-pypi-4470  
- https://pypi.org/project/uv/0.1.32/

