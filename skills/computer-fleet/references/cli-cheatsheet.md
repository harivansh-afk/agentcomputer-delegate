# CLI Cheatsheet

## Authentication

```bash
computer whoami
computer login
```

## Machine discovery

```bash
computer ls --json
computer fleet status --json
```

## Agent discovery

```bash
computer agent agents <machine> --json
```

## Sessions

```bash
computer agent sessions list <machine> --json
computer agent sessions new <machine> --agent claude --name review --json
computer agent status <machine> --session <session_id> --json
```

## Prompting

```bash
computer agent prompt <machine> "inspect the repo and summarize the failing tests" --agent claude --name review
computer agent prompt <machine> "continue from the previous task" --session <session_id>
```

## Streaming and control

```bash
computer agent watch <machine> --session <session_id>
computer agent cancel <machine> --session <session_id> --json
computer agent interrupt <machine> --session <session_id> --json
computer agent close <machine> --session <session_id>
```

## Good defaults

- Prefer machine handles over machine ids when both are available.
- Prefer `--name` for human-meaningful persistent sessions.
- Prefer `--json` when another program or agent needs to read the result.
