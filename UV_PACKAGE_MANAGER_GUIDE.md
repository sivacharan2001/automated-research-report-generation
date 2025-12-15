# UV Package Manager Guide

## What is UV?

`uv` is an extremely fast Python package installer and resolver written in Rust. It's designed as a drop-in replacement for `pip` and `pip-tools`, offering significantly faster package installation and dependency resolution.

---

## Installation

### Windows (PowerShell)
```powershell
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```

### macOS/Linux
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### Using pip
```bash
pip install uv
```

### Verify Installation
```bash
uv --version
```

---

## Virtual Environment Management

### Create a Virtual Environment
```bash
# Create a new virtual environment
uv venv

# Create with a specific name
uv venv myenv

# Create with a specific Python version
uv venv --python 3.11
```

### Activate Virtual Environment

**Windows (PowerShell):**
```powershell
.venv\Scripts\Activate.ps1
```

**Windows (Command Prompt):**
```cmd
.venv\Scripts\activate.bat
```

**macOS/Linux:**
```bash
source .venv/bin/activate
```

### Deactivate Virtual Environment
```bash
deactivate
```

---

## Package Management

### Install Packages

#### Install a Single Package
```bash
uv pip install packagename
```

#### Install Multiple Packages
```bash
uv pip install package1 package2 package3
```

#### Install a Specific Version
```bash
uv pip install package==1.2.3
```

#### Install from Requirements File
```bash
uv pip install -r requirements.txt
```

#### Install in Editable Mode (Development)
```bash
uv pip install -e .
```

### Uninstall Packages

```bash
# Uninstall a single package
uv pip uninstall packagename

# Uninstall multiple packages
uv pip uninstall package1 package2

# Uninstall all packages from requirements.txt
uv pip uninstall -r requirements.txt
```

### List Installed Packages

```bash
# List all installed packages
uv pip list

# Show outdated packages
uv pip list --outdated
```

### Show Package Information

```bash
uv pip show packagename
```

### Freeze Installed Packages

```bash
# Export to requirements.txt
uv pip freeze > requirements.txt

# View frozen packages
uv pip freeze
```

---

## Working with Requirements Files

### Install from requirements.txt
```bash
uv pip install -r requirements.txt
```

### Create requirements.txt
```bash
# From currently installed packages
uv pip freeze > requirements.txt
```

### Install from Multiple Requirements Files
```bash
uv pip install -r requirements.txt -r requirements-dev.txt
```

---

## Dependency Resolution & Compilation

### Compile Requirements (pip-compile equivalent)
```bash
# Create requirements.txt from requirements.in
uv pip compile requirements.in -o requirements.txt

# Upgrade all packages
uv pip compile requirements.in --upgrade

# Upgrade specific package
uv pip compile requirements.in --upgrade-package django
```

### Sync Environment (pip-sync equivalent)
```bash
# Install/uninstall packages to match requirements.txt exactly
uv pip sync requirements.txt
```

---

## Advanced Commands

### Install with Constraints
```bash
uv pip install -r requirements.txt -c constraints.txt
```

### Dry Run (Show What Would Be Installed)
```bash
uv pip install packagename --dry-run
```

### Install with Index URL
```bash
uv pip install packagename --index-url https://pypi.org/simple
```

### Install from Git Repository
```bash
uv pip install git+https://github.com/user/repo.git
```

### Install from Local Directory
```bash
uv pip install /path/to/package
```

---

## Common Workflows

### Starting a New Project

```bash
# 1. Create project directory
mkdir my-project
cd my-project

# 2. Create virtual environment
uv venv

# 3. Activate virtual environment
.venv\Scripts\Activate.ps1  # Windows PowerShell
# OR
source .venv/bin/activate    # macOS/Linux

# 4. Install packages
uv pip install django flask requests

# 5. Freeze dependencies
uv pip freeze > requirements.txt
```

### Working with Existing Project

```bash
# 1. Clone repository
git clone https://github.com/user/repo.git
cd repo

# 2. Create virtual environment
uv venv

# 3. Activate virtual environment
.venv\Scripts\Activate.ps1  # Windows PowerShell

# 4. Install dependencies
uv pip install -r requirements.txt
```

### Updating Dependencies

```bash
# 1. Update all packages
uv pip install --upgrade -r requirements.txt

# 2. Freeze updated dependencies
uv pip freeze > requirements.txt
```

---

## Package Installation Speed Comparison

| Tool | Typical Speed |
|------|---------------|
| pip  | Baseline |
| uv   | **10-100x faster** |

---

## Common Errors & Solutions

### Error: "Package(s) not found"
**Issue:** Package not installed
```bash
# Solution: Install the package
uv pip install packagename
```

### Error: "No virtual environment found"
**Issue:** Virtual environment not created or activated
```bash
# Solution 1: Create virtual environment
uv venv

# Solution 2: Activate virtual environment
.venv\Scripts\Activate.ps1  # Windows
```

### Error: Typo in filename (e.g., `requirements,txt`)
**Issue:** Using comma instead of dot
```bash
# Wrong:
uv pip install -r requirements,txt

# Correct:
uv pip install -r requirements.txt
```

---

## Tips & Best Practices

1. **Always use a virtual environment** - Never install packages globally
2. **Freeze dependencies** - Use `uv pip freeze > requirements.txt` to track dependencies
3. **Pin versions in production** - Use exact versions (e.g., `package==1.2.3`)
4. **Use `.venv` as the default name** - Most tools recognize this automatically
5. **Add `.venv/` to `.gitignore`** - Never commit virtual environments to version control
6. **Use `uv pip sync`** - Ensures environment matches requirements exactly

---

## Useful Aliases (Optional)

Add to your shell profile for convenience:

**PowerShell (`$PROFILE`):**
```powershell
function uvi { uv pip install $args }
function uvl { uv pip list $args }
function uvr { uv pip install -r requirements.txt }
```

**Bash/Zsh (`~/.bashrc` or `~/.zshrc`):**
```bash
alias uvi='uv pip install'
alias uvl='uv pip list'
alias uvr='uv pip install -r requirements.txt'
```

---

## Quick Reference

| Task | Command |
|------|---------|
| Create venv | `uv venv` |
| Activate venv (Windows) | `.venv\Scripts\Activate.ps1` |
| Activate venv (Unix) | `source .venv/bin/activate` |
| Install package | `uv pip install package` |
| Install from requirements | `uv pip install -r requirements.txt` |
| Uninstall package | `uv pip uninstall package` |
| List packages | `uv pip list` |
| Show package info | `uv pip show package` |
| Freeze packages | `uv pip freeze > requirements.txt` |
| Sync environment | `uv pip sync requirements.txt` |
| Compile requirements | `uv pip compile requirements.in -o requirements.txt` |

---

## Additional Resources

- **Official Documentation:** https://docs.astral.sh/uv/
- **GitHub Repository:** https://github.com/astral-sh/uv
- **Discord Community:** https://discord.gg/astral-sh

---

**Created:** December 2025  
**Version:** 1.0
