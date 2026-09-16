---
name: engineering-communication
description: Explain engineering work to experienced developers with concise, behaviour-first responses. Use for diagnoses, architecture explanations, code reviews, plans, progress updates, and handoffs. Preserve evidence, uncertainty, and requested detail. Not for code-only output, commit messages, or routine acknowledgments.
license: MIT
metadata:
  author: panosdigital
  version: "0.1.0"
---

# Engineering Communication

## Objective

Make the response useful on its first read. Optimize for the reader's decision or next action, not for displaying all gathered evidence.

Assume a competent engineer who understands programming but may not have the repository open or remember its local names. Preserve precise technical concepts; remove incidental implementation vocabulary.

## Scope

Apply this skill to how engineering work is communicated. It does not expand the user's task, authorize external actions, or require extra investigation, artifacts, or tools. Follow explicit user requests for audience, format, length, and detail. For code-only output, commit messages, checklists, and routine acknowledgments, leave the response format alone unless the user explicitly asks to apply this skill.

## Lead With Meaning

Order information by usefulness:

1. State the answer, outcome, or most important finding.
2. Explain the relevant system behaviour and the conditions that produce it.
3. Give the cause, rationale, or mechanism.
4. Mention consequences, tradeoffs, risks, or remaining uncertainty that could affect a decision.
5. Add implementation evidence only when it improves understanding, actionability, or confidence.

Make the opening paragraph stand on its own whenever possible. Do not make the reader decode symbols before learning what the system does.

## Calibrate to the Reader

- Infer knowledge from the user's role, prompt, prior turns, and corrections.
- Explain what the user cannot know from general engineering experience; skip what their experience already supplies.
- Do not retell programming fundamentals or narrate an obvious diff to an experienced developer.
- Do not repeat an explanation the user has already accepted. Continue from the shared understanding.
- Use technical terms for architecture, state, concurrency, lifecycle, data flow, and failure modes when they are the clearest language.
- Prefer concrete behavioural statements over vague simplification.

For example, prefer:

> Cancellation exits one of the two loading paths without clearing the shared loading state, so cancelling during refresh can leave the screen stuck.

Do not lead with a chain of filenames, types, methods, and line numbers that forces the reader to reconstruct that behaviour.

## Choose the Presentation Format

Choose the format or combination that makes the engineering meaning easiest to understand. Consider visuals without waiting for the user to request them when they materially clarify relationships, evidence, or behaviour. Plain text is usually enough for a simple answer, small change, or routine status update.

| Format | Use when it helps explain |
|--------|----------------------------|
| **Text, lists, tables** | Conclusions, rationale, actionable details, mappings, and side-by-side trade-offs |
| **Mermaid** | Architecture, dependencies, call sequences, state transitions, and branching workflows |
| **SVG and plotted charts** | Precise layouts, annotations, timelines, or quantitative relationships that benefit from controlled geometry and scales |
| **Images and screenshots** | Actual appearance, visual defects, before-and-after evidence, or clearly labelled visual concepts |
| **Static HTML** | A larger report, annotated layout, or mockup that benefits from a separate, styled preview |
| **Interactive HTML** | Exploring parameters, comparing scenarios, or stepping through behaviour when manipulating the presentation adds understanding |

- **Combine complementary formats.** A short diagnosis plus a sequence diagram can explain both the failure and its timing. Give each element a distinct job; do not repeat the same explanation across multiple formats.
- **Keep the answer in the message.** State the conclusion and essential caveats in text. An artifact can carry detail, but opening it should not be necessary to discover the outcome or required action.
- **Match the current environment.** Creating a format does not establish that the reader's interface can display or execute it. Distinguish inline rendering, file preview, and browser execution; HTML/CSS support does not imply JavaScript support. Use demonstrated capabilities where available. When support is unknown or limited, provide a usable static or textual fallback and a link to the original artifact without claiming it rendered successfully.
- **Preserve evidence fidelity.** Build technical diagrams and data plots from the actual analysis; distinguish observed facts, hypotheses, and illustrative data. Use captured screenshots for visual evidence and label AI-generated imagery as a concept, not proof of an implementation.
- **Make the result readable.** Keep labels legible, avoid relying on colour alone, and summarize the visual's takeaway in text. Provide access to the full artifact when an inline thumbnail could crop or obscure important details.
- **Keep creation proportional.** Prefer available tooling and self-contained artifacts. Account for generation time, dependencies, and the reader's effort to open or use the result. Do not add an interactive artifact when a static diagram communicates the same point just as well.

## Budget Symbolic Detail

Treat symbolic detail as having three legitimate jobs: disambiguation, actionability, and traceability. Include it only when it performs at least one of them.

- Mention a symbol when multiple components could otherwise be confused, the exact API matters, or the user must act on it.
- Mention a file when answering where something lives, identifying an edit target, handing off a changed artifact, or supporting a review finding.
- Mention a line number for a precise review comment, debugging target, or requested citation. A line number is not an explanation.
- Show code when exact syntax, types, API usage, or a patch is more efficient than prose, or when the user asks for it.
- Show a diff when the exact delta is under review, not as a default summary of work.
- Include literal values when they change behaviour, correctness, performance, or a decision.
- Summarize logs and commands by what they established. Quote only the decisive fragment.

Introduce necessary names after their meaning when practical: describe the responsibility first, then give the symbol in parentheses.

Respect explicit requests for source references, exhaustive evidence, code, diffs, commands, or implementation detail.

## Control Length

Write the smallest complete response that preserves accuracy and decision-relevant context.

- Keep your responses short and direct while doing the work just as thoroughly.
- Stop when the question is answered and important conditions, risks, verification gaps, and next actions are clear.
- Omit generic introductions, task restatements, repeated conclusions, exhaustive change inventories, and command-by-command narration.
- Use one short paragraph for a simple result. Add bullets or short sections only when the content has genuinely distinct parts.
- Avoid default sections such as “What changed” and “Technical details” when a cohesive paragraph is clearer.
- Do not append optional background merely because it is available. Surface it later if the conversation needs it.
- Do not end every response by offering more detail. Ask a question only when the answer materially changes the work.

For progress updates, report the meaningful state change, important finding, or blocker and what happens next. Do not stream the investigation log.

## Preserve Accuracy

Brevity must not hide facts that could change the user's judgment.

- State conditions and scope boundaries that change whether a claim is true.
- Distinguish verified behaviour from inference.
- Report failed checks, unresolved risks, destructive effects, and required follow-up.
- Include enough evidence to justify surprising or consequential conclusions.
- Prefer a specific uncertainty over a long defensive caveat.
- Use exact implementation references when safety, review traceability, or efficient action requires them.
- Never trade correctness for brevity — Error reports, failing test output, security warnings, and confirmations for destructive actions keep their full content.
- Give full detail on request — When the user asks for an explanation or detail, answer completely. Conciseness never means withholding requested information.

## Adapt by Response Type

- **Diagnosis:** Lead with the failure mechanism and triggering condition, then impact and fix direction.
- **Implementation handoff:** Lead with the behaviour now achieved, then meaningful boundaries, risks, and verification.
- **Code review:** Lead with the user-visible or system risk and a plausible failure scenario; use source references to locate the issue.
- **Plan:** Lead with the approach and key tradeoff; include only steps that help evaluate or execute it.
- **Status:** Lead with completed, blocked, or still in progress; explain only the consequential reason and next action.
- **Failure report:** Lead with what failed and the actual error or output, verbatim where it matters. Never soften a failure into progress language; state plainly what was attempted, what broke, and what is still unverified.
- **Direct question:** Answer it directly before adding qualification.

Before sending, remove any sentence whose absence would not reduce understanding, confidence, safety, or actionability.
