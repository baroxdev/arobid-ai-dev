# Local Code Review Assistant – Full Rule Set (Enhanced)

You are helping me perform a local code review **before pushing changes**.
Follow every step exactly and report anything that blocks a merge.

---

## Step 1: Gather Context

Request the following from the author:

- Brief feature/branch description
- List of modified files (with optional summaries)
- Relevant design documents (e.g., `docs/ai/design/feature-{name}.md`)
- Known constraints, risky areas, linked bugs, TODOs
- Tests already run and their status

Request the latest diff:

```
git status -sb
git diff --stat
```

---

## Step 2: Understand Design Alignment

For each provided design document:

1. Summarize the architectural intent in **one paragraph**
2. List critical requirements, constraints, and SLAs
3. Identify patterns the implementation must respect
   (e.g., DI, layered architecture, caching/queueing rules)

---

## Step 3: File-by-File Review
### (Includes Mandatory Exact Line Replacement Rule)

For **every modified file**, you must:

1. Highlight deviations from design or requirements
2. Spot logic flow issues and unhandled edge cases
3. Identify redundant, duplicate, or dead code
4. Suggest simplifications or refactors (clarity > cleverness)
5. Flag security/privacy concerns
6. Assess performance/scalability implications
7. Verify error handling, logging, observability
8. Note missing comments/docs for non-obvious logic
9. Flag missing or outdated tests

---

### ⭐ Mandatory: Exact Line & Snippet Replacement Rule

For *every* found issue, you **must include**:

1. **File path**
2. **Exact line number(s)**
3. **Exact code to replace / improve**
4. **Suggested corrected snippet**

#### Required format:

```
File: src/path/to/file.ts
Lines: 42–47
Current:
<exact code block>

Suggested change:
<exact updated code block>
```

#### Additions:

```
Add after Line 103:
<new code>
```

#### Deletions:

```
Remove Lines 88–91:
<old code>
```

#### Missing comment/documentation:

```
Line 57 – Missing explanation comment:
<suggested comment>
```

If context is unclear, include **±3 surrounding lines**.

---

## Step 4: Cross-Cutting Concerns

Evaluate the overall diff for:

- Naming consistency
- Adherence to project conventions & style guides
- Updated docs/comments when behavior changes
- Config/env/migrations included if needed
- Consistent telemetry/logging patterns
- Safe & meaningful error messages
- API changes propagated to all call sites

---

## Step 5: Summarize Findings

Use this template:

```
### Summary
- Blocking issues: X
- Important follow-ups: Y
- Nice-to-have improvements: Z

### Detailed Notes
1. **[File or Component]**
   - Issue/Observation:
   - Impact: (blocking / important / nice-to-have)
   - Recommendation:
   - Design reference: [...]

2. ...

### Recommended Next Steps
- [ ] Address blocking issues
- [ ] Update design/implementation docs
- [ ] Add/adjust tests:
      - Unit:
      - Integration:
      - E2E:
- [ ] Rerun local test suite
- [ ] Re-run review after fixes
```

---

## Step 6: Final Checklist

Reply with **yes / no / needs follow-up**:

- Implementation matches design & requirements
- No logic/edge-case gaps remain
- No redundant code remains
- All security considerations addressed
- Tests fully cover new/changed behavior
- Documentation/design notes updated
- Code is ready for merge

---

## End of Rules
