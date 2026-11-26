---
id: ADR-0003
title: In our own loops the model is a driven actor
revision: 1
state: Proposed
decision_date: 2026-11-26
revision_date: 2026-11-26
approved_by: ""
approved_revision: ""
approval_ref: ""
---

# ADR-0003 — In our own loops the model is a driven actor

The owner settled design-map ticket C1 on 2026-11-26 in the gzfactory
project's book-impact discussion. That choice does not approve this
written edition. The approval fields stay empty, and the state stays
Proposed, until the owner approves revision 1.

## Context

Strict hexagonal architecture asks, for each interaction, who starts it.
*Clean Applications with Hexagonal Architecture* (Montenegro, 10.1) gives
direction to each interaction, not to the whole system. A model can look
like a driving actor because its tool calls ask our code to act.

*AI Agents in Action* (2nd ed.), the baseline, runs the model inside the
agent loop that our code controls. *Designing AI Agents* (Huang, 10.10)
says completion needs acceptance outside the agent.

## Decision

1. Inside our own loops, in every layer, the model sits behind an output
   port. Our handler calls it.
2. A tool call the model returns is an untrusted proposal. The handler
   validates it against policy before any adapter acts on it.
3. The model is never a driving actor in our loops. It cannot call input
   ports directly.

## Consequences

- Port shapes in every layer treat model output as a proposal to validate,
  never as a command.
- Model providers are driven adapters behind that port, and can be swapped.

## Reopen trigger

Reopen this decision if we expose tools to outside agents, for example as an
MCP server. An outside agent calling us would be a driving actor, and needs
its own driving adapter and input ports.

## Reversal

Only an explicit owner decision changes this.
