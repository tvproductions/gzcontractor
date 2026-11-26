---
id: ADR-0002
title: Each layer admits memory at the scope of the unit it accepts
revision: 1
state: Proposed
decision_date: 2026-11-26
revision_date: 2026-11-26
approved_by: ""
approved_revision: ""
approval_ref: ""
---

# ADR-0002 — Each layer admits memory at the scope of the unit it accepts

The owner settled design-map ticket C2 on 2026-11-26 in the gzfactory
project's memory-ownership discussion. That choice does not approve this
written edition. The approval fields stay empty, and the state stays
Proposed, until the owner approves revision 1.

## Context

*AI Agents in Action* (2nd ed.) is the baseline. In 10.2 its cognitive agent
records an experience only after its own evaluation module has scored the
outcome. In 6.4.5 it says production memory needs access control, eviction
and evaluation, and it allows separate stores for each scope.

*Designing AI Agents* (Huang, 4.1, 4.6, 10.10) adds validity gates on memory
and writes memory only after the outcome is accepted outside the agent.
Security guidance also names memory poisoning as an agentic risk.

gzkit's drydock refit review (`docs/rnd/repair-work-organization/review.md`
in tvproductions/gzkit) names four levels of work. An epic is a feature
package. A story is a work package. An order is a work order, where Gate 5
acceptance sits. An action is a task.

## Decision

1. Long-lived memory is written after the fact, only after the unit of work
   is accepted outside the agent that did it. Working notes inside a unit of
   work are not affected.
2. The admission rules sit with the layer that accepts the unit:

   | gzkit unit | Layer | Owns admission of |
   | --- | --- | --- |
   | Work package | gzcontractor (layer 3) | lessons across work orders |
   | Work order | gzfactory (layer 2) | lessons from one run, after Gate 5 |
   | Task | gzyoke (layer 1) | working notes only; it proposes candidate memories |

3. Memory stores, Graphiti first, are adapters behind a memory port. Mem0,
   pueo's earlier choice, could return only as another adapter.

## Departure from the baseline

The book's gate is the agent's own evaluation module. This decision moves
the judge outside the agent. Reason: a model's output is a proposal
(settled input in the design map), and self-judged memory can be poisoned
or wrong without anyone outside the agent noticing.

## Consequences

- gzcontractor defines a memory port for work-package lessons. gzfactory
  defines its own for run lessons. There is no shared memory context that
  both call.
- gzyoke's outputs carry candidate memories as proposals. gzfactory decides
  which of them to admit.
- Each admitted memory records its source unit and acceptance evidence.

## Reversal

Only an explicit owner decision changes this.
