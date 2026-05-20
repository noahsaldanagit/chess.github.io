# Standard Chess with CSS Promotion Modal

A lightweight, browser-based chess game built entirely with vanilla **HTML5**, **CSS3**, and **JavaScript**. This project renders an interactive 8x8 chess board, handles path-clearing and basic movement rules, detects check/checkmate/stalemate scenarios, and features a responsive modal UI for pawn promotion.

---

## 🚀 Features

* **Vanilla Implementation:** Zero external frameworks, dependencies, or asset images.
* **Visual Highlights:** Active pieces and their valid destination squares are dynamically highlighted upon selection.
* **Pawn Promotion Modal:** A custom CSS overlay breaks out of standard play when a pawn reaches its respective back rank, freezing the board until a piece upgrade is chosen.
* **Game State Engine:** Out-of-the-box support for:
    * Turn-based execution (`white` vs `black`).
    * Geometric movement logic (Rooks, Knights, Bishops, Queens, Kings, and Pawns).
    * Check, Checkmate, and Stalemate validation checks.

---

## 🛠️ Code Architecture

### 1. State Management
The application manages game state using standard JavaScript variables and a 2D matrix array:

| Variable | Type | Description |
| :--- | :--- | :--- |
| `board` | `Array[][]` | An 8x8 matrix storing raw Unicode characters for pieces, or `''` for empty squares. |
| `turn` | `String` | Tracks the active player color (`'white'` or `'black'`). |
| `selectedPiece` | `Object` \| `null` | Holds coordinate state `{ row, col }` of the currently selected piece. |
| `pendingPromotion` | `Object` \| `null` | Tracks `{ row, col }` during a promotion selector state to freeze interactions. |
| `gameOver` | `Boolean` | Flag that locks out all click handlers once a game-ending condition is reached. |

### 2. Core Validation Pipeline
* **`isValidMove()`**: Governs the theoretical geometric rules for individual pieces (e.g., L-shapes for Knights, diagonals for Bishops).
* **`isPathClear()`**: Ensures linear and diagonal pieces (Rooks, Bishops, Queens) cannot leap over obstructing pieces.
* **`isInCheck()`**: Scans the board configuration, uncovers the targeted color's King location, and verifies if any enemy line-of-sight compromises that square.
* **`isLegalMove()`**: Deep-clones the active board state using `currentBoard.map(row => [...row])`, simulates the desired move on the clone, and checks if the player's own King is left exposed. If exposed, the move is rejected.

---

## 🎨 UI & Styling Highlights

* **Board Construction:** Built using **CSS Grid Layout** (`grid-template-columns: repeat(8, 70px)`) keeping the 64 squares completely structured without structural drift.
* **Asset-Free Pieces:** Uses high-fidelity Unicode vectors (`♕`, `♜`, `♙`) embedded directly as text layers, styled with drop shadows (`text-shadow`) to give contrast against the wood-grain inspired board themes.
* **Modal Interception:** The promotion system leverages a high `z-index` overlay paired with a `position: fixed` layer. It safely handles state transitions by changing `display: none` to `display: flex` using DOM style alterations.

---

## 🏁 How to Run

1. Save the codebase into a file named `index.html`.
2. Open `index.html` directly inside any modern web browser (Chrome, Safari, Firefox, Edge).
3. Play begins immediately. **White moves first.**
