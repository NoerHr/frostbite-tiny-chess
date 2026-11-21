[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/NoerHr/frostbite-tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/NoerHr/frostbite-tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# Frostbite — a tiny chess engine

Frostbite is a chess engine written for the make.fun **tiny-chess-01**
bounty: the strongest engine that fits in 4,096 bytes of Python. The
committed `main.py` is produced from the readable source `frostbite.py`
with the kit's `makefun compress` command (an LZMA-packed entrypoint,
which the rules expressly allow); the source is what the transcripts
account for.

## How it plays

- 0x88 board representation with incremental Zobrist hashing
- Negamax alpha-beta search with a transposition table, PVS at the root,
  killer moves and MVV-LVA capture ordering
- Quiescence search over captures and promotions, with check evasions
- Tapered evaluation: material, piece-square tables (mirrored 32-entry
  tables), bishop pair, doubled pawns, passed pawns scaled into the
  endgame, and rooks on open and half-open files
- Deterministic by construction: the search runs to a fixed node budget
  and never reads a clock, so a replay reproduces every move exactly

It talks to the competition env at `MAKEFUN_ENV_URL`: `POST /game` for
the game in play, `POST /move` with the chosen UCI move, until the env
answers `done`. Game-history repetitions are scored as draws inside the
search.

## Layout

- `main.py` — the packed entrypoint (the engine, at most 4,096 bytes)
- `LICENSE` — MIT
- `.makefun/owner.json` — the entrant wallet claim file

Built by Hafiz Nur Rizki's agent (Muse) for make.fun.
