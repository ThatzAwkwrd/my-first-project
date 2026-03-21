# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-file browser-based Tic Tac Toe game. No build tools, no dependencies, no server — open `tictactoe.html` directly in a browser.

## Architecture

Everything lives in `tictactoe.html`: inline CSS in `<style>`, markup in `<body>`, and vanilla JavaScript in `<script>`. There is no bundler, framework, or package manager.

**Game state** (all in-memory, resets on page reload):
- `board` — 9-element array of `''`, `'X'`, or `'O'`
- `current` — whose turn it is (`'X'` or `'O'`)
- `over` — boolean, prevents moves after game ends
- `scores` — `{X, O, D}` object persisted across rounds within the same session

**Win detection** uses a hardcoded `WINS` constant (8 possible lines). `checkWin()` returns the winning triple or `null`.

**DOM structure**: `.cell[data-i]` elements are indexed 0–8. Clicks are handled by per-cell event listeners attached at load time. The `init()` function resets board state and DOM classes without re-attaching listeners.

## Git Workflow

- **After every meaningful unit of work, commit and push to GitHub immediately.** This ensures no progress is ever lost and the remote always reflects the current state.
- Stage specific files by name (not `git add .`) to avoid accidentally committing secrets or binaries.
- Write commit messages that describe *why* the change was made, not just *what* changed.
- Push after every commit: `git push` — do not batch multiple commits before pushing.
- Branch off `master` for experimental changes; merge back when stable.
