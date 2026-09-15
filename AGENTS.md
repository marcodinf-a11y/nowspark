# Agent instructions

## Delegation and context management

Prefer small, focused contexts to reduce context rot. Keep the main agent focused
on orchestration: understanding the request, dividing work, tracking decisions,
and integrating and verifying results. Delegate substantial investigation and
implementation to subagents whenever practical.

### Context budget

Use these approximate context-window targets for both the orchestrator and
subagents:

- Up to about 20%: preferred.
- Between about 20% and 40%: acceptable.
- Above about 40%: a signal to split remaining work or prepare a handoff.

These are planning guidelines, not hard limits or measured quality guarantees.
Use context-usage information when available; otherwise judge by the amount of
material needed and the scope of the task. Prefer natural task boundaries over
cutting work at an arbitrary percentage.

### Dividing work

- Give each subagent a bounded objective with a clear completion criterion.
  If the work is likely to exceed the context budget, divide it further.
- Pass only the relevant requirements, decisions, file references, and necessary
  background. Prefer a focused brief over inheriting the full conversation.
- Use parallel subagents for independent tasks, with clear ownership of edits.
  Use sequential subagents when later work depends on earlier results.
- Prefer a succession of focused agents over one agent repeatedly compacting.
  At natural boundaries, hand completed findings to a fresh agent for the next
  stage.
- Handle trivial, tightly scoped work directly when delegation would add more
  coordination overhead than context savings.

### Handoffs and integration

Subagents should return a concise summary of the outcome, changed files,
verification performed, and unresolved questions or risks. Include the decisions
and evidence needed for the next step; keep detailed artifacts in files and
reference them instead of returning raw logs or large source excerpts.

The orchestrator remains responsible for reconciling results, checking the
combined work against the user's request, and completing appropriate validation.
