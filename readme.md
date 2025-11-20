# 🕹️ 420-SNT-MS Object-Oriented Programming - Final Project

## Tic Tac Toe - Object-Oriented Implementation in Python (tkinter)

| Course | Instructor | Date | Group Members |
| :--- | :--- | :--- | :--- |
| 420-SNT-MS Object-Oriented Programming | Robert D. Vincent | November 27, 2025 | Jonah Rosenbloom, Ariella Guttman |

---

## ⬇️ Download

The source code for this project can be found in this repository.

---

## 📝 Introduction

This project creates a **graphical Tic Tac Toe game** using object-oriented Python and the standard **`tkinter`** GUI library. It supports both **single-player** (player vs. computer) and **two-player local multiplayer**.

The computer AI has three difficulty levels: **Easy**, **Medium**, and **Hard** (unbeatable **minimax algorithm**).

The program is structured around three main classes:
* The **`Game`** class manages the interface and user interactions.
* The **`Board`** class tracks and updates the game state.
* The **`AI`** class contains the logic used to choose computer moves.

---

## 🧑‍💻 User Guide

### Requirements

* **Python 3** (with `tkinter`, which is usually included with standard Python installations).

### Controls and Interface

* Click any empty square to place your mark.
* **Keyboard bindings:**
    * Keys `1-9` correspond to the board positions:

| 1 | 2 | 3 |
| :---: | :---: | :---: |
| 4 | 5 | 6 |
| 7 | 8 | 9 |

    * `p` - toggle multiplayer mode
    * `x` - toggle whether X starts
    * `n` or `r` - new game
    * `q` - quit
    * `Shift+1` - AI Easy
    * `Shift+2` - AI Medium
    * `Shift+3` - AI Hard

### Options and Game Modes

* **Multiplayer checkbox:** Enables two-player local mode.
* **X starts checkbox:** Selects the starting player.
* **AI difficulty dropdown:** Easy, Medium, or Hard.

> **Note:** Changing options automatically resets the board.

### Game End

* Winning lines are **highlighted** and the window title changes.
* A tie highlights all cells and displays **`Tie!`**.

---

## ⚙️ Design Guide

The program is centered on three main classes:

* **`Game`** (subclass of `tk.Tk`): Handles GUI layout, key bindings, and event handling.
* **`Board`** (subclass of `list`): A 3×3 matrix storing the game state.
* **`AI`**: Implements the logic for Easy/Medium/Hard move selection.

### Important Details

* Board coordinates use **`(row, col)`** pairs from 0–2.
* **X is encoded as 1**, **O as 0**.
* AI moves use `after(200,...)` to simulate the AI "thinking" delay.

### Algorithms

#### Easy Algorithm
The Easy level is a simple strategy: the computer chooses moves **randomly** from the available empty squares, not actively trying to win.

#### Medium Algorithm
The Medium level uses a **one-step lookahead** strategy. It checks each possible move to:
1.  See if it can **win immediately** (and take that move).
2.  **Block the opponent** if they could win on their next turn.

If neither condition applies, it chooses a random free square.

#### Hard Algorithm (Minimax)
The Hard level uses the **minimax algorithm** to play perfectly. [attachment_0](attachment)

The AI examines all possible future moves using recursion, assigning scores to each outcome (win=$1$, loss=$-1$, draw=$0$). The AI chooses the move that **maximizes its chance of winning**. On this level, the AI **cannot be defeated**.

#### Minimax Algorithm Pseudocode

```python
function minimax(board, isAI):
    if X has won, return -1
    if O has won, return 1
    if tie, return 0

    if isAI:
        for each empty cell:
            try move as AI
            score = minimax(next board, false)  # human's turn next
            undo move
        return the highest score
    else:
        for each empty cell:
            try move as human
            score = minimax(next board, true)  # AI's turn next
            undo move
        return the lowest score

function bestMove():
    for each empty cell:
        try move as AI
        score = minimax(next board, false)  # human plays next
        undo move
    choose any move with the best score  # usually multiple options with same outcome
