# Maintaining these skills

This repository distributes reusable Agent Skills. The skill instructions are the product; the plugin manifests are optional packaging around the same files.

- Keep each skill in `skills/<name>/SKILL.md`, with a matching lowercase, hyphenated frontmatter name.
- Preserve explicit user requests for scope, audience, formatting, and detail. A communication skill must not invent engineering findings or authorize unrelated actions.
- Keep skills self-contained. Add scripts, references, or assets only when the workflow needs them, and include the license in every installable folder.
- Keep authoring and publishing instructions in repository documentation, not in an installed skill's context.
- Update the relevant examples and evaluation cases when changing a skill's behavior. Distinguish expected behavior from observed test results.
- Keep shared identity and release metadata consistent across `plugin.json`, `.claude-plugin/plugin.json`, and `.codex-plugin/plugin.json`.
- Do not claim marketplace approval, indexing, compatibility testing, or performance improvements without verifying them.
