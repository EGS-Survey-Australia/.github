# Miniforge Setup Guide

Miniforge is required for all EGS Python tools. We use it instead of standard pip/venv because
our tools depend on compiled geospatial and scientific libraries (GDAL, PROJ, cfgrib, NetCDF4,
HDF5) that are unreliable to install via pip on Windows. Miniforge installs them correctly and
ensures everyone runs an identical environment.

---

## What is Miniforge?

Miniforge gives you the `conda` package manager configured to use **conda-forge** — a free,
community-maintained package channel. It is functionally identical to Anaconda but has no
commercial licence restrictions.

The key benefit for sharing code: instead of sending someone a list of packages to install,
you give them an `environment.yml` file and one command rebuilds your exact environment on
their machine.

---

## Windows Installation

**If you have Anaconda installed, uninstall it first.** Running Anaconda and Miniforge side by
side causes conflicts. Uninstall via Windows Settings → Apps.

1. Download the Miniforge3 Windows installer from https://conda-forge.org/download/
2. Run the installer
3. Install for **"Just Me"** and accept the default install location
4. Leave **"Register Miniforge3 as my default Python"** unticked
5. When installation is complete, open **Miniforge Prompt** from the Start menu

All `conda` commands should be run from the **Miniforge Prompt**.

**Optional but recommended** — run this once to stop conda loading the base environment
automatically every time you open a terminal:

```
conda config --set auto_activate_base false
```

---

## macOS / Linux Installation

Do **not** uninstall the Python that came with your operating system — the OS needs it.
Install Miniforge alongside it.

Open a terminal and run:

```bash
curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
bash Miniforge3-$(uname)-$(uname -m).sh
```

Follow the prompts and close and reopen your terminal when done.

---

## Installing a tool

Every EGS repository includes an `environment.yml` file. To install any tool:

```bash
# 1. Clone the repository (requires git — https://git-scm.com/downloads)
git clone https://github.com/EGS-Survey-Australia/<repo-name>.git
cd <repo-name>

# 2. Build the environment (downloads all dependencies automatically)
conda env create -f environment.yml

# 3. Activate the environment
conda activate <env-name>
```

The env name is set inside `environment.yml`. After activation the tool's command is available
in your terminal.

For subsequent uses just activate — no need to recreate the environment:

```bash
conda activate <env-name>
```

---

## PyCharm setup

Build the environment in the Miniforge Prompt first (above), then connect PyCharm to it.

**Settings → Python Interpreter → Add Interpreter → Conda Environment → Use existing environment → select the environment from the list**

If PyCharm cannot find conda automatically, point it at the conda executable manually:

- Windows: `C:\Users\<you>\miniforge3\Scripts\conda.exe`
- macOS/Linux: `~/miniforge3/bin/conda`

Once conda is found the environment appears in the list — select it and click OK.

Always build environments in the Miniforge Prompt first, then connect PyCharm to the existing
environment. Do not let PyCharm create conda environments through its own dialog.

---

## Common commands

| Task | Command |
|------|---------|
| List all environments | `conda env list` |
| Create from file | `conda env create -f environment.yml` |
| Activate an environment | `conda activate <name>` |
| Deactivate | `conda deactivate` |
| Install a package | `conda install <package>` |
| Update a package | `conda update <package>` |
| Remove an environment | `conda env remove -n <name>` |

If `conda install` is slow, use `mamba install` instead — it is pre-installed with Miniforge
and does the same thing much faster.

---

## Questions

Contact Ryan for help with setup or to be added to the organisation.
