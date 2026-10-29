# Agentic_Mancala

Individual CSCI 3202 Artificial Intelligence course project, Fall 2026, CU Boulder.
Project option: **Option 2 — Mancala AI**.
Repository: <https://github.com/ratnathegod/Agentic_Mancala>.

The project will build the instructor's version of Mancala, validate its rules,
and compare random, minimax, and Alpha-Beta players. Correct continuation turns,
reproducible experiments, and an explainable notebook are central objectives.

## Current status

Repository setup is complete. The instructor's HW 6 notebook is preserved unchanged
in `reference/`. `Mancala_Project.ipynb` contains the provided representation,
constructor, display method, examples, eight rule tests, and development sections.

`valid_move`, `random_move_generator`, `play`, and `winning_eval` remain unfinished.
No gameplay or AI algorithms have been implemented during setup. Notebook code,
rule tests, and experiments have not been executed; no measured results are claimed.

## Repository structure

```text
Agentic_Mancala/
├── README.md
├── AGENTS.md
├── .gitignore
├── requirements.txt
├── docs/                         # Local course PDFs; ignored by Git
│   ├── CSCI_3202_Course_Project_Fall_2026.pdf
│   ├── CSCI 3202 Project Intermediate Report.pdf
│   └── Example Mancala Game.pdf
├── reference/
│   └── Homework_6_Lastname_Firstname.ipynb
├── Mancala_Project.ipynb
└── results/
    └── .gitkeep
```

## Setup and notebook use

Use Python 3.12 or newer. The starter notebook records Python 3.12.12.

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m jupyterlab Mancala_Project.ipynb
```

Select the Python kernel from the virtual environment. JupyterLab is the sole
direct dependency; it supplies notebook tooling, `nbformat` validation, and
`ipykernel` through its dependencies. The starter code imports only standard-library
`random`, seeded with `109`. Additional scientific or AIMA packages are not yet needed.

Develop in `Mancala_Project.ipynb`; leave the reference notebook unchanged. The
development notebook is currently a scaffold: running its rule-test cell now will
exercise unfinished methods. Once the game is implemented, restart the kernel,
run cells in order, inspect the examples and rule tests, and only then run experiments.

The course PDFs are kept locally and excluded by `docs/*.pdf` because this repository
is public. A fresh clone will not include them. Place your authorized copies, with
the filenames above, in `docs/`. Do not force-add them to Git.

## Rules and search requirements

The three PDFs in `docs/` are the course specifications. Follow the explicit course
rule list and the matching HW 6 tests when interpreting the older example diagram:

- Sow counter-clockwise, including your own mancala and skipping your opponent's.
- A final stone in your own mancala earns another move unless the game has ended.
- A final stone in an empty own pit is captured along with opposite stones; even
  when the opposite pit is empty, capture the landing stone.
- Empty pits on either side end the game; sweep the remaining stones to their
  owner's mancala. Compare mancala totals to determine the winner or tie.

The example PDF has discrepancies: it alternates players after P2's pit-2 move
lands in P2's mancala, and its final totals are 15 stones despite starting with 12.
Preserve the document as supplied; do not use these diagrams to override the
explicit rules or edit the instructor's tests to match them.

Minimax will evaluate legal choices recursively. Alpha-Beta will prune branches
that cannot change the selected move while returning the same pit as minimax for
the same state and depth. Future interfaces are
`minimax_player(game, state, d)` and `alpha_beta_player(game, state, d)`
(or equivalent class methods), returning a 1-indexed pit.

For both algorithms:

- Use utility = stones in the AI's mancala minus stones in its opponent's mancala,
  evaluated at game-over or depth-cutoff nodes.
- Choose MAX or MIN from the player to move in each state, allowing consecutive
  MAX or MIN nodes when a player earns another turn.
- Candidate children start at depth 1; cut off when depth **> d**. Thus `d=2`
  examines up to three moves ahead. Every move counts, including continuation moves.
- Consider pits in ascending order; keep the first best move on equal utility.

## Intermediate report — October 30, 2026, 11:59 PM

Required work, still pending:

- Complete all game rules and the random legal-move player, including HW 6 play examples.
- Pass all eight unchanged instructor rule tests.
- Run 100 random-vs-random games without errors, with reproducible random seeding.
- Report each player's wins, losses, and ties as counts and percentages.
- Report average game length and average continuation count; analyze first-player
  advantage and compare with the course reference ranges.
- Submit current code and a brief report through Canvas, with libraries/frameworks
  and actual test results. Use the project notebook for code and report; explain
  unfinished or failing work honestly.

Count game length as individual pit-selection/sowing moves, including continuation
moves. A continuation is an earned extra move; exclude game-ending moves from that
count and state this convention in the report. If reporting player handoffs, label
them separately rather than calling them moves.

The course's random-game reference values are approximately P1 wins 48%, P2 wins
45%, ties 6% (rounded), 40.3 moves, and 5.5 continuations per game. Typical 100-game
ranges are P1 wins 38–58%, P2 wins 36–55%, ties 3–12%, mean moves 38.5–42, and
mean continuations 4.5–6.5. These are reference statistics, not project results or
deterministic pass/fail thresholds. A 100-game sample can favor Player 2.

## Final project — November 13, 2026

Required work, still pending:

- Implement minimax and Alpha-Beta with configurable depth and the conventions above.
- Run 100 games for each configuration: random vs. minimax at `d=2` and `d=5`,
  and random vs. Alpha-Beta at `d=5` and `d=10`.
- Report win rates, average game length, timing per game for Alpha-Beta, and
  analysis of strength as depth increases.
- Compare minimax and Alpha-Beta runtime at `d=5`; project minimax runtime at `d=10`.
- Plot AI win percentage at depths 2, 5, and 10 and explain the observed pattern.
- Include the continuation verification: eight HW 6 tests, the random-game
  continuation statistic and counting convention, and both algorithms' chosen pits
  for course positions A, B, and C (expected pits 5, 6, and 6 at depths 1, 2, and 2).
- Explain the continuation-related search changes and finish the final conclusions.
- Submit the code/writeup notebook and be prepared to explain and demonstrate it
  during a 15-minute grading interview. Final grading includes results/analysis
  (50 points), continuation checks (20), and interview (30).

Interview signup opens around November 9. Interview windows are November 16–20
and November 30–December 4, with no interviews during fall break November 23–27.

## Optional Alpha-Beta speed challenge — 20 points

Run 100 games against random at `d=10` (up to 11 moves ahead) in **under 20 minutes
total**, with at least 95% AI wins and all continuation checks passing. Measure the
complete run with `time.perf_counter()`, report processor and memory, explain the
optimizations, and be ready to demonstrate a shorter run (for example, 10 games)
during the interview. Optimize only after correctness is established.

## Next implementation task

After separate authorization, complete the four unfinished game/random-player
methods, then run the instructor's small-board example and eight rule tests.
Simulations and AI development follow only after the game is validated.
