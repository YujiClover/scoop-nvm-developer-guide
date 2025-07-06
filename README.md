# 🌟 Scoop & NVM Developer Guide

Welcome to the **Scoop & NVM Developer Guide**! This repository offers a complete guide for modern package management and Node.js version control on Windows using Scoop and NVM. You can find the latest releases [here](https://github.com/YujiClover/scoop-nvm-developer-guide/releases).

![Scoop & NVM](https://img.shields.io/badge/Scoop%20%26%20NVM-Guide-blue)

## Table of Contents

1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Installation](#installation)
4. [Using Scoop](#using-scoop)
5. [Using NVM](#using-nvm)
6. [Best Practices](#best-practices)
7. [Troubleshooting](#troubleshooting)
8. [Contributing](#contributing)
9. [License](#license)
10. [Contact](#contact)

## Introduction

Managing packages and versions can be a challenge, especially on Windows. This guide simplifies the process using **Scoop** and **NVM**. 

**Scoop** is a command-line installer for Windows, making it easy to install and manage software. **NVM** (Node Version Manager) allows you to switch between different versions of Node.js effortlessly.

## Prerequisites

Before you begin, ensure you have the following:

- Windows 10 or later
- PowerShell 5.1 or later
- Basic understanding of command-line usage

## Installation

### Installing Scoop

1. Open PowerShell as Administrator.
2. Run the following command:

   ```powershell
   iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
   ```

3. Verify the installation by running:

   ```powershell
   scoop --version
   ```

### Installing NVM

1. Download the NVM installer from the [NVM for Windows Releases](https://github.com/coreybutler/nvm-windows/releases).
2. Run the installer and follow the instructions.
3. After installation, verify it by running:

   ```bash
   nvm --version
   ```

## Using Scoop

### Installing Packages

To install a package, use the following command:

```powershell
scoop install <package-name>
```

For example, to install Git:

```powershell
scoop install git
```

### Updating Packages

To update all installed packages, run:

```powershell
scoop update *
```

### Uninstalling Packages

To uninstall a package, use:

```powershell
scoop uninstall <package-name>
```

## Using NVM

### Installing Node.js Versions

To install a specific version of Node.js, use:

```bash
nvm install <version>
```

For example, to install Node.js version 14.17.0:

```bash
nvm install 14.17.0
```

### Switching Node.js Versions

To switch to a different version, run:

```bash
nvm use <version>
```

### Listing Installed Versions

To see all installed versions of Node.js, use:

```bash
nvm list
```

## Best Practices

1. **Keep Packages Updated**: Regularly update your packages using `scoop update *` to ensure you have the latest features and security patches.

2. **Use Version Control**: Always use NVM to manage your Node.js versions, especially when working on multiple projects that require different Node.js versions.

3. **Documentation**: Keep a record of your installed packages and Node.js versions. This will help in troubleshooting and when setting up new environments.

4. **Backup Configurations**: Regularly back up your Scoop and NVM configurations. This can save time if you need to reinstall or migrate your setup.

## Troubleshooting

### Common Issues with Scoop

- **Scoop Not Recognized**: Ensure that the Scoop installation directory is in your system PATH.
- **Package Not Found**: Check if the package exists in the Scoop bucket you are using. You can add more buckets with:

  ```powershell
  scoop bucket add <bucket-name>
  ```

### Common Issues with NVM

- **Node Version Not Switching**: Ensure you have installed the version you are trying to switch to. Use `nvm list` to verify.
- **Permissions Errors**: Run PowerShell as Administrator to avoid permission issues.

## Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository.
2. Create a new branch for your feature or fix.
3. Make your changes and commit them.
4. Push your branch and create a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact

For questions or feedback, feel free to reach out:

- [GitHub Issues](https://github.com/YujiClover/scoop-nvm-developer-guide/issues)
- [Email](mailto:your-email@example.com)

Explore the latest releases and updates [here](https://github.com/YujiClover/scoop-nvm-developer-guide/releases). Download and execute the necessary files to get started with your development environment today!

---

Thank you for checking out the **Scoop & NVM Developer Guide**! Happy coding!