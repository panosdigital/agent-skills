# Agent Skills

Reusable skills by [Panos Spiliotis](https://github.com/panosdigital).

## Skills

| Skill | Purpose |
| --- | --- |
| [Engineering Communication](skills/engineering-communication/SKILL.md) | Explain engineering work with the behaviour and outcome first, preserving evidence, uncertainty, and requested detail. |

## Engineering Communication

Coding agents often explain their work by listing files, functions, and commands. This skill helps them explain what happened and why it matters before introducing implementation details.

Use it for diagnoses, architecture explanations, code reviews, plans, progress updates, and final handoffs to experienced developers. It also helps the agent choose between prose, a table, and a diagram when the format improves understanding.

It is not a blanket instruction to shorten every answer. Explicit requests for detail, code, evidence, or a different audience still take priority. It does not change code-only output, commit messages, or routine acknowledgments unless explicitly requested.

### Example

Illustrative wording, not a measured benchmark:

**Implementation-first:**

> I updated `cancelLoad()` in `SearchViewModel.swift` to reset `isLoading` and added a cancellation test.

**Behaviour-first:**

> Cancelling a search now clears the loading state, so the spinner stops. The cancellation test passes. The change is in `cancelLoad()`.

The technical evidence remains available; it no longer has to carry the explanation by itself.

## Install one skill

Use [Vercel's Skills CLI](https://github.com/vercel-labs/skills):

```sh
npx skills add panosdigital/agent-skills --skill engineering-communication
```

Or, with Bun:

```sh
bunx skills add panosdigital/agent-skills --skill engineering-communication
```

These are alternative ways to run the same installer. It downloads the skill from this GitHub repository and lets you choose the target agent. Bun and Node.js are not dependencies of the skill itself. The package runner may download the installer if it is not already available.

To see the available skills without installing them:

```sh
bunx skills add panosdigital/agent-skills --list
```

You can also download the repository and copy `skills/engineering-communication` into your agent's supported skills directory. No package runner is needed for a manual copy.

### Compatibility

The skill follows the [Agent Skills specification](https://agentskills.io/specification). It contains Markdown instructions and optional OpenAI display metadata, with no executable helpers, required MCP servers, API keys, services, or runtime dependencies.

It is intended for Claude Code, Codex, and other agents that support the format. Loading and invocation behavior depends on the host. See [evaluation cases](evals/engineering-communication.md) for reproducible checks; cross-agent performance is not claimed as measured.

## Use

In Codex, explicitly invoke it with:

```text
Use $engineering-communication to explain this change and its verification results.
```

In Claude Code, a standalone installation can be invoked with `/engineering-communication`. The host can also select the skill when a request matches its description.

Example requests:

- Explain the root cause of this bug to a developer who has not read the affected code.
- Summarize this change, including what was verified and what remains untested.
- Review this patch and lead each finding with the user-visible failure.
- Compare these architectures and use a diagram only if it helps explain the tradeoff.

## Repository layout

```text
skills/engineering-communication/
  SKILL.md
  LICENSE.txt
  agents/openai.yaml
evals/engineering-communication.md
plugin.json
.claude-plugin/plugin.json
.codex-plugin/plugin.json
```

Each future skill gets its own folder under `skills/`. Users can select individual skills with the Skills CLI. The optional plugin manifests package this repository's collection as **Panos Digital Skills**; they do not duplicate the skill files or establish a marketplace listing.

## License

[MIT](LICENSE). Each installable skill includes its license so the terms travel with the files.
