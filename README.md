# Agent Skills

Reusable skills by [Panos Spiliotis](https://github.com/panosdigital).

## Skills

| Skill | Purpose |
| --- | --- |
| [Engineering Communication](skills/engineering-communication/) | Explain engineering work with the behaviour and outcome first, preserving evidence, uncertainty, and requested detail. |

Each skill's folder has a README with usage, examples, and evaluation cases.

## Install

### Individual skills

Use [Vercel's Skills CLI](https://github.com/vercel-labs/skills) to install one skill:

```sh
npx skills add panosdigital/agent-skills --skill <skill-name>
```

Or, with Bun:

```sh
bunx skills add panosdigital/agent-skills --skill <skill-name>
```

These are alternative ways to run the same installer. It downloads the skill from this GitHub repository and lets you choose the target agent. Bun and Node.js are not dependencies of the skills themselves. The package runner may download the installer if it is not already available.

To see the available skills without installing them:

```sh
bunx skills add panosdigital/agent-skills --list
```

You can also download the repository and copy a folder from `skills/` into your agent's supported skills directory. No package runner is needed for a manual copy.

### Claude Code plugin

Install every skill in this repository as one plugin:

```text
/plugin install agent-skills --marketplace panosdigital/agent-skills
```

This works in one step on Claude Code 2.1.275 or later.

## Compatibility

The skills follow the [Agent Skills specification](https://agentskills.io/specification). They work with any agent that supports the Agent Skills format, including Claude Code and Codex. Loading and invocation behavior depends on the host.

## Repository layout

```text
skills/engineering-communication/
  SKILL.md
  README.md
  LICENSE.txt
  agents/openai.yaml
evals/engineering-communication.md
evals/fixtures/
evals/verify_fixtures.py
plugin.json
.claude-plugin/plugin.json
.claude-plugin/marketplace.json
.claude-plugin/icon.png
.codex-plugin/plugin.json
```

Each skill gets its own folder under `skills/` and its own evaluation file under `evals/`. Users can select individual skills with the Skills CLI. The optional plugin manifests package this repository's collection as **Panos Digital Skills** without duplicating the skill files. `.claude-plugin/marketplace.json` makes this repository a Claude Code marketplace that users can install from directly; it is not a listing in any public catalog.

## License

[MIT](LICENSE). Each installable skill includes its license so the terms travel with the files.
