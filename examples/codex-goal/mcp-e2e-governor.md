# Codex Goal Example: mcp-e2e-governor

Use this when a Codex project has installed `mcp-e2e-governor` and the user wants an MCP E2E loop to continue until assertions pass or a gate blocks progress.

## Plan

```bash
npm run agents:goal-plan -- \
  --agent mcp-e2e-governor \
  --project-id domainforge-fabric \
  "Prove the MCP material-evolution journey from prompt confirmation to evidence-backed proposal"
```

## Codex Goal

```text
/goal Prove the MCP material-evolution journey from prompt confirmation to evidence-backed proposal. Use mcp-e2e-governor as the inner loop protocol. Execute from the MCP boundary, preserve prompt confirmation, collect assertion evidence, persist loopState, and stop on pending approval, critical blocker, or passed assertions.
```

## Expected Artifacts

```text
data/mcp-e2e/domainforge-fabric/loop-state.json
data/mcp-e2e/domainforge-fabric/current-status.md
data/mcp-e2e/domainforge-fabric/evidence/
```

## Stop Conditions

- Assertions pass.
- Maximum attempts or deadline is reached.
- Prompt confirmation is pending.
- Self-evolution approval is pending.
- A critical MCP-facing blocker appears.
