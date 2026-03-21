---
name: computer-acp
description: Bridge a remote Agent Computer machine agent into a local ACP-compatible stdio process using `computer acp serve`. Use when a local agent client or ACP tool needs to talk to Claude or another remote machine agent through one local command.
allowed-tools: Bash(npm:*), Bash(npx aicomputer@latest:*), Bash(aicomputer:*), Bash(computer:*), Bash(acpx:*)
---

# Computer ACP

Use this skill when a local ACP-capable client should treat a remote machine agent as if it were a local ACP server.

## What this does

`computer acp serve` starts a local stdio ACP bridge. The remote machine stays in the cloud, but the local client speaks ACP to the bridge process.

That means you can point an ACP client at a command like:

```bash
computer acp serve <machine> --agent claude --name review
```

## Setup

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

3. Pick a machine and agent.

```bash
$COMPUTER ls --json
$COMPUTER agent agents <machine> --json
```

## Start the bridge

```bash
$COMPUTER acp serve <machine> --agent claude --name review
```

Keep that process running. The local ACP client should launch or connect to this command over stdio.

## Recommended pattern

- Use one stable machine per bridge.
- Use one stable session name per task thread.
- Prefer a named session like `review` or `debug` so reconnects stay simple.
- Use the normal `computer-fleet` skill if you only need CLI control and not ACP interoperability.

## Example

If `acpx` is installed, a typical shape is:

```bash
acpx --agent "computer acp serve <machine> --agent claude --name review" "fix the failing tests"
```

## Limits

- This bridge is for agent chat/session control, not direct filesystem or terminal passthrough.
- If the bridge process exits, the ACP client loses the connection and should reconnect by starting the command again.

## Protocol notes

Read [references/acp-flow.md](references/acp-flow.md) for the supported ACP flow and expected behavior.
