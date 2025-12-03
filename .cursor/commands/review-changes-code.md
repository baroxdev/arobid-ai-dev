# Code Review With Snapshot

You are helping me perform a local code review **with an automatic git snapshot first**.

---

## Phase 1: Git Snapshot (run terminal commands)

1. In the project root, use the terminal tool to run:
   ```bash
   git status -sb
   git diff --stat
   ```

2. Capture the output and present it exactly as:
   ```text
   === git status -sb ===
   <full output here>

   === git diff --stat ===
   <full output here>
   ```

3. Do **not** summarize or interpret the results in this phase.

---

## Phase 2: Full Code Review (same rules as `/code-review`)

Now continue as a full `/code-review` session over the paths I provide
(for example `@app`), following the rules from `.cursor/commands/code-review.md`:

1. **Gather context**
   - Ask for:
     - Brief feature/branch description
     - List of modified files (with optional summaries)
     - Relevant design documents under `docs/ai/design/`
     - Known constraints, risky areas, linked bugs, TODOs
     - Tests already run and their status

2. **Understand design alignment**
   - For each design doc:
     - Summarize architectural intent in one paragraph
     - List critical requirements, constraints, SLAs
     - Note patterns the implementation must respect

3. **File-by-file review** (including the Exact Line & Snippet Replacement Rule)
   - Highlight deviations from design/requirements
   - Spot logic flow issues and unhandled edge cases
   - Identify redundant/duplicate/dead code
   - Suggest simplifications or refactors (clarity > cleverness)
   - Flag security/privacy concerns
   - Assess performance/scalability
   - Verify error handling, logging, observability
   - Note missing comments/docs
   - Flag missing or outdated tests

   For **every** found issue, include:

   - File path
   - Exact line number(s)
   - Exact current code
   - Suggested corrected snippet

   Using this format:

   ```text
   File: path/to/file.tsx
   Lines: 42–47
   Current:
   <exact code block>

   Suggested change:
   <exact updated code block>
   ```

4. **Cross-cutting concerns**
   - Naming consistency and conventions
   - Docs/comments updated when behavior changes
   - Config/env/migrations included if needed
   - Consistent telemetry/logging
   - Safe, meaningful error messages
   - API changes propagated to all call sites

5. **Summarize findings**
   - Use the same Summary / Detailed Notes / Recommended Next Steps template
     defined in `.cursor/commands/code-review.md`.

6. **Final checklist**
   - Reply with yes / no / needs follow-up for the final checklist items in
     `.cursor/commands/code-review.md`.

---

Always perform **Phase 1 (snapshot)** and then **Phase 2 (review)** in a single `/review-with-snapshot` run.


