# Tetris — Project Specification

## 1. Project Overview

**Name:** Tetris
**Type:** Browser-based arcade game (single HTML file)
**Variants:** Single Player (1P) and Two Player Battle (2P)
**Summary:** Classic Tetris clone with modern visual polish, plus a 2P battle mode where clearing lines sends garbage rows to your opponent.
**Target users:** Anyone who wants a quick Tetris game — solo or versus a friend.

---

## 2. Visual & Rendering Specification

### Scene Setup

**1P Mode:** Centered game board (10×20 grid) with side panel for score/next piece/controls.

**2P Mode:** Two boards side by side (P1 left, P2 right). Each board has its own side panel (score, level, lines, next). Center divider with VS indicator.

**Background:** Dark, atmospheric — deep charcoal with subtle scan-line overlay.

**Font:** JetBrains Mono (Google Fonts) — monospace, retro-tech aesthetic.

**Color palette:**
- Background: `#0d0d0d`
- Board background: `#1a1a1a`
- Grid lines: `#2a2a2a`
- Text/UI: `#e0e0e0`
- Accent: `#00ff88` (neon green for highlights)
- P1 accent: `#00f0f0` (cyan)
- P2 accent: `#f0a000` (orange)

**2P Layout:**
```
[P1 Board | P1 Panel]  VS  [P2 Panel | P2 Board]
```
Each board: 10×20 cells. Boards have matching scale, mirrored positioning around center.

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
- Ghost piece (wireframe preview of landing position)
- Line-clear flash animation
- Garbage row animation (rows rise from bottom)
- Scanline CSS overlay for retro feel
- Screen shake on big line clears (3+ lines)

---

## 3. Game Logic Specification

### Board
- 10 columns × 20 rows per player
- Standard Tetris rules (simplified SRS rotation)
- Piece spawns at top-center

### Pieces (Tetrominoes)
Standard 7: I, O, T, S, Z, J, L — each with rotation states.

### Movement
| Key (P1) | Key (P2) | Action |
|----------|----------|--------|
| ← → | Numpad 4/6 | Move horizontally |
| ↓ | Numpad 2 | Soft drop |
| ↑ | Numpad 8 / X | Rotate clockwise |
| Z | Numpad 7 | Rotate counter-clockwise |
| Space | Numpad + | Hard drop |
| P | Numpad 5 | Pause (2P: pauses both) |

### Scoring
| Action        | Points |
|---------------|--------|
| Soft drop     | 1 per cell |
| Hard drop     | 2 per cell |
| Single line   | 100 |
| Double        | 300 |
| Triple        | 500 |
| Tetris (4 lines) | 800 |

### Leveling (per player)
- Level increases every 10 lines cleared
- Drop speed: `max(100, 1000 - (level - 1) * 90)` ms per row

### Garbage Rows (2P Battle Mechanic)
When a player clears **n** lines, the opponent receives **n − 1** garbage rows (if n > 1).

- Garbage rows appear at the **bottom** of the opponent's board, pushing existing rows up.
- The top rows are removed if the board would exceed 20 rows.
- Garbage rows have a **single random gap** (one empty cell per row) to allow survival.
- Garbage rows are visually distinct: dark grey `#3a3a3a` with a subtle texture.

### Game Over
- In 1P: Game over when board is full at spawn.
- In 2P: The player whose board fills up first loses. Winner is the survivor.

---

## 4. Interaction Specification

### Controls
- **Keyboard** for both players on one machine.
- **P1:** Arrow keys + Z + Space + P
- **P2:** Numpad layout (4=left, 6=right, 2=down, 8=rotate CW, 7=rotate CCW, +=hard drop, 5=pause)

### Mode Selection
- Start screen shows: "1P" and "2P BATTLE" buttons.
- 1P: Single board, solo play, high score tracking.
- 2P: Two boards, battle mode, no AI — local 2-player.

### UI (1P)
- SCORE / LEVEL / LINES / NEXT — right panel

### UI (2P)
- P1 panel (left of P1 board): SCORE / LEVEL / LINES / NEXT
- P2 panel (right of P2 board): SCORE / LEVEL / LINES / NEXT
- Center: "VS" indicator in accent color
- Garbage incoming indicator: flashing arrow when rows are pending

### Start Screen
- Title "TETRIS" in large retro font
- "1P" button
- "2P BATTLE" button
- High score display (localStorage, 1P only)

### Pause
- All game loops pause.
- "PAUSED" overlay.
- Press P (or numpad 5) to resume.

---

## 5. Technical Specification

- **Single HTML file** — all CSS/JS inline
- **No external dependencies** except Google Fonts (JetBrains Mono)
- **Canvas rendering** — one canvas per player board, one for next-piece preview per player
- **localStorage** for 1P high score persistence
- **Responsive** — scales to fit viewport; 2P scales to ~50% width per board

---

## 6. Acceptance Criteria

### 1P
- [ ] Game board renders correctly at 10×20
- [ ] All 7 tetrominoes spawn and rotate correctly
- [ ] Collision detection prevents invalid moves
- [ ] Line clearing works and score updates
- [ ] Ghost piece shows landing position (wireframe)
- [ ] Hard drop and soft drop function
- [ ] Game over triggers when board is full
- [ ] Score, level, lines displayed and updated
- [ ] High score persists via localStorage
- [ ] Responsive layout works on different screen sizes
- [ ] Touch controls work on mobile

### 2P
- [ ] Two boards render side by side
- [ ] Each player controls their own board independently
- [ ] Clearing 2+ lines sends n-1 garbage rows to opponent
- [ ] Garbage rows appear at bottom with a random gap
- [ ] Garbage rows visually distinct (dark grey)
- [ ] Loser detected when board fills at spawn
- [ ] Winner overlay shown
- [ ] Both players' scores/levels/lines update independently
