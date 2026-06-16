# Codex Goal Example: product-evolution-lab

Use this when Codex should keep pressure-testing a non-production product environment through approved UI, API, MCP, CLI, worker, or message-bus entrypoints.

## Plan

```bash
npm run agents:goal-plan -- \
  --agent product-evolution-lab \
  --project-id agent-product \
  "Run three production-closed-loop evolution rounds and stop on product-grade blockers"
```

## Codex Goal

```text
/goal Run three production-closed-loop evolution rounds against the approved non-production target. Use product-evolution-lab as the inner loop protocol. Verify readiness before every round, use only authorized materials, collect product-gap evidence, update current-status.md, and stop on product-grade blocker, missing readiness, unsafe mutation, or completed rounds.
```

## Expected Artifacts

```text
data/product-evolution-lab/agent-product/loop-state.json
data/product-evolution-lab/agent-product/current-status.md
data/product-evolution-lab/agent-product/evidence/
```

## Stop Conditions

- Goal proven.
- Product-grade blocker appears.
- Maximum rounds or deadline is reached.
- Required readiness check fails.
- Protected-path mutation or publish requires explicit confirmation.
