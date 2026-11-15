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
- `CircleShape` base class added in `circleshape.py` (inherits from `pygame.sprite.Sprite`) — 01/10/2026
- `Player` class added in `player.py` (inherits from `CircleShape`), drawn as a white triangle in the centre of the window — 07/11/2026
- Player rotation added: `A` rotates the ship left and `D` rotates it right (`rotate` and `update` methods on `Player`, plus a `PLAYER_TURN_SPEED` constant) — 13/11/2026
- Player movement added: `W` moves the ship forward in the direction it's facing and `S` moves it backward (`move` method on `Player`, plus a `PLAYER_SPEED` constant) — 13/11/2026
- Sprite groups added: `updatable` and `drawable` groups in `main.py`, which the `Player` joins automatically through `Player.containers`, so the game loop updates and draws the groups instead of the player directly — 14/11/2026
- `Asteroid` class added in `asteroid.py` (inherits from `CircleShape`), drawn as a white circle outline that drifts in a straight line, plus a new `asteroids` group and the `ASTEROID_*` constants — 14/11/2026
- `AsteroidField` added in `asteroidfield.py`, which keeps spawning new asteroids from the edges of the screen — 14/11/2026
- Collision detection added: `collides_with` on `CircleShape`, so flying into an asteroid logs a `player_hit` event, prints `Game over!` and ends the game — 14/11/2026
- Shooting added: the spacebar fires small round bullets (`Shot` class in `shot.py`) in the direction the ship is facing, plus a `shots` group and the `SHOT_RADIUS` and `PLAYER_SHOOT_SPEED` constants — 15/11/2026


## Features

- Initializes Pygame & reports the installed version on startup
- Central `constants.py` module storing shared values like screen width/height, avoiding magic numbers scattered through the code
- Logging system (`logger.py`) that snapshots game state to `game_state.jsonl` roughly once per second, for debugging without needing to watch the game window directly
- Opens a 1280x720 black game window that stays open in a game loop until the window is closed (added 30/09/2026)
- Window close button exits the game cleanly via `pygame.QUIT` event handling (added 30/09/2026)
- Game is capped at a maximum of 60 FPS & now tracks delta time (`dt`) since the last frame (added 30/09/2026)
- Reusable `CircleShape` base class that stores a position, velocity and radius for game objects (added 01/10/2026)
- A `Player` that spawns in the centre of the window and is drawn as a white triangle outline every frame (its hitbox is a circle) (added 07/11/2026)
- The player's ship rotates left/right while the `A`/`D` keys are held, at a speed scaled by `dt` so it turns at the same rate on any computer (added 13/11/2026)
- The player's ship flies forward/backward with `W`/`S` in whatever direction it is currently pointing, again scaled by `dt` so the speed doesn't depend on the computer (added 13/11/2026)
- Game objects are managed with pygame sprite groups (`updatable` and `drawable`), so one call updates everything that needs updating and one loop draws everything that needs drawing, which keeps the game loop tidy as more objects are added (added 14/11/2026)
- Asteroids (white circle outlines) drift across the screen in straight lines at a constant speed, and the `AsteroidField` spawns a new one from a random edge of the screen roughly every 0.8 seconds, with a random size, speed and direction (added 14/11/2026)
- Collision detection between circular shapes: if the player touches an asteroid, the hit is logged as a `player_hit` event in `game_events.jsonl`, `Game over!` is printed to the terminal and the game exits. Asteroids simply pass through each other for now (added 14/11/2026)
- The player can shoot: holding the spacebar fires small white circles (bullets) from the ship in the direction it is currently facing, at a constant speed. For now, holding the spacebar fires a constant stream of bullets and the bullets pass straight through asteroids without any effect (both are expected at this stage of the course) (added 15/11/2026)

## Project Structure (files/folders) - May be updated as the Project grows
```
├── .venv/
├── __pycache__/
├── .gitignore
├── .python-version
├── asteroid.py
├── asteroidfield.py
├── circleshape.py
├── constants.py
├── game_events.jsonl
├── game_state.jsonl
├── logger.py
├── main.py
├── player.py
├── pyproject.toml
├── shot.py
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

**13/11/2026 note:** once the game is running, hold `A` to rotate the ship left and `D` to rotate it right.

**13/11/2026 note (movement):** `W` flies the ship forward (the way the triangle's point is facing) and `S` flies it backward. Combine them with `A`/`D` to steer.

**14/11/2026 note:** asteroids now drift in from the edges of the screen. If the ship touches one, the game ends immediately and `Game over!` is printed in the terminal (not in the game window), so keep an eye out and steer around them.

**15/11/2026 note:** press (or hold) the spacebar to shoot. Bullets fly out in the direction the ship is facing.

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

**07/11/2026** — after adding the `Player`: the terminal output is the same two pygame lines as 30/09/2026, but the black 1280x720 window now has a white triangle outline in the middle. The triangle points downwards because `rotation` is `0` and, in pygame, "forward" at zero rotation points down the screen. `game_state.jsonl` also now records the player (the Boot.dev test looks for `"type": "Player"` at `"pos": [640.0, 360.0]`, the centre of the screen).

**13/11/2026** — after adding rotation: the terminal output is unchanged, but holding `A` or `D` now spins the triangle in the window. The player's rotation value in `game_state.jsonl` changes as it turns (the Boot.dev test checks that at least one recorded `Player` rotation is not `0`, so the keys have to actually be pressed while the game runs).

**13/11/2026** — after adding movement: the terminal output is still unchanged, but `W`/`S` now fly the triangle around the window. The player's `pos` in `game_state.jsonl` changes as it moves (the Boot.dev test checks that the recorded `Player` positions contain more than one unique value, so the ship has to actually be flown around while the game runs).

**14/11/2026** — after adding sprite groups: the terminal output and the way the game looks and plays are exactly the same as before (the ship still turns and flies with `W`/`A`/`S`/`D`), because groups only change *how* the game loop manages objects, not what they do. The difference shows up in `game_state.jsonl`, which now records the `updatable` and `drawable` groups (the Boot.dev test checks that both groups contain at least one sprite).

**14/11/2026** — after adding asteroids: the terminal output is unchanged, but white circles of different sizes now appear at the edges of the window roughly every 0.8 seconds and drift across it while the ship flies around as before. `game_state.jsonl` now also records the `asteroids` group (the Boot.dev test checks that an `AsteroidField` is in the `updatable` group and that the `asteroids` group contains at least one asteroid at the end of the log).

**14/11/2026** — after adding collisions: when the ship touches an asteroid, the terminal prints `Game over!` and the program exits, so the game window closes right away. A single `player_hit` event is also written to `game_events.jsonl` (the Boot.dev test checks that exactly one is logged, so the game should be run once and crashed into an asteroid once).

**15/11/2026** — after adding shooting: the terminal output is the same as before, but pressing the spacebar now makes small white circles shoot out of the ship in the direction it is facing (they keep flying in a straight line, even off the edge of the screen, and pass through asteroids). `game_state.jsonl` now also records the `shots` group (the Boot.dev test checks that at least one recorded snapshot has `shots.count > 0`). The logger only records for roughly the first 16 seconds of a run, so the spacebar has to be pressed early in the run for the test to see any shots.

## How It Works (this specific project, variables can change)

**main.py**
- `main()` — entry point; prints the pygame version and the configured screen width/height on startup
- **30/09/2026 update:** `main()` now calls `pygame.init()`, creates the window with `pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))`, then runs the game loop
- The game loop (`while True:`) repeats every frame: `log_state()`, handle events (returning on `pygame.QUIT`), `screen.fill("black")`, then `pygame.display.flip()` (flip comes last so the finished frame is what gets shown)
- The general idea of a game loop: check player input, update the game world, draw to the screen, many times per second
- **30/09/2026 update (FPS + delta time):** a `pygame.time.Clock()` is stored in the `clock` variable, alongside a `dt` variable that starts at `0.0` (a float, since it will hold a decimal number of seconds). At the end of each pass of the game loop, `dt = clock.tick(60) / 1000` caps the game at 60 FPS and stores how many seconds passed since the last frame. `.tick(60)` returns milliseconds, hence dividing by 1000.
- **Why delta time matters:** it decouples the game's speed from the computer's speed. If a computer's CPU speeds up or slows down, things like the asteroids shouldn't speed up or slow down with it. Movement can later be multiplied by `dt` so it stays consistent. `dt` isn't used for anything yet.
- **Placement matters:** the `dt = clock.tick(60) / 1000` line has to sit at the same indentation as the `for event` loop (directly in the `while` loop's body), not inside it, so it runs once per frame rather than once per event.
- **07/11/2026 update (Player):** before the game loop starts, the centre of the screen is worked out (`SCREEN_WIDTH / 2`, `SCREEN_HEIGHT / 2`) and a single `Player` is created there and stored in the `player` variable. Inside the loop, `player.draw(screen)` sits between `screen.fill("black")` and `pygame.display.flip()`, so each frame is: wipe the screen, draw the player, then show the result. (Drawing before the fill would just get painted over by the black.)
- **13/11/2026 update (Moving Around):** the loop now calls `player.update(dt)` once per frame, after the events are handled and before the screen is filled and drawn. So each frame is: log the state, handle events, update the player, wipe the screen, draw the player, flip, then work out `dt` for the next frame. `dt` is finally being used, which is what it was saved for.
- **14/11/2026 update (Groups):** before the game loop, two empty sprite groups are created: `updatable = pygame.sprite.Group()` (everything that can be updated) and `drawable = pygame.sprite.Group()` (everything that can be drawn). Then `Player.containers = (updatable, drawable)` is set, and only *after* that is the `Player` created. That order matters: the class has to know its groups before any `Player` object exists, otherwise the player is created without joining either group and nothing gets updated or drawn. The loop no longer calls `player.update(dt)` and `player.draw(screen)` directly. Instead each frame is now: log the state, handle events, `updatable.update(dt)`, wipe the screen, `for thing in drawable: thing.draw(screen)`, then flip and work out `dt`. The `flip()` sits outside the `for` loop so it runs once per frame, not once per object. The point of all this is that the loop doesn't need to know about each individual object: any future object (asteroids, shots) just joins the right groups and gets updated/drawn automatically.
- **Groups can overlap:** an object can be in several groups at once. The player is in both `updatable` and `drawable`, whereas some later objects (like the asteroid field) will only need updating, so they'll be in `updatable` only.
- **14/11/2026 update (Asteroids):** a third group, `asteroids`, is created next to `updatable` and `drawable`, and the containers are set before anything is created: `Asteroid.containers = (asteroids, updatable, drawable)` (every asteroid joins all three groups automatically) and `AsteroidField.containers = (updatable,)` (the field only needs updating — it isn't drawn and it isn't an asteroid itself, and the trailing comma is what makes it a one-item tuple). `asteroid_field = AsteroidField()` is created after its container is set, and from then on the field spawns asteroids by itself as part of `updatable.update(dt)`, so nothing in the game loop had to change for them to appear and move.
- **14/11/2026 update (Collisions):** right after `updatable.update(dt)`, the loop checks every asteroid in the `asteroids` group with `asteroid.collides_with(player)`. If one is touching the player, it calls `log_event("player_hit")`, prints `Game over!` and calls `sys.exit()` to end the game straight away (`sys` is imported at the top, along with `log_event` from `logger`). The check happens before the drawing, so the frame of the collision never gets drawn.
- **15/11/2026 update (Collisions placement):** after the Collisions code had to be put back (see Troubleshooting Notes), the collision loop currently sits *after* `pygame.display.flip()` rather than right after `updatable.update(dt)`. It behaves the same for the game and the lesson (touching an asteroid logs `player_hit`, prints `Game over!` and exits), the only difference being that the frame where the collision happens is drawn once before the game ends.
- **15/11/2026 update (Shooting):** a fourth group, `shots`, is created with the other three before the game loop, and `Shot.containers = (shots, drawable, updatable)` is set with the other `containers` lines (before anything is created). Every bullet the player fires joins those three groups automatically, so the loop didn't need any other changes for bullets to be updated and drawn. The group has to be called `shots` because the Boot.dev test reads that name from `game_state.jsonl`.

**constants.py**
- `SCREEN_WIDTH` — the game window's width in pixels (1280)
- `SCREEN_HEIGHT` — the game window's height in pixels (720)
- **07/11/2026 update:** `PLAYER_RADIUS` (20) — the radius of the player's hitbox circle, and `LINE_WIDTH` (2) — the thickness of the lines used to draw the player's ship
- **13/11/2026 update:** `PLAYER_TURN_SPEED` (300) — how fast the player rotates, in degrees per second
- **13/11/2026 update:** `PLAYER_SPEED` (200) — how fast the player moves, in pixels per second
- **14/11/2026 update:** `ASTEROID_MIN_RADIUS` (20) — the radius of the smallest asteroid, `ASTEROID_KINDS` (3) — how many asteroid sizes there are, `ASTEROID_SPAWN_RATE_SECONDS` (0.8) — how often a new asteroid spawns, and `ASTEROID_MAX_RADIUS` — worked out as `ASTEROID_MIN_RADIUS * ASTEROID_KINDS` (60), the radius of the biggest asteroid
- **15/11/2026 update:** `SHOT_RADIUS` (5) — the radius of a bullet, and `PLAYER_SHOOT_SPEED` (500) — how fast bullets travel, in pixels per second

**logger.py**
- Provided logging utility (not written from scratch, was instead given to us in BootDev Chapter 2 Lesson 2) that snapshots the game's local state at about once per second & writes it to `game_state.jsonl`, so that the game behaviour is able to be verified without the need to manually inspect the running window
- **14/11/2026 update:** `log_event` (also provided) is used for one-off events, such as `log_event("player_hit")` when the ship hits an asteroid. These are written to `game_events.jsonl`, which was added to `.gitignore` so it doesn't get committed (it's a generated file, like `game_state.jsonl`).

**circleshape.py** (added 01/10/2026)
- Provided base class from BootDev Chapter 3 Lesson 1 (pasted in, not written from scratch). `CircleShape` inherits from `pygame.sprite.Sprite`, meaning it starts with everything `Sprite` already has and adds game-specific attributes on top. Other game objects (the player, later the asteroids) are built on top of it so the shared parts are only written once.
- `__init__(x, y, radius)` stores three attributes: `position` (a `pygame.Vector2` of x and y), `velocity` (a `Vector2` starting at `(0, 0)`, i.e. not moving) and `radius`.
- Inside `__init__`, `hasattr(self, "containers")` checks whether any sprite groups have been set up; if so, `super().__init__(*self.containers)` adds the object to them automatically, otherwise plain `super().__init__()` is used. The groups aren't used yet, they're for later.
- `draw(screen)` and `update(dt)` are empty placeholders (`pass`) marked "must override": each child class provides its own version, since a ship and an asteroid will draw and update differently.
- **14/11/2026 update:** the groups are now being used. Because `Player.containers = (updatable, drawable)` is set before the player is created, the `hasattr(self, "containers")` check finds it, and `super().__init__(*self.containers)` adds the new player to both groups automatically. `circleshape.py` itself didn't need any changes.
- **14/11/2026 update (Collisions):** `collides_with(other)` was added. It gets the distance between the two shapes' centres with `self.position.distance_to(other.position)` and returns `True` if that distance is less than or equal to the two radii added together (`self.radius + other.radius`), otherwise `False`. Everything is treated as a circle for collisions, including the triangular ship, which keeps the maths simple. It lives on `CircleShape` because everything that can collide inherits from it.

**player.py** (added 07/11/2026)
- `Player` inherits from `CircleShape`. Its constructor takes `x` and `y`, passes `x`, `y` and `PLAYER_RADIUS` up to `CircleShape` with `super().__init__(...)`, and sets `self.rotation = 0`. The radius isn't an input because it's always the same constant.
- `triangle()` (provided by Boot.dev) works out the three corner points of a triangle from the player's position, radius and rotation. The ship is drawn as a triangle, but its hitbox is a circle.
- `draw(screen)` overrides `CircleShape.draw` and calls `pygame.draw.polygon(screen, "white", self.triangle(), LINE_WIDTH)`.
- `rotation` has to be stored as an attribute (`self.rotation`) rather than a plain variable, otherwise `triangle()` couldn't read it later.
- **13/11/2026 update:** `rotate(dt)` adds `PLAYER_TURN_SPEED * dt` to `self.rotation`. Multiplying by `dt` means the ship turns by an amount based on how much time passed since the last frame, so it spins at the same speed (about 300 degrees per second) however fast the computer runs.
- **13/11/2026 update:** `update(dt)` overrides `CircleShape.update`. It uses `pygame.key.get_pressed()` to see which keys are currently held down: `A` calls `self.rotate(-dt)` and `D` calls `self.rotate(dt)`. Passing a negative `dt` reverses the direction, which is how `A` turns the ship left while `D` turns it right.
- **13/11/2026 update (movement):** `move(dt)` works in four steps. (1) Start with a unit vector pointing straight down, `pygame.Vector2(0, 1)`. (2) Rotate it by the player's `rotation` so it points the same way the ship does (`unit_vector.rotate(...)` returns a *new* vector rather than changing the original, hence it's saved into `rotated_vector`). (3) Multiply it by `PLAYER_SPEED * dt` so its length is how far the ship should travel this frame. (4) Add that vector to `self.position`. `update` now also calls `self.move(dt)` when `W` is held and `self.move(-dt)` when `S` is held, so negative `dt` makes the ship go backward, the same trick as the rotation keys.
- **15/11/2026 update (shooting):** `shoot()` creates a new `Shot` at the player's current position (`Shot(self.position.x, self.position.y)`) and sets its `velocity` the same way `move` works out a direction: start with `pygame.Vector2(0, 1)`, rotate it by `self.rotation` so it points the way the ship is facing, then multiply it by `PLAYER_SHOOT_SPEED` to make it travel fast. `update` also checks `pygame.K_SPACE` and calls `self.shoot()`. `Shot` and `PLAYER_SHOOT_SPEED` have to be imported at the top of `player.py`. A missing import only causes a crash the first time the spacebar is pressed, not when the game starts.

**asteroid.py** (added 14/11/2026)
- `Asteroid` inherits from `CircleShape`, the same way `Player` does. Its constructor takes `x`, `y` and `radius` and passes all three up with `super().__init__(x, y, radius)`.
- `draw(screen)` overrides `CircleShape.draw` and draws a white circle outline with `pygame.draw.circle(screen, "white", self.position, self.radius, LINE_WIDTH)`. The circle you see is also the hitbox, so what you see is what collides.
- `update(dt)` overrides `CircleShape.update` with `self.position += self.velocity * dt`, so the asteroid moves in a straight line at a constant speed (and, like the player, scaled by `dt`). A new asteroid's `velocity` starts at `(0, 0)`, and the `AsteroidField` gives it a real velocity when it spawns it.

**asteroidfield.py** (added 14/11/2026)
- Provided by Boot.dev (pasted in, not written from scratch). `AsteroidField` is itself a sprite, but it never draws anything, it just keeps a timer and spawns asteroids, which is why it only goes in the `updatable` group.
- Its `update(dt)` adds `dt` to a spawn timer. Once the timer goes past `ASTEROID_SPAWN_RATE_SECONDS` (0.8), it resets and spawns a new asteroid from a random edge of the screen, with a random speed (40 to 100), a direction that's randomly turned up to 30 degrees either way, and a random size (`ASTEROID_MIN_RADIUS * kind`, where `kind` is 1 to `ASTEROID_KINDS`).
- `spawn(radius, position, velocity)` creates the `Asteroid` and gives it its velocity. Because `Asteroid.containers` was set earlier, every spawned asteroid joins the `asteroids`, `updatable` and `drawable` groups on its own.

**shot.py** (added 15/11/2026)
- `Shot` (a bullet) inherits from `CircleShape`, like `Asteroid`. Its constructor only takes `x` and `y`, and passes `x`, `y` and `SHOT_RADIUS` up with `super().__init__(...)`, because every bullet is the same size.
- `draw(screen)` and `update(dt)` are written the same way as the asteroid's: a white circle outline of the shot's radius, and `self.position += self.velocity * dt` for straight-line movement at a constant speed. The `velocity` isn't set in `Shot` itself, `Player.shoot()` sets it after creating the shot, which is what makes bullets go the way the ship faces.
- Bullets are never removed yet, so they keep flying off the screen forever (a problem for a later lesson).

## Troubleshooting Notes

- **27/09/2026 — Backwards import syntax**: Wrote `import from constants import SCREEN_WIDTH` instead of `from constants import SCREEN_WIDTH`. Python's `from X import Y` order is fixed — `from` always comes before the module name, `import` always comes before the names being pulled in. Fixed by rewriting the line in the correct order.

- **27/09/2026 — Typo in imported name**: Wrote `SREEN_WIDTH` instead of `SCREEN_WIDTH` when importing, which doesn't match the variable actually defined in `constants.py`. Lesson: imported names must match the source file's spelling exactly — Python won't auto-correct typos.

- **27/09/2026 — `ModuleNotFoundError: No module named 'pygame'`**: Ran the script with plain `python3 main.py`, which uses the system Python rather than the project's virtual environment where pygame was actually installed. Fixed by running it through `uv run main.py` instead, which automatically uses the project's own `.venv`.

- **27/09/2026 — Missing `.gitignore`**: The lesson said `uv init` would auto-create a `.gitignore`, but it wasn't present after setup. Also got confused between two different `.gitignore` files — one auto-generated later inside `.venv/` (governs pygame/venv internals only) and the actual project-level one next to `main.py` (created manually with `touch .gitignore`, and the one that matters for git tracking). Lesson: check *which* `.gitignore` you're editing when a project has more than one.

- **30/09/2026 — `Failed to spawn main.py: No such file or directory`**: Ran `uv run main.py` from the outer `Asteroids-Project` folder, but `main.py` lives inside a nested folder, so the terminal couldn't find it. Fixed by using `pwd` and `ls` to see where I was, then `cd`-ing into the folder that contains `main.py`. Lesson: the terminal only looks in the folder it's standing in.

- **07/11/2026 — Merge conflict in `player.py`**: Half-finished Chapter 3 Lesson 2 work had been committed straight onto `main` instead of the lesson branch, so merging the `Draw-Player` branch into `main` conflicted in `player.py` (git marks the two competing versions with `<<<<<<<`, `=======` and `>>>>>>>` lines inside the file). Fixed by keeping the incoming `Draw-Player` version (the finished one) in the editor and checking that no marker lines were left in the file. Afterwards `git status` still showed `player.py` as modified, meaning the cleaned-up version hadn't been committed yet and the committed merge still had leftover junk in it, so it needed its own commit and push. Lesson: a conflict isn't resolved until the clean file is committed, and unfinished lesson work should stay on its own branch rather than `main`.

- **14/11/2026 — `ModuleNotFoundError: No module named 'asteroid'`**: Saved the new class in a file called `asteroids.py` (with an "s"), but the lesson's `asteroidfield.py` does `from asteroid import Asteroid`. Python imports by *file name*, so it couldn't find a module called `asteroid`. Changing the import in `main.py` to match the wrong file name only fixed one of the two files that import it. Fixed by renaming the file to `asteroid.py` (as the lesson says) and putting the import in `main.py` back. Lesson: when provided code imports a module by a certain name, the file has to be named exactly that.

- **15/11/2026 — Collisions code went missing, so hitting an asteroid did nothing**: While working on the Shooting lesson, flying into an asteroid stopped ending the game, with no error message at all. The Collisions code (the collision loop and the `sys`/`log_event` imports in `main.py`, and the `collides_with` method in `circleshape.py`) was no longer in the Shooting branch, most likely because the Collisions branch hadn't been merged into `main` before the Shooting branch was started. The Boot.dev submit for Shooting also failed until it was put back. Fixed by re-adding the collision loop and imports to `main.py`; the first run after that then crashed with `AttributeError: 'Asteroid' object has no attribute 'collides_with'`, which is what showed `collides_with` was missing from `circleshape.py` too, so that was added back as well. Lesson: merge each finished lesson into `main` (and check with `git branch --merged main`) before starting the next lesson's branch, so nothing gets left behind.

## Other Mentions

- **27/09/2026** — Learning Git/source control alongside this project — using VS Code's Source Control panel (stage → commit → push) rather than the terminal for most git operations, with terminal used mainly for running/testing the code via `uv`.

- **30/09/2026** — Started using a separate git branch for each lesson (`gameLoop` for this one) so mistakes never touch `main`. Committed and pushed the branch, then merged it into `main` from the terminal (`git checkout main`, `git merge gameLoop`, `git push origin main`). The branch was kept afterwards to preserve history. I started to do this as I learnt from my bookbot mistakes

- **07/11/2026** — Came back to the project after a break in the middle of Chapter 3 Lesson 2 (Draw Player). I carried on from the existing `Draw-Player` branch, finished the lesson there, then merged it into `main`, which led to my first merge conflict (see Troubleshooting Notes). Both branches were kept for history.

- **14/11/2026** — The branch for the Asteroids lesson was named `Asteroid's`. The apostrophe means the name has to be wrapped in double quotes in terminal commands (`git push -u origin "Asteroid's"`, `git merge "Asteroid's"`), otherwise zsh thinks a quote has been opened and waits for it to be closed. Simple branch names (no apostrophes or brackets) are easier.