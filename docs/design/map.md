# gzcontractor design map

Status: open fog, 2026-11-26. Resolve these before writing the first design
spec. Each ticket is HITL (only the owner can settle it, in a live session) or
AFK (an agent can research it and report back). An agent never answers a HITL
ticket on the owner's behalf.

Process: resolve tickets in direct sessions in this repository, using
Superpowers brainstorming. Record each lasting choice as an ADR in
`docs/adr/`, then write one design spec. Define ports in `docs/ports/` only
after the owner approves that spec.

## Settled inputs

- Layer 3 has its own repository and hexagon (ADR 0001).
- The owner sets goals. gzcontractor never sets its own objectives.
- Strict hexagonal, in a spirit of strictness: exceptions are recorded as
  named departures with reasons.
- A model's output is a proposal. Completion needs external acceptance
  evidence; missing evidence means incomplete, never success.
- gzcontractor picks AFK tickets only. Unattended work defaults to
  diagnosis-only unless the owner approves otherwise (gzkit ADR-0.0.62).
- Prefect and Pydantic AI are one implementation strategy for the lower
  layers, kept behind ports so they can be replaced.

## Tickets

| ID | Question | Mode | Blocks |
| --- | --- | --- | --- |
| C1 | Model direction: inside our own loops, is the model only a driven actor whose tool calls come back as proposals, with the model a driving actor only when an outside agent calls our MCP server? | HITL | Port shapes in every layer |
| C2 | Memory ownership: who owns admission rules for lessons, by layer (run lessons in gzfactory, cross-mission lessons here) or a separate memory context both call? | HITL | Memory ports |
| C3 | Mission contents: goal, acceptance owner, acceptance probe, budgets, allowed tickets | HITL, after A1 | gz-cartridge T7 |
| C4 | Starting autonomy: level 1 (proposes, owner acts), and how a given action is promoted or demoted | HITL | Approval port |
| C5 | Ticket sources: gzkit tickets, GitHub issues, gz-starter projects; which first | HITL | Ticket-source port |
| C6 | Engines behind "submit run": gzfactory first; gzkit routines as a second adapter? | HITL | Factory port |
| C7 | What drives gzcontractor itself: a CLI, a schedule, a workflow engine as a driving adapter | HITL, after Montenegro ch 13 | Driving adapters |
| C8 | What "strict" covers across repos: gzkit's kernel choices (frozen Pydantic, buses) or only structure | HITL, shared with gz-starter | Kernel dependency |
| A1 | Read Huang ch 8 and 9 (collaboration and governance patterns); propose a starting topology and autonomy controls | AFK | C3, C4 |
| A2 | Map gzkit's HITL/AFK ticket model and ADR-0.0.62 Routine port onto gzcontractor's inputs | AFK | C5, C6 |
| A3 | Draft the port list (input and output) as a proposal for owner review | AFK, after C1 | `docs/ports/` |

## Sources

- Project doc "Designing AI Agents under strict hexagonal" (2026-11-26).
- Project doc "AI Agents in Action vs gzfactory and gzyoke".
- gz-cartridge `docs/design/map.md` (T7 depends on C3).
