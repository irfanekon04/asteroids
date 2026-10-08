# Asteroids

A classic Asteroids clone built with Pygame. Pilot a triangle ship, shoot incoming asteroids, and survive as they split into smaller, faster rocks.

## Features

- Player ship with rotation, thrust, and shooting with cooldown
- Asteroid field spawning from screen edges with random speed/angle
- Asteroid splitting (large → medium → small)
- Circle-based collision detection (`CircleShape` base class)
- 60 FPS game loop with delta-time movement
- JSONL game state/event logging for debugging (`game_state.jsonl`, `game_events.jsonl`)

## Requirements

- Python 3.13
- [uv](https://docs.astral.sh/uv/) (recommended) or pip
- Pygame 2.6.1 (see `pyproject.toml`)

## Setup

```bash
uv sync
```

Or with pip:

```bash
pip install pygame==2.6.1
```

## Run

```bash
python main.py
# or
uv run main.py
```

## Controls

| Key | Action |
|-----|--------|
| `W` | Thrust forward |
| `S` | Thrust backward |
| `A` | Rotate left |
| `D` | Rotate right |
| `Space` | Shoot |
| Close window | Quit |

Game over when an asteroid hits the player.

## Project structure

```
main.py          # Game loop, groups, collision checks
player.py        # Ship rendering, movement, shooting
asteroid.py      # Asteroid rendering, movement, split()
asteroidfield.py # Edge spawning logic
circleshape.py   # CircleShape base (position, velocity, collides_with)
shot.py          # Bullet rendering/movement
constants.py     # Screen size, speeds, radii, cooldowns
logger.py        # log_state() / log_event() JSONL logger
```

## Configuration

Tweak gameplay in `constants.py`:

- `SCREEN_WIDTH`, `SCREEN_HEIGHT`
- `PLAYER_SPEED`, `PLAYER_TURN_SPEED`
- `PLAYER_SHOOT_SPEED`, `PLAYER_SHOOT_COOLDOWN_SECONDS`
- `ASTEROID_KINDS`, `ASTEROID_MIN_RADIUS`, `ASTEROID_SPAWN_RATE_SECONDS`

## Logs

`logger.py` writes `game_state.jsonl` (per-second snapshots, first 16s) and `game_events.jsonl` (`asteroid_shot`, `asteroid_split`, `player_hit`). Both files are git-ignored.
