# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

番茄钟 (Pomodoro Timer) — a single-file timer app built with vanilla HTML/CSS/JS. No build tools, no dependencies, no package manager.

## Running the app

Open `index.html` directly in a browser. No server or build step required.

## Architecture

All code lives in `index.html`:

- **CSS (`<style>` in `<head>`):** CSS custom properties define the color scheme (`--focus` orange, `--break` green), backdrop-blur card layout, SVG progress ring, and responsive breakpoint at 480px.
- **HTML:** A `.card` wraps a state badge, SVG progress ring with centered time display, three buttons (toggle/reset/skip), and a completed-pomodoro counter with dot indicators.
- **JS (`<script>` at end of `<body>`):** State machine managing two modes — `focus` (25 min) and `break` (5 min). The timer auto-advances: focus completes → play sound → switch to break → auto-start; break completes → play sound → switch to focus → auto-start.

## Key JS constants and state

- `SETTINGS.focus = 25 * 60` (1500s), `SETTINGS.break = 5 * 60` (300s)
- `CIRCUMFERENCE = 2 * Math.PI * 44` — matches the SVG circle's `r="44"`
- State variables: `state` (`'focus'`|`'break'`), `timeLeft`, `totalTime`, `isRunning`, `pomodoroCount`
- Timer ticks via `setInterval(tick, 1000)`

## Keyboard shortcuts

| Key | Action |
|-----|--------|
| `Space` | Start / pause |
| `R` | Reset current timer |
| `S` | Skip current phase |
