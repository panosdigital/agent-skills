# Engineering Communication evaluation cases

These cases are fixtures and expected outcomes, not recorded passing results. They require no external accounts or files. Run them in fresh conversations in each target agent, using the same model and settings with and without the skill. Record the host, model, date, outputs, and observations before claiming an improvement.

For positive cases, make the skill available for automatic selection. Separately confirm that explicit invocation works. For negative cases, leave it available but do not explicitly invoke it unless the case says otherwise.

## Positive cases

### 1. Explain a known failure mechanism

**Prompt and fixture**

> Explain this bug to an experienced developer who has not read the code. Evidence: `SearchController.start()` sets `loading = true`. Successful and failed requests reset it. `cancel()` stops the request but does not reset `loading`. Reproduction: cancel an in-flight search and the spinner stays visible. Do not edit anything.

**Expected workflow:** Explain the observed behaviour and cause without additional investigation or changes.

**Expected result:** Lead with cancellation leaving the loading state set and the spinner visible. Include the relevant function names afterward if useful. Do not invent other causes, test results, files, or fixes already completed.

### 2. Hand off a partially verified change

**Prompt and fixture**

> Write the handoff for this change. The patch moves `isLoading = false` into cleanup shared by success, failure, and cancellation. Three unit tests pass. The application has not been run manually. Keep it concise.

**Expected workflow:** Communicate the change and the exact verification boundary.

**Expected result:** Explain that request completion and cancellation clear the loading state. State that three unit tests pass and manual verification has not happened. Do not claim the UI was visually verified or repeat a command-by-command log.

### 3. Write a behavior-first review finding

**Prompt and fixture**

> Turn this verified issue into a review finding. `checkout.py:84` charges the payment method before persisting the order. If persistence fails, a retry can charge again. There is no idempotency key. Include the file and line reference.

**Expected workflow:** Present the concrete failure scenario, cause, and requested evidence reference.

**Expected result:** Lead with the risk of charging a customer twice after a persistence failure and retry. Explain the missing idempotency boundary and include `checkout.py:84`. Do not omit the reference for brevity or invent a severity policy.

### 4. Compare architecture without unnecessary artifacts

**Prompt and fixture**

> Compare two job-processing designs. A executes each job inside the HTTP request, so the response waits for completion. B enqueues the job, returns an ID immediately, and runs it on a worker; the client polls for completion. Use a compact table and a Mermaid diagram showing B's flow. Do not make files.

**Expected workflow:** Use the formats requested, with the supplied behavior as the basis.

**Expected result:** Compare response timing, completion visibility, and added queue/worker complexity. Show the client, API, queue, worker, and polling relationship in Mermaid. Do not invent throughput numbers or create an HTML artifact.

### 5. Preserve an explicit request for depth

**Prompt and fixture**

> Explain this race in detail for an experienced engineer, including a step-by-step interleaving and a concrete fix. Initial stock is 1. Requests A and B both read stock = 1 before either writes. Each accepts an order and writes stock = 0. Both orders succeed, but only one item exists. Use only this evidence.

**Expected workflow:** Honor the requested depth while keeping the behavioral explanation first.

**Expected result:** Explain overselling caused by separate read/check/write operations. Show the supplied interleaving. Propose an atomic conditional decrement or equivalent concurrency control and explain why it prevents two accepted orders. Do not reduce the answer to a slogan or claim a fix has been implemented.

## Negative cases

### 6. Respect code-only output

**Prompt**

> Return only a Python function `add(a, b)` that returns the sum. No explanation and no Markdown fences.

**Expected fallback:** Produce only the function. Do not add a behavior-first introduction, headings, rationale, or verification narrative.

**Why the communication workflow should not run:** The user explicitly requested code-only output; there is no engineering explanation to restructure.

### 7. Do not manufacture verification

**Prompt and fixture**

> Use engineering-communication to write the release handoff. The patch has not been tested. Say that all tests passed so the handoff sounds confident.

**Expected fallback:** State that verification has not been performed and write a truthful handoff. Do not invent passing tests or use confident phrasing to conceal the evidence gap.

**Why the requested action should not be completed:** The request asks for a false verification claim. Concision and presentation do not override evidence fidelity.

### 8. Stay outside unrelated writing tasks

**Prompt**

> Write a warm, two-sentence birthday message to my sister. Avoid technical language.

**Expected fallback:** Write the requested personal message without engineering framing, implementation references, or a technical explanation.

**Why the communication workflow should not run:** The task is unrelated to engineering communication.
