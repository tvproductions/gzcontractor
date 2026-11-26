# ADR 0001: Layer 3 lives in its own design-first repository

Status: accepted by the owner on 2026-11-26 (decision card in the gzfactory
project's book-impact discussion). Approval of this written edition is
pending review of the pull request that adds it.

## Context

*AI Agents in Action* (2nd ed., ch 9) describes three loop layers. gzyoke is
layer 1 and gzfactory is layer 2. Layer 3, the meta loop, chooses and
sequences work across runs: the book's delegate, re-plan and finalise moves.

Layer 3's domain differs from gzfactory's. It deals in missions, goals and
the choice of the next ticket, not in workflow stages and stop rules. It must
also drive more than one layer-2 engine: gzfactory first, and possibly gzkit
routines (gzkit ADR-0.0.62). Kept inside gzfactory, layer-3 rules would leak
into layer 2.

## Decision

Create gzcontractor as its own repository and hexagon. Start design-first:
ADRs, a design map and port definitions only. Write code after the owner
approves a design spec and gzfactory's input ports exist, since those are
what gzcontractor calls.

## Consequences

- gzcontractor reaches gzfactory through a "submit run" port and reads
  outcomes through another. gzfactory is one adapter behind them.
- Records crossing layers are gz-cartridge shapes (mission, run request,
  outcome). gz-cartridge ticket T7 waits on this repository's mission design.
- The repository boundary is packaging. The hexagon boundary is what stops
  coupling, and the import-rule checker enforces it once code exists.

## Reversal

Only an explicit owner decision changes this. Folding layer 3 into another
repository would need evidence that the separate repository costs more than
the coupling it prevents.
