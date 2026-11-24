[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/lsummi27-ui/chess-engine-4kb/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/lsummi27-ui/chess-engine-4kb/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
<sub>Entered on [make.fun](https://make.fun/?ref=7yd20ms9&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>

# Tiny Chess Engine (4 KB)

A compact, original chess engine in a single `main.py` (<= 4,096 bytes).
0x88 board, alpha-beta search with a transposition table, quiescence search
over captures and promotions, MVV-LVA move ordering, and a piece-square
evaluation. Deterministic: a fixed node budget per move, no wall clock, no
unseeded randomness. The source is stored lzma-compressed (base85) inside
`main.py` and unpacked at startup; the unpacker plus payload count toward
the 4,096-byte limit.

## Design

- Board: 0x88 (128 squares), piece lists for fast move generation.
- Search: iterative deepening alpha-beta with a transposition table,
  null-move pruning, and quiescence over captures, promotions, and
  check evasions.
- Evaluation: material plus standard piece-square tables (single phase).
- Budget: 400,000 nodes per move (fixed, deterministic). No clock is used.

## Practice

Tested locally against the kit's practice trials (6 games each) with the
official scorer. The engine plays the full gauntlet (depth-2 through
nodes-500k) and reports wins, draws, and losses to stderr when run
interactively.

## Usage

Run against the make.fun environment:

```
python3 main.py
```

It reads `MAKEFUN_ENV_URL` and `MAKEFUN_PROMPT_FILE`, plays the gauntlet
through the env HTTP protocol, and exits when the trial is done.

## License

MIT. See `LICENSE`.
