# Tetris — Project Specification

## 1. Project Overview

**Name:** Tetris
**Type:** Browser-based arcade game (single HTML file)
**Summary:** Classic Tetris clone with modern visual polish, playable directly in the browser.
**Target users:** Anyone who wants a quick Tetris game.

---

## 2. Visual & Rendering Specification

### Scene Setup
- **Layout:** Centered game board (10×20 grid) with side panel for score/next piece/controls
- **Background:** Dark, atmospheric — deep charcoal with subtle scan-line overlay
- **Font:** JetBrains Mono (Google Fonts) — monospace, retro-tech aesthetic
- **Color palette:**
  - Background: `#0d0d0d`
  - Board background: `#1a1a1a`
  - Grid lines: `#2a2a2a`
  - Text/UI: `#e0e0e0`
  - Accent: `#00ff88` (neon green for highlights)

### Tetromino Colors
| Piece | Color   |
|-------|---------|
| I     | `#00f0f0` (cyan)    |
| O     | `#f0f000` (yellow)   |
| T     | `#a000f0` (purple)  |
| S     | `#00f000` (green)   |
| Z     | `#f00000` (red)     |
| J     | `#0000f0` (blue)    |
| L     | `#f0a000` (orange)  |

### Effects
- Ghost piece (transparent preview of landing position)
- Line-clear flash animation
- Subtle glow on active piece
- Scanline CSS overlay for retro feel
- Smooth piece movement (CSS transitions on board cells)

---

## 3. Game Logic Specification

### Board
- 10 columns × 20 rows
- Standard Tetris rules (SRS rotation system simplified)
- Piece spawns at top-center

### Pieces (Tetrominoes)
Standard 7: I, O, T, S, Z, J, L — each with rotation states

### Movement
- **Arrow Left/Right:** Move piece horizontally
- **Arrow Down:** Soft drop (faster fall)
- **Arrow Up / X:** Rotate clockwise
- **Z / Ctrl:** Rotate counter-clockwise
- **Space:** Hard drop (instant placement)
- **P:** Pause/Resume
- **R:** Restart (when game over)

### Scoring
| Action        | Points |
|---------------|--------|
| Soft drop     | 1 per cell |
| Hard drop     | 2 per cell |
| Single line   | 100 |
| Double        | 300 |
| Triple        | 500 |
| Tetris (4 lines) | 800 |

### Leveling
- Level increases every 10 lines cleared
- Drop speed: `max(100, 1000 - (level - 1) * 100)` ms per row

### Game Over
- Triggered when new piece cannot spawn (blocked at top)
- Display "GAME OVER" overlay with final score
- Press R or click to restart

---

## 4. Interaction Specification

### Controls
- Keyboard only (desktop)
- Touch: on-screen buttons for mobile (left, right, rotate, drop)

### UI Panel (right side)
- **SCORE** — current score
- **LEVEL** — current level
- **LINES** — total lines cleared
- **NEXT** — 4×4 preview of next piece

### Start Screen
- Title "TETRIS" in large retro font
- "Press SPACE to start" prompt
- High score display (localStorage)

### Pause
- Overlay with "PAUSED" text
- Press P to resume

---

## 5. Technical Specification

- **Single HTML file** — all CSS/JS inline
- **No external dependencies** except Google Fonts (JetBrains Mono)
- **Canvas rendering** for the game board (HTML5 Canvas 2D)
- **localStorage** for high score persistence
- **Responsive:** scales to fit viewport while maintaining aspect ratio

---

## 6. Acceptance Criteria

- [ ] Game board renders correctly at 10×20
- [ ] All 7 tetrominoes spawn and rotate correctly
- [ ] Collision detection prevents invalid moves
- [ ] Line clearing works and score updates
- [ ] Ghost piece shows landing position
- [ ] Hard drop and soft drop function
- [ ] Game over triggers when board is full
- [ ] Score, level, lines displayed and updated
- [ ] High score persists via localStorage
- [ ] Responsive layout works on different screen sizes
- [ ] Touch controls work on mobile
