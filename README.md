# Jerry John Doviavu's Personal Academic Website

This repository contains my personal academic website and data science blog created for DSCI 521. It features interactive posts and computational analyses built using Quarto, Python, and R.

## Prerequisites & Required Tools

These commands assume a **macOS or Linux shell** (bash/zsh). If you're on Windows, use WSL or Git Bash — the `R -e "..."` syntax below is not guaranteed to work as written in Command Prompt or PowerShell.

Install the following before building the site. Versions shown are what this project was built and tested with:

| Tool | Version used | Install |
|---|---|---|
| **Quarto** | 1.10.18 | [quarto.org/docs/get-started](https://quarto.org/docs/get-started/) |
| **uv** | 0.12.5 | `curl -LsSf https://astral.sh/uv/install.sh \| sh` — see [docs.astral.sh/uv](https://docs.astral.sh/uv/getting-started/installation/) |
| **Python** | 3.14.7 | Installed automatically by `uv` via `uv sync` (no separate install needed) |
| **R** | 4.6.1 | [cran.r-project.org](https://cran.r-project.org/) |

*Note: You do not need to install `renv` manually — it bootstraps itself automatically via the `.Rprofile` in this repository the first time R is started at the project root.*

## Setup & Rebuilding the Site (Step-by-Step)

Run these commands in order from a Terminal / Shell, exactly as shown, to go from a fresh clone to a fully built site.

### 1. Clone the repository

Run in your **Terminal / Shell**, in whatever directory you want the project folder created:

```bash
git clone https://github.com/jerryjohndoviavu/jerryjohndoviavu.github.io.git
cd jerryjohndoviavu.github.io
```

Everything below assumes your working directory is this project root (`jerryjohndoviavu.github.io/`).

### 2. Restore the Python environment

Run in your **Terminal / Shell**, from the project root. This creates the `.venv` virtual environment and installs all required Python packages (pandas, seaborn, matplotlib, palmerpenguins, jupyter, ipykernel):

```bash
uv sync
```

### 3. Restore the R package environment

Run in your **Terminal / Shell**, from the project root. This starts R non-interactively, which triggers `renv` to bootstrap itself and then restores all R packages listed in `renv.lock`:

```bash
R -e "renv::restore()"
```

*(Equivalent alternative: open an interactive R console at the project root and type `renv::restore()` directly.)*

### 4. Render the website

Run in your **Terminal / Shell**, from the project root:

```bash
uv run quarto render
```

## Output Location & Local Preview

- **Built site location:** The rendered static HTML pages and compiled assets are written to the `docs/` directory at the project root. This folder is configured for automatic deployment via GitHub Pages.
- **Local preview:** To view and interact with the built site locally in your default web browser, run in your **Terminal / Shell**, from the project root:

```bash
uv run quarto preview
```

## Data Sources & Network Requirements

- **R post** (`posts/gapminder-r/index.qmd`): Uses the [Gapminder Dataset](https://www.gapminder.org/data/) (licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)).
- **Python post** (`posts/palmer-penguins-python/index.qmd`): Uses the [Palmer Penguins Dataset](https://allisonhorst.github.io/palmerpenguins/) (licensed under [CC0](https://creativecommons.org/publicdomain/zero/1.0/)).

Both datasets are bundled as installable packages and are fully installed into the project's local environments (`.venv` and `renv/library`) during Steps 2 and 3 above.

**Network access:**
- Required during Steps 1–3 (cloning the repo, and fetching packages from GitHub, PyPI, and CRAN).
- **Not** required during `uv run quarto render` (Step 4) — all data and package dependencies are already present locally by that point.