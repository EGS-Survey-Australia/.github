# EGS Survey Australia — Python Scripts

This organisation is home to Python tools developed by the EGS Survey Australia team for survey data processing, analysis, and reporting.

---

## Getting started

**Prerequisites — install these first:**

1. **Miniforge** — required for all tools. See the **[Miniforge Setup Guide](../MINIFORGE_SETUP.md)** for installation instructions.
2. **git** — required to clone repositories and pull updates. Download from https://git-scm.com/downloads (accept all defaults on Windows).

Once set up, every tool follows the same pattern:

```bash
git clone https://github.com/EGS-Survey-Australia/<repo-name>.git
cd <repo-name>
conda env create -f environment.yml
conda activate <env-name>
```

The `environment.yml` file in each repo handles all dependencies automatically — no manual package installation needed.

---

## What belongs in this organisation

This organisation is for Python tools you want to share with the team — but not everything qualifies. Before adding a repo, check it meets the bar:

**Good candidates:**
- Tools for moderate to complex workflow tasks that represent hours or more of development effort
- Code that's critical for everyone to be running from the same tested, verified version — e.g. anything doing survey computations

**Not a good fit:**
- Simple one-off scripts that anyone could reproduce in a few minutes from ChatGPT
- Code that hasn't been tested or used by at least one other person

**Still in development?**
Develop in your own GitHub account first. If you want colleagues to collaborate mid-development, you can add it here — but put a clear warning in the README so people know it's not production-ready.

---

## Rules for all repositories

Every repo in this organisation must follow these rules:

| Rule | Requirement |
|------|------------|
| README | Required. Describe what the tool does and who to contact. |
| Environment | Must use Miniforge + `environment.yml`. No pip/venv. |
| Visibility | Private. Not public. |
| Owners | Minimum 2 people with admin access per repo. |
| Naming | Simple and explicit. Use `egs-tool-name` or `purpose-name` format. |
| Credentials | Never commit API keys, passwords, or tokens. Keep them in config files listed in `.gitignore`. |
| Bugs & improvements | If you find a bug or have an improvement idea, raise an issue on the repo. |

**Security:** Enable 2-factor authentication on your GitHub account — go to Settings → Password and authentication → https://github.com/settings/security.

---

## Why Miniforge — not pip or venv

All tools in this organisation use Miniforge because we rely heavily on compiled geospatial and scientific libraries — GDAL, PROJ, cfgrib, NetCDF4, HDF5. These are notoriously painful to install through standard Python/pip on Windows and produce inconsistent results across machines. Miniforge installs them reliably, and `environment.yml` means anyone can recreate your exact environment with one command.

Do not use `pip install` or `python -m venv` as the primary environment for tools shared here. If a package is only on PyPI and not available through conda, install it via pip inside the activated conda environment — that's fine. But the environment itself must be conda-based and defined in `environment.yml`.

---

## Creating a new repository

Follow this checklist when adding a new tool to the organisation.

### 1. The repo must include

- `README.md` — what the tool does, prerequisites, install steps, and how to run it
- `environment.yml` — defines the conda environment (see template below)
- `.gitignore` — at minimum exclude `__pycache__/`, `*.pyc`, `.venv/`, `data/`, and any credential or config files

### 2. environment.yml template

Every `environment.yml` must specify the `conda-forge` channel so environments build consistently across all machines:

```yaml
name: egs-<tool-name>
channels:
  - conda-forge
dependencies:
  - python=3.12
  - <package-1>
  - <package-2>
  - pip
  - pip:
    - -e .        # include only if the repo is an installable package with a CLI
```

- Use `conda-forge` as the only channel — do not mix with `defaults`
- List only the packages you explicitly depend on (not every sub-dependency)
- If a package is only on PyPI, add it under `pip:` at the bottom
- Name the environment `egs-<tool-name>` so it's clear where it came from

### 3. Standard README prerequisites block

Copy this into your README and fill in the credential steps that apply:

```markdown
## Prerequisites

- **Miniforge** — required for environment management. See [SETUP_GUIDE.md](SETUP_GUIDE.md) for installation instructions.
- **git** — required to clone this repository and pull updates. Download from https://git-scm.com/downloads (accept all defaults on Windows).
- [any API credentials your tool needs]

## Installation

\`\`\`bash
git clone https://github.com/EGS-Survey-Australia/<repo-name>.git
cd <repo-name>
conda env create -f environment.yml
conda activate egs-<tool-name>
\`\`\`
```

### 4. PyCharm setup note (optional but useful)

If your tool is used in PyCharm, include this in your README:

> Build the environment in the Miniforge Prompt first (above), then in PyCharm go to **Settings → Python Interpreter → Add Interpreter → Conda Environment → Use existing environment** and select `egs-<tool-name>` from the list. If PyCharm cannot find conda, point it manually at `C:\Users\<you>\miniforge3\Scripts\conda.exe`.

---

## Joining the organisation

Send your GitHub username to Ryan and you will be added. Once added, you can clone any repo using the standard pattern above.
