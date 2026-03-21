---
name: computer-fleet
description: Control Agent Computer machines and remote agent sessions from a local agent using the aicomputer CLI. Use when you need to list machines, inspect installed agents, create or resume remote sessions, send prompts, stream progress, cancel or interrupt work, or close sessions cleanly.
allowed-tools: Bash(npm:*), Bash(npx aicomputer@latest:*), Bash(aicomputer:*), Bash(computer:*)
---

# Computer Fleet

Use the `aicomputer` CLI as the control plane for remote machine agents.

## When to use

Use this skill when the user wants to:

- work on one of their Agent Computer machines from a local agent
- delegate coding or research work to a remote Claude/Codex-style agent
- inspect remote agent status or stream progress
- stop or clean up remote agent sessions

Do not use SSH, VNC, or browser URLs when simple agent control is enough.

## Quick start

1. Ensure the CLI exists.

```bash
if command -v computer >/dev/null 2>&1; then
  COMPUTER=computer
elif command -v aicomputer >/dev/null 2>&1; then
  COMPUTER=aicomputer
else
  npm install -g aicomputer
  COMPUTER=computer
fi
```

2. Verify auth.

```bash
$COMPUTER whoami || $COMPUTER login
```

3. List running machines.

```bash
$COMPUTER ls --json
```

4. Inspect available agents on a machine.

```bash
$COMPUTER agent agents <machine> --json
```

5. Create or reuse a named session.

```bash
$COMPUTER agent sessions new <machine> --agent claude --name review --json
```

6. Send prompts and stream output.

```bash
$COMPUTER agent prompt <machine> "fix the failing tests" --agent claude --name review
```

## Default workflow

Prefer this flow:

1. Pick a running machine from `computer ls --json`.
2. Check `computer agent agents <machine> --json` and choose an installed agent with credentials.
3. Reuse a stable session name for a task thread like `review`, `debug`, or `migration`.
4. Use `computer agent prompt ...` for the work.
5. Use `computer agent status ...` or `computer fleet status --json` when you need current state.
6. Use `computer agent cancel ...` for normal stop.
7. Use `computer agent interrupt ...` only if normal cancel is not enough.
8. Use `computer agent close ...` when the session is no longer needed.

Prefer `--json` whenever you need to parse output programmatically.

## Session naming

Use short stable names:

- `review`
- `debug`
- `backend`
- `frontend`
- `release`

Reuse the same session name when continuing the same line of work on the same machine. Start a new name when the task changes meaningfully.

## Cancellation rules

- `cancel` is the normal stop path.
- `interrupt` is the hard stop path when the session does not settle quickly enough.
- `close` is cleanup after the task is done or abandoned.

## Commands reference

Read [references/cli-cheatsheet.md](references/cli-cheatsheet.md) when you need the exact command set.
