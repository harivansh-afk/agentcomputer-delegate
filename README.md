# agentcomputer-delegate

Skills for controlling Agent Computer machines and remote agent sessions through the `aicomputer` CLI.

## Install

Install all skills:

```bash
npx skills add harivansh-afk/agentcomputer-delegate -g -y
```

Install only the main fleet-control skill:

```bash
npx skills add harivansh-afk/agentcomputer-delegate -g -y --skill computer-fleet
```

Install only the ACP bridge skill:

```bash
npx skills add harivansh-afk/agentcomputer-delegate -g -y --skill computer-acp
```

## Skills

- `computer-fleet`: Use `computer` / `aicomputer` to list machines, create remote agent sessions, prompt them, watch progress, cancel, interrupt, and close.
- `computer-acp`: Use `computer acp serve` to expose a remote machine agent as a local ACP-compatible stdio command.

## Notes

- These skills assume the `aicomputer` CLI is installed or can be installed with `npm install -g aicomputer`.
- Authentication uses the normal browser flow: `computer login`.
- The recommended install source is this repo directly:

```bash
npx skills add harivansh-afk/agentcomputer-delegate
```
