# gzcontractor

Layer-3 meta loop for agentic work. gzcontractor turns the owner's goals into
missions, picks the next AFK ticket, and contracts runs out to layer-2 engines
such as gzfactory. It talks to them only through ports, using gz-cartridge
records.

Status: design only. No code yet.

## Where it sits

The layers follow *AI Agents in Action*, 2nd ed. (Lanham, Manning, 2026), ch 9.

| Layer | Loop | Project | Owns |
| --- | --- | --- | --- |
| 3 | Meta loop | **gzcontractor** | Missions, choosing the next ticket, re-planning, finalising |
| 2 | Task loop | [gzfactory](https://github.com/tvproductions/gzfactory) | Workflow stages, budgets, evidence, stop rules |
| 1 | Inner loop | [gzyoke](https://github.com/tvproductions/gzyoke) or Pydantic AI | One bounded agent loop |
| All | Contract | [gz-cartridge](https://github.com/tvproductions/gz-cartridge) | The work-unit spec and the records layers exchange |

A contractor picks which "fabs" fulfil a design. The owner, not gzcontractor,
sets the goals.

## Design rules

1. **Strict hexagonal.** gzcontractor is its own hexagon. gzfactory, gzkit
   routines, ticket sources and model providers are adapters behind ports.
2. **The model proposes; the domain decides.** What is allowed, and when a
   mission is done, is decided in code from external acceptance evidence.
3. **Start small.** Begin with a deterministic picker or one agent at autonomy
   level 1 (it proposes, the owner acts). Add agents or autonomy only after
   measured evidence.
4. **AFK only.** gzcontractor may choose AFK tickets. HITL tickets wait for
   the owner.
5. **Records, not imports.** Layers exchange gz-cartridge records and never
   share domain code.

## Layout

- `docs/adr/`: decisions.
- `docs/design/map.md`: open questions, each HITL or AFK.
- `docs/ports/`: port definitions, once designed.

## Sources

- Design discussion, 2026-11-26: "Designing AI Agents under strict hexagonal"
  and "AI Agents in Action vs gzfactory and gzyoke" (project docs).
- gzkit hexagonal specification and ADR-0.0.62 (AFK work is diagnosis-only).
- Huang, *Designing AI Agents* (Manning MEAP); Montenegro, *Clean Applications
  with Hexagonal Architecture* (Manning MEAP). Cited by chapter only.
