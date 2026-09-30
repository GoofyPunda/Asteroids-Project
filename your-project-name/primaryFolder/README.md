# Building Asteroid's

## Description

Asteroids is a Python game project (following the boot.dev Pygame curriculum) that recreates the classic Asteroids arcade game. It uses Pygame for graphics & input and `uv` for project/dependency management.

**IMPORTANT-NOTE:** This README will contain EVERYTHING — entries are dated & kept even if later code changes or removes what they describe. If a change affects existing output/behaviour, a new dated note is added rather than the old one being deleted.
## Status

🚧 Project in Progress:
- project setup with `uv` and virtual environment — 27/09/2026
- constants module for screen dimensions — 27/09/2026
- pygame initialization and screen resolution printout — 27/09/2026
- game state logging module added — 27/09/2026
- game window opens via `pygame.display.set_mode` — 30/09/2026
- game loop added (log_state, handle events - allow's for the extrnal window to be opened & closed at will, fill black & flip) — 30/09/2026
- `pygame.QUIT` event handling so the window's close button exits cleanly — 30/09/2026
- 60 FPS cap and delta time (`dt`) added using `pygame.time.Clock` — 30/09/2026


## Features

- Initializes Pygame & reports the installed version on startup
- Central `constants.py` module storing shared values like screen width/height, avoiding magic numbers scattered through the code
- Logging system (`logger.py`) that snapshots game state to `game_state.jsonl` roughly once per second, for debugging without needing to watch the game window directly
- Opens a 1280x720 black game window that stays open in a game loop until the window is closed (added 30/09/2026)
- Window close button exits the game cleanly via `pygame.QUIT` event handling (added 30/09/2026)
- Game is capped at a maximum of 60 FPS & now tracks delta time (`dt`) since the last frame (added 30/09/2026)

## Project Structure (files/folders) - May be updated as the Project grows
```
├── .venv/
├── __pycache__/
├── .gitignore
├── .python-version
├── constants.py
├── game_state.jsonl
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

**30/09/2026 note:** `uv run main.py` only looks in the folder you're currently in, so you may have to `cd` into the folder that contains `main.py` first (`cd your-project-name/primaryFolder`).

## Example Output

**27/09/2026** — after adding constants and the startup print statements:
```
pygame 2.6.1 (SDL 2.28.4, Python 3.13.15)
Hello from the pygame community. https://www.pygame.org/contribute.html
Starting Asteroids with pygame version: 2.6.1
Screen width: 1280
Screen height: 720
```

**30/09/2026** — after adding the game loop:
```
pygame 2.6.1 (SDL 2.28.4, Python 3.13.15)
Hello from the pygame community. https://www.pygame.org/contribute.html
```
A black 1280x720 window opens & stays open until it's manually closed. As of right now, the three startup `print` lines from 27/09/2026 no longer appear. 
The terminal is also unable to be used until the pygame window closes at this time of the project(may carry through until the end).

**30/09/2026** — while testing the 60 FPS cap, `dt` was temporarily printed every frame. The first value was larger (~0.485, since it includes the time spent setting up the window), then it settled at roughly 0.016–0.017 seconds per frame. The `print(dt)` line was removed afterwards, as the lesson asked - "Remove the line that prints dt to the console (but leave the variable itself, we'll need it later) - it creates a lot of noise, we just wanted to see it working"- so this doesn't appear in the normal output.

## How It Works (this specific project, variables can change)

**main.py**
- `main()` — entry point; prints the pygame version and the configured screen width/height on startup
- **30/09/2026 update:** `main()` now calls `pygame.init()`, creates the window with `pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))`, then runs the game loop
- The game loop (`while True:`) repeats every frame: `log_state()`, handle events (returning on `pygame.QUIT`), `screen.fill("black")`, then `pygame.display.flip()` (flip comes last so the finished frame is what gets shown)
- The general idea of a game loop: check player input, update the game world, draw to the screen, many times per second
- **30/09/2026 update (FPS + delta time):** a `pygame.time.Clock()` is stored in the `clock` variable, alongside a `dt` variable that starts at `0.0` (a float, since it will hold a decimal number of seconds). At the end of each pass of the game loop, `dt = clock.tick(60) / 1000` caps the game at 60 FPS and stores how many seconds passed since the last frame. `.tick(60)` returns milliseconds, hence dividing by 1000.
- **Why delta time matters:** it decouples the game's speed from the computer's speed. If a computer's CPU speeds up or slows down, things like the asteroids shouldn't speed up or slow down with it. Movement can later be multiplied by `dt` so it stays consistent. `dt` isn't used for anything yet.
- **Placement matters:** the `dt = clock.tick(60) / 1000` line has to sit at the same indentation as the `for event` loop (directly in the `while` loop's body), not inside it, so it runs once per frame rather than once per event.

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

- **30/09/2026 — `Failed to spawn main.py: No such file or directory`**: Ran `uv run main.py` from the outer `Asteroids-Project` folder, but `main.py` lives inside a nested folder, so the terminal couldn't find it. Fixed by using `pwd` and `ls` to see where I was, then `cd`-ing into the folder that contains `main.py`. Lesson: the terminal only looks in the folder it's standing in.

## Other Mentions

- **27/09/2026** — Learning Git/source control alongside this project — using VS Code's Source Control panel (stage → commit → push) rather than the terminal for most git operations, with terminal used mainly for running/testing the code via `uv`.

- **30/09/2026** — Started using a separate git branch for each lesson (`gameLoop` for this one) so mistakes never touch `main`. Committed and pushed the branch, then merged it into `main` from the terminal (`git checkout main`, `git merge gameLoop`, `git push origin main`). The branch was kept afterwards to preserve history. I started to do this as I learnt from my bookbot mistakes