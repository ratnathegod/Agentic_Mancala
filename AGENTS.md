# Project instructions for Codex

## Scope and authoritative material

- This is an individual CSCI 3202 Fall 2026 project, Option 2: Mancala AI.
- The three official PDFs in local `docs/` are the source of truth. Read all three
  before changing game behavior or interpreting project requirements.
- PDFs are intentionally local and ignored by `docs/*.pdf` because GitHub is public.
  Never force-add or publish them. If missing in a fresh clone, explain which
  authorized copies are needed; never fabricate placeholder PDFs.
- Preserve the instructor's rules exactly. Where the example diagram conflicts
  with the explicit course rules and matching HW 6 tests, follow the latter and
  document the discrepancy. Do not silently change or rewrite the source documents.
- `Mancala_Project.ipynb` is the development and submission notebook.
- Do not modify `reference/Homework_6_Lastname_Firstname.ipynb`. Preserve its
  original bytes, provided interfaces, and attribution. The reference is starter
  material, not the final deliverable.

## Game correctness

- Preserve the configurable board representation, constructor, display method,
  1-indexed pit interface, move history, and `current_player` semantics.
- Sow counter-clockwise, skip the opponent's mancala, and include the mover's.
- Support the continuation rule, including consecutive extra moves. A move that
  ends the game grants no extra turn.
- Capture the final stone in an empty own pit together with opposite stones;
  capture the landing stone even if the opposite pit is empty.
- End the game when either side's pits are empty and sweep remaining stones into
  their owner's mancala. Compare mancala totals for wins and ties.
- `winning_eval()` must return a bool; it does not return a winner identifier.
- Preserve the ordered checks in `play`: game over before invalid move. Invalid
  moves do not change the board, player, or history.
- Preserve the required HW 6 Part 3 test cell unchanged in the project notebook.
  Fix implementations when tests fail; do not weaken or edit the eight tests.

## Required AI search conventions

- The final project requires both minimax and Alpha-Beta, each with configurable
  depth and equivalent behavior to `minimax_player(game, state, d)` and
  `alpha_beta_player(game, state, d)`, returning a pit numbered 1–6.
- Both algorithms must account for consecutive moves by the same player. Determine
  MAX/MIN from whose turn it is in each state relative to the root AI; never assume
  that the players alternate at every recursion level.
- Count depth exactly as the instructor specifies: the AI's candidate moves lead
  to depth 1, each further move adds 1, and cutoff occurs at depth > d. A depth d
  search therefore looks up to d + 1 moves ahead. Count continuation moves too.
- Use utility = AI mancala stones minus opponent mancala stones for all required
  results, evaluated at game-over or cutoff nodes.
- Examine legal pits in ascending order and keep the first best move on ties
  (lowest pit number). Alpha-Beta must select the same pit as minimax at the same
  state and depth. Any future optimization must preserve this behavior.
- Retain the course continuation positions A/B/C, expected pits 5/6/6 at depths
  1/2/2, as future verification requirements for both algorithms.

## Experiments and implementation practices

- Never invent results or claim unexecuted tests passed. Distinguish instructor
  expected outputs and reference statistics from observed project results.
- Count game length as individual moves, including extra-turn moves. Exclude
  game-ending moves from continuation counts and disclose the convention.
- Use reproducible seeds; retain the starter seed 109 unless a documented
  experiment intentionally uses a different seed.
- Keep implementations readable and explainable during the grading interview.
- Prefer minimal dependencies and straightforward Python. Add dependencies only
  when the project actually uses them.
- Prioritize correctness before performance optimization. Required work and
  optional speed-challenge requirements are documented in README.md.

## Repository safety and current task boundary

- Preserve local changes and remote history. Do not force-push, hard-reset,
  discard local changes, or overwrite existing work. Stop and explain any
  consolidation conflict that cannot be resolved safely.
- Do not commit or push without the user's approval.
- The currently authorized task is repository setup and validation only. Leave
  gameplay/random-player stubs unchanged, do not implement search, and do not run
  gameplay tests or experiments during setup. Further implementation requires a
  new user instruction.
