## Step-by-Step Guide to Set Up and Use NVM (Node Version Manager) with Node.js

### 1. Install NVM

#### On macOS/Linux:

- Open your terminal.
- Run the install script:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
```

Or using wget:

```bash
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
```

- This installs NVM into your home directory (`~/.nvm`) and updates your shell profile (`.bashrc`, `.zshrc`, etc.) to load NVM.
- Reload your shell configuration:

```bash
source ~/.bashrc
```

or restart your terminal.
- Verify installation:

```bash
nvm --version
```


#### On Windows:

- Download the NVM for Windows installer from the [nvm-windows GitHub repository](https://github.com/coreybutler/nvm-windows/releases).
- Run the installer and follow the prompts.
- Open a new Command Prompt or PowerShell window and verify:

```powershell
nvm --version
```


---

### 2. Install Node.js Versions Using NVM

- To install the latest Node.js version:

```bash
nvm install node
```

- To install a specific version, e.g., 18.14.2:

```bash
nvm install 18.14.2
```

- List all available Node.js versions:

```bash
nvm ls-remote
```


---

### 3. Use a Specific Node.js Version

- To switch to a specific installed version:

```bash
nvm use 18.14.2
```

- To set a default version for new shells:

```bash
nvm alias default 18.14.2
```

- Verify the active Node.js version:

```bash
node -v
```


---

### 4. Manage Installed Node.js Versions

- List installed versions:

```bash
nvm ls
```

- Uninstall a version:

```bash
nvm uninstall 16.0.0
```


---

### 5. Run Node.js Commands Without Switching Shell Version

- Run a command with a specific Node.js version without switching:

```bash
nvm run 14.17.0 --version
```


---

### Summary Table

| Step | Command/Action |
| :-- | :-- |
| Install NVM (macOS/Linux) | `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash` |
| Install NVM (Windows) | Download and run installer from nvm-windows GitHub |
| Install latest Node | `nvm install node` |
| Install specific Node | `nvm install <version>` |
| Use specific Node version | `nvm use <version>` |
| Set default Node version | `nvm alias default <version>` |
| List installed versions | `nvm ls` |
| Run command with version | `nvm run <version> -- <command>` |


---

NVM lets you easily install, switch, and manage multiple Node.js versions on your system, enabling smooth development across projects requiring different Node environments.

*⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂ References ⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂*

[^1]: https://codedamn.com/news/nodejs/nvm-installation-setup-guide

[^2]: https://github.com/nvm-sh/nvm

[^3]: https://www.linode.com/docs/guides/how-to-install-use-node-version-manager-nvm/

[^4]: https://www.sitepoint.com/quick-tip-multiple-versions-node-nvm/

[^5]: https://help.dreamhost.com/hc/en-us/articles/360029083351-Installing-a-custom-version-of-NVM-and-Node-js

[^6]: https://blog.tericcabrel.com/install-node-with-nvm/

[^7]: https://4geeks.com/how-to/install-nvm-on-every-operating-system

[^8]: https://heynode.com/tutorial/install-nodejs-locally-nvm/

