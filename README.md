# 🧩 Unruly Puzzle Solver

An Artificial Intelligence solver for the logic puzzle **Unruly**, implemented as an academic project. This repository explores and compares two distinct AI problem-solving paradigms: **Systematic Search** and **Simulated Annealing** (Local Search).

## 📖 About the Game

Unruly is a grid-based logic puzzle played on an $n \times m$ board (where $n$ and $m$ are even numbers $\ge 6$). The board starts with some squares pre-colored black or white, and the rest empty. 

The goal is to fill all empty squares subject to two rules:
* **No Triplets:** No three consecutive squares can share the same color (horizontally or vertically).
* **Balance:** Every row and every column must contain an exactly equal number of black and white squares.

You can play the game online [here](http://www.chiark.greenend.org.uk/~sgtatham/puzzles/js/unruly.html).

## 🚀 Features & Algorithms

This project implements two different solvers to tackle the puzzle:

### 1. Systematic Search (Complete & Optimal)
* Formulates the puzzle as a classic search problem.
* Guarantees finding a valid solution if one exists, or conclusively proves that a puzzle is unsolvable.
* **Bonus Implementation:** Includes heuristic guidance to evaluate states and reach the solution faster with fewer node expansions.
* Outputs the exact execution time and the total number of expanded nodes.

### 2. Simulated Annealing (Stochastic Local Search)
* Initializes the board with a fully colored, random (or pseudo-random) complete state.
* Explores the state space using localized moves (swapping colors of non-fixed squares) without altering the initially provided clues.
* Utilizes a dynamic temperature cooling schedule (e.g., linear, exponential, or logarithmic) to escape local minima.
* Evaluates state quality using a custom penalty/objective function $f(s)$ that counts rule violations. A perfect solution yields $f(s) = 0$.

**Objective Function Formula:**
$$f(s) = \sum_{i=1}^{n} |rbi(s) - rwi(s)| + \sum_{j=1}^{m} |cbj(s) - cwj(s)| + \sum_{i=1}^{n} tri(s) + \sum_{j=1}^{m} trj(s)$$

*Where:*
* $rbi, rwi$: Count of black/white squares in row $i$.
* $cbj, cwj$: Count of black/white squares in column $j$.
* $tri, trj$: Count of consecutive triplets of the same color in row $i$ and column $j$.

## 📂 Input & Output Format

The solvers read puzzles from an ASCII text file containing a single line. The string encodes the board dimensions, followed by the positions of the pre-colored squares.

**Example Input:**
`8x8:bceadEDgCcAgCcabBi`

**Format Rules:**
* **Uppercase letters (`A-Z`):** Represent Black squares.
* **Lowercase letters (`a-z`):** Represent White squares.
* **Letter value:** Represents the distance from the previously colored square (e.g., `a` = 1 space, `b` = 2 spaces, `c` = 3 spaces, etc.), reading left-to-right, top-to-bottom.
* The string concludes with a lowercase letter pointing one space out of bounds $(n, m+1)$.

The program outputs the solved board to the console for verification and writes the final state to an output text file using the exact same continuous string format.
