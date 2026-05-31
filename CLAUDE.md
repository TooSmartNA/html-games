# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the games

No build step — open any `.html` file directly in a browser. Double-click the file or use `start shooter.html` / `start tictactoe.html` in the terminal.

## Repository structure

Each game is a **single self-contained HTML file** with inline CSS and JS. No dependencies, no bundler, no server required.

- `shooter.html` — Retro Swarm: top-down wave shooter on an HTML5 Canvas
- `tictactoe.html` — Tic Tac Toe: DOM-based two-player game

## shooter.html architecture

**Canvas setup:** Fixed 900×660 logical resolution. Mouse coordinates are scaled from CSS pixels to canvas pixels via `getBoundingClientRect()`.

**State machine** — four states stored in the global `state` variable:
```
S.MENU → S.PLAYING → S.SHOP → S.PLAYING → ... → S.GAME_OVER → S.MENU
```

**Data tables** drive all tunable values — edit these rather than class internals:
- `WDEFS` — weapon stats (cost, cooldown, damage, speed, pellets, spread)
- `EDEFS` — enemy stats (speed, HP, radius, damage, points)
- `PDEFS` — shop power-up definitions (cost, max level, effect description)

**Classes:** `Player`, `Bullet`, `Enemy`, `Particle`, `FloatText`, `WaveManager`. Each has `update()`, `draw()`, and an `active` boolean flag. Dead objects are filtered out each frame with `.filter(x => x.active)`.

**Game loop:** `requestAnimationFrame` → `update()` → `render()`. The global `frame` counter increments every tick and drives animations/pulses.

**Shop layout** is computed from constants (`CX0`, `CW`, `CGAP`) so all four weapon cards and four upgrade cards stay aligned automatically.

**Wave scaling:** `WaveManager.speedMult()` increases enemy speed each wave (capped at 2.2×). Enemy count = `5 + (wave - 1) * 3`. Tank/fast enemy types unlock at wave 5/3 respectively.

## tictactoe.html architecture

Pure DOM — no canvas. Board state is a 9-element array; cells are `<div>` elements with `data-i` attributes. `WINS` is a static array of all eight winning index triples. Scores persist across resets within a session (stored in the `scores` object).

## Conventions used in this repo

- All game logic lives inside `<script>` tags in the same file as the HTML — keep new features in the same file.
- Retro/synthwave dark color palette: cyan (`#00ffff`), magenta (`#cc00ff`), amber (`#ffdd00`) on near-black backgrounds.
- `ctx.shadowColor` + `ctx.shadowBlur` for neon glow effects throughout shooter.html — maintain this pattern for any new visual elements.
- shooter.html uses `'use strict'` at the top of its script block.

## Git workflow

- New repo per project, pushed to GitHub under account `TooSmartNA`.
- **Commit and push after every meaningful unit of work** — a new feature, a bug fix, a significant refactor. Never leave work uncommitted at the end of a session.
- **Always stage and commit untracked files** — run `git status` before committing and include any untracked files that belong to the project (`.html`, `.md`, `.ps1`, config files, etc.). Do not leave project files sitting untracked.
- Commit messages should describe *what changed and why*, not just what files were touched.
- Push to `origin` after every commit so GitHub always reflects the latest state. The goal is that the remote is never behind the local branch.
