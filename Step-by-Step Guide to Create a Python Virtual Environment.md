## Step-by-Step Guide to Create a Python Virtual Environment

### 1. Open a Terminal or Command Prompt

- On Windows: Open Command Prompt or PowerShell.
- On macOS/Linux: Open your terminal application[^2][^4].

---

### 2. Navigate to Your Project Directory (Optional)

- Use `cd` to change to the folder where you want your virtual environment.
- Example:

```bash
cd path/to/your/project
```

- It’s common to create the virtual environment inside your project folder[^2][^5].

---

### 3. Create the Virtual Environment

- **On Windows:**

```bash
python -m venv myenv
```

- **On macOS/Linux:**

```bash
python3 -m venv myenv
```

- Replace `myenv` with your preferred environment name (e.g., `.venv` is a common convention)[^2][^3][^5][^6].

This command creates a new directory (`myenv` or `.venv`) containing a standalone Python installation and all necessary supporting files[^1][^3][^5].

---

### 4. Activate the Virtual Environment

- **On Windows:**

```bash
myenv\Scripts\activate
```

- **On macOS/Linux:**

```bash
source myenv/bin/activate
```

- After activation, your terminal prompt will show the environment name, e.g., `(myenv)`, indicating you are now working inside the virtual environment[^2][^3][^6].

---

### 5. Install Packages (Optional)

- Now, any Python packages you install using `pip` will be installed in this virtual environment only.

```bash
pip install <package-name>
```


---

### 6. Deactivate the Virtual Environment

- When you are done, exit the virtual environment by running:

```bash
deactivate
```

- Your prompt will return to normal, and you’ll be back to the system Python environment[^2][^3][^4].

---

### Summary Table

| Step | Windows Command | macOS/Linux Command |
| :-- | :-- | :-- |
| Create | `python -m venv myenv` | `python3 -m venv myenv` |
| Activate | `myenv\Scripts\activate` | `source myenv/bin/activate` |
| Deactivate | `deactivate` | `deactivate` |


---

**Tip:**
Using a virtual environment is a best practice for Python development, keeping your project dependencies isolated and manageable[^7].

---

**References:**
[^1][^2][^3][^5][^6][^7]

*⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂ References ⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂*

[^1]: https://docs.python.org/3/library/venv.html

[^2]: https://www.w3resource.com/python-interview/how-do-you-create-a-virtual-environment-in-python-using-the-venv-module.php

[^3]: https://docs.python.org/3/tutorial/venv.html

[^4]: https://www.youtube.com/watch?v=oN0cISyzWe8

[^5]: https://fastapi.tiangolo.com/virtual-environments/

[^6]: https://www.pythontutorial.net/python-basics/python-virtual-environments/

[^7]: https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/

[^8]: https://realpython.com/python-virtual-environments-a-primer/

[^9]: https://www.w3schools.com/python/python_virtualenv.asp

[^10]: https://www.youtube.com/watch?v=ySk09NKutm8

