# Codex Goal Runtime Adapter

Codex `/goal` is the outer objective runtime for Octopus AgentOps agents. The toolkit loop contract remains runtime-neutral; Codex only supplies a persistent goal driver for environments where the `goals` feature is enabled.

## Boundary

Use this adapter when a Codex project has installed `integrations/codex/agents/*.toml` into `.codex/agents/` and the user wants a long-running or repeated goal-driven workflow.

Do not treat `/goal` as a replacement for an agent's domain loop protocol. The outer Codex goal keeps the work moving; the selected agent still owns loop inputs, loop state, evidence requirements, stop policies, confirmation gates, and dangerous-action boundaries.

## Mapping

```text
Codex /goal
  -> outer objective runtime
  -> resume and continue pressure
  -> stop when the goal is complete or blocked

Octopus agent loopContract
  -> inner domain loop protocol
  -> loopCadence, goalWindow, stopPolicies, loopState, evidence
  -> confirmation gates and dangerous actions
```

## Required Runtime Checks

Before starting a Codex-goal run:

1. Check the project-scoped Codex install:

   ```bash
   npm run agents:codex-status -- --project-root /path/to/project
   ```

2. Check whether Codex goals are enabled. The status command reports this when `codex` is available.

3. Render the adapter plan:

   ```bash
   npm run agents:goal-plan -- --agent mcp-e2e-governor --project-id my-project "Prove the MCP onboarding journey"
   ```

4. Start `/goal` in Codex with the rendered outer goal, then run the selected installed agent as the inner loop protocol.

## State And Evidence

Every Codex-goal run must persist or report:

- Loop goal window: `finalGoal`, `phaseGoals`, `currentPhase`, `acceptanceCriteria`, `reportCadence`, and `finalDecision`.
- `loop-state.json`: current loop state, blocker, stop policy, and next action.
- `current-status.md`: human-readable heartbeat for long-running loops.
- `evidence/`: command output, MCP responses, screenshots, logs, artifacts, or assertion reports.

If the agent cannot establish the loop goal window or write these artifacts in the target environment, it must report the same fields in chat and stop on missing evidence rather than claiming release readiness.

## Safety Rules

- Keep confirmation gates authoritative even when `/goal` is continuous.
- Stop on pending user confirmation, missing evidence, unsafe production action, or a domain blocker.
- Do not silently accept self-evolution candidates as new loop rules.
- Do not promote project-specific runtime facts into generic toolkit instructions.
