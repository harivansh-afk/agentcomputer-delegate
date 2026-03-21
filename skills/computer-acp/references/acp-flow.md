# ACP Flow

The `computer acp serve` bridge is intended to feel like a local ACP agent command while proxying work to a remote machine agent.

## Basic shape

1. The local client starts `computer acp serve <machine> --agent <agent> --name <session>`.
2. The bridge handles ACP initialization on stdin/stdout.
3. The bridge maps ACP session operations onto Agent Computer session APIs.
4. Remote session updates are streamed back as ACP `session/update` notifications.

## Good commands

```bash
computer acp serve yinnar-south --agent claude --name review
computer acp serve airport --agent claude --name debug
```

## Recommended client behavior

- Reuse a stable session name when reconnecting.
- Treat the bridge as the single local command for remote-agent interaction.
- Use the normal `computer agent ...` commands outside ACP when you need manual inspection or cleanup.
