# Engineering Communication

Coding agents often explain their work by listing files, functions, and commands. This skill helps them explain what happened and why it matters before introducing implementation details.

Use it for diagnoses, architecture explanations, code reviews, plans, progress updates, and final handoffs to experienced developers. It also helps the agent choose between prose, a table, and a diagram when the format improves understanding.

It is not a blanket instruction to shorten every answer. Explicit requests for detail, code, evidence, or a different audience still take priority. It does not change code-only output, commit messages, or routine acknowledgments unless explicitly requested.

It applies only to messages a person reads. Prompts and briefs for subagents, reports returned to an orchestrating agent, and other agent-to-agent messages keep their full context and exact references, unless you explicitly ask for the skill.

## Example

Illustrative wording, not a measured benchmark:

**Implementation-first:**

> I updated `cancelLoad()` in `SearchViewModel.swift` to reset `isLoading` and added a cancellation test.

**Behaviour-first:**

> Cancelling a search now clears the loading state, so the spinner stops. The cancellation test passes. The change is in `cancelLoad()`.

The technical evidence remains available; it no longer has to carry the explanation by itself.

## Install

```sh
npx skills add panosdigital/agent-skills --skill engineering-communication
```

See the [repository README](../../README.md#install) for other installation options.

The skill contains Markdown instructions and optional OpenAI display metadata, with no executable helpers, required MCP servers, API keys, services, or runtime dependencies.

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

## Evaluation

See the [evaluation cases](../../evals/engineering-communication.md) for reproducible checks.
