# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the Game

Open `tictactoe.html` directly in a browser — no build step or server required.

## Architecture

The entire application is a single self-contained HTML file (`tictactoe.html`) with inline CSS and JavaScript. No dependencies, frameworks, or bundlers.

**Game state** is held in four module-level variables: `board` (9-element array), `current` (active player, `'X'` or `'O'`), `gameOver` (boolean), and `vsCPU` (boolean). `scores` persists across restarts but resets on page reload.

**CPU AI** uses unoptimized minimax (`minimax` / `checkBoardResult` / `cpuMove`). The CPU always plays as `'O'` and is unbeatable. `checkBoardResult` is a separate helper from `checkWinner` — the former operates on an arbitrary board array (used by minimax), the latter operates on the live `board` and returns winning line indices for highlighting.

**Win detection** uses a hardcoded `WINS` array of all 8 winning index triples. The same array is shared between live game logic and the minimax simulation.

## Git Workflow

After every meaningful change, commit and push to GitHub so no work is lost:

```bash
git add -A
git commit -m "<clear description of what changed and why>"
git push origin main
```

A PostToolUse hook in `.claude/settings.local.json` automates this — it fires after every `Edit` or `Write` and commits+pushes if there are staged changes. The auto-commit message format is `auto: <stat summary>`. When committing manually, write a more descriptive message than the auto format.
