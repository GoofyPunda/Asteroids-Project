# Building Asteroid's

## Description

Asteroids is a Python game project (following the boot.dev Pygame curriculum) that recreates the classic Asteroids arcade game. It uses Pygame for graphics & input and `uv` for project/dependency management.

## Status

🚧 Project in Progress:
- project setup with `uv` and virtual environment — 27/09/2026
- constants module for screen dimensions — 27/09/2026
- pygame initialization and screen resolution printout — 27/09/2026
- game state logging module added — 27/09/2026

**IMPORTANT-NOTE:** This README will contain EVERYTHING — entries are dated & kept even if later code changes or removes what they describe. If a change affects existing output/behaviour, a new dated note is added rather than the old one being deleted.

## Features

- Initializes Pygame & reports the installed version on startup
- Central `constants.py` module storing shared values like screen width/height, avoiding magic numbers scattered through the code
- Logging system (`logger.py`) that snapshots game state to `game_state.jsonl` roughly once per second, for debugging without needing to watch the game window directly

## Project Structure (files/folders) - Updated as the project grows
```
├── .venv/
├── __pycache__/
├── .gitignore
├── .python-version
├── constants.py
├── logger.py
├── main.py
├── pyproject.toml
├── uv.lock
└── README.md
```

## Requirements

- Python 3.13
- [uv](https://github.com/astral-sh/uv) (Python package/project manager)
- Pygame 2.6+ (installed automatically into the project's virtual environment via `uv`)

## Usage

Run the script from the project root directory using `uv`, so it picks up the project's virtual environment automatically:

```zsh
uv run main.py
```

## Example Output

**27/09/2026** — after adding constants and the startup print statements:
```
pygame 2.6.1 (SDL 2.28.4, Python 3.13.15)
Hello from the pygame community. https://www.pygame.org/contribute.html
Starting Asteroids with pygame version: 2.6.1
Screen width: 1280
Screen height: 720
```

## How It Works (this specific project, variables can change)

**main.py**
- `main()` — entry point; prints the pygame version and the configured screen width/height on startup

**constants.py**
- `SCREEN_WIDTH` — the game window's width in pixels (1280)
- `SCREEN_HEIGHT` — the game window's height in pixels (720)

**logger.py**
- Provided logging utility (not written from scratch, was instead given to us in BootDev Chapter 2 Lesson 2) that snapshots the game's local state at about once per second & writes it to `game_state.jsonl`, so that the game behaviour is able to be verified without the need to manually inspect the running window

## Troubleshooting Notes

- **27/09/2026 — Backwards import syntax**: Wrote `import from constants import SCREEN_WIDTH` instead of `from constants import SCREEN_WIDTH`. Python's `from X import Y` order is fixed — `from` always comes before the module name, `import` always comes before the names being pulled in. Fixed by rewriting the line in the correct order.

- **27/09/2026 — Typo in imported name**: Wrote `SREEN_WIDTH` instead of `SCREEN_WIDTH` when importing, which doesn't match the variable actually defined in `constants.py`. Lesson: imported names must match the source file's spelling exactly — Python won't auto-correct typos.

- **27/09/2026 — `ModuleNotFoundError: No module named 'pygame'`**: Ran the script with plain `python3 main.py`, which uses the system Python rather than the project's virtual environment where pygame was actually installed. Fixed by running it through `uv run main.py` instead, which automatically uses the project's own `.venv`.

- **27/09/2026 — Missing `.gitignore`**: The lesson said `uv init` would auto-create a `.gitignore`, but it wasn't present after setup. Also got confused between two different `.gitignore` files — one auto-generated later inside `.venv/` (governs pygame/venv internals only) and the actual project-level one next to `main.py` (created manually with `touch .gitignore`, and the one that matters for git tracking). Lesson: check *which* `.gitignore` you're editing when a project has more than one.

## Other Mentions

- **27/09/2026** — Learning Git/source control alongside this project — using VS Code's Source Control panel (stage → commit → push) rather than the terminal for most git operations, with terminal used mainly for running/testing the code via `uv`.