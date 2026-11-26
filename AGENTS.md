# Project agent instructions

Read [AGENTS.skills-first.md](AGENTS.skills-first.md) for this project's development stack.
Add project-owned rules, verification commands, and operational skill routing here.

## Project rules

- This repository designs layer 3 (the meta loop). It is design-first: no code until the owner approves a design spec and gzfactory's input ports exist.
- Follow gzkit's hexagonal specification (`docs/governance/hexagonal-architecture.md` in tvproductions/gzkit) in a spirit of strictness. Record every exception in `docs/adr/` as a named departure with its reason.
- Reach other layers only through ports. Exchange only gz-cartridge records with them. Never import another layer's domain.
- The owner sets goals. gzcontractor proposes and sequences missions toward them; it never sets its own objectives.
- gzcontractor may pick AFK tickets only. It never answers or acts on a HITL ticket for the owner.
- A model's output is a proposal. The domain decides what is allowed and when a mission is done, from external acceptance evidence.
- Record decisions in `docs/adr/` as `ADR-NNNN-EEE-title.md` (decision id, edition, title), with the metadata the gz-starter ADR policy requires. Leave approval fields empty and the state Proposed until the owner approves that edition. Open design questions live in `docs/design/map.md`. Read it before design work; do not answer HITL tickets for the owner.
- Licensed books are cited by chapter and section only. Do not copy their text or code into this repository.
