Review the current branch's changes against main (or the base branch) using the checklist below. Work through every section in order. Do not skip sections. Report findings inline as you go, then give a final verdict.

## How to run

1. Get the diff: `git diff main...HEAD` (or the base branch if specified by the user)
2. Get the commit log: `git log main...HEAD --oneline`
3. List changed files: `git diff main...HEAD --name-only`
4. For each changed file, read the full file if context is needed to evaluate design or complexity
5. Work through the checklist below top-to-bottom, section by section

---

## Checklist

### 1. Scope — is this change focused?

- [ ] The change does one thing. It is not secretly a refactor + feature + bug fix bundled together.
- [ ] Every file touched is necessary for the stated purpose.
- [ ] If the change is large (>400 lines of diff excluding generated/vendor code), flag it and explain why splitting would help.

### 2. Design — does this fit the system?

- [ ] New abstractions are justified. No premature generalization.
- [ ] Interfaces and boundaries make sense. Dependencies flow in the right direction.
- [ ] The change doesn't duplicate logic that already exists elsewhere in the codebase.
- [ ] If this interacts with other systems or teams, those interactions are correct.

### 3. Functionality — does it do what it claims?

- [ ] The code does what the PR description says it does.
- [ ] Edge cases are handled (empty inputs, nulls, off-by-one, concurrency if relevant).
- [ ] No obvious logic errors or off-path bugs introduced.
- [ ] If there is UI, the user-visible behavior is correct (check screenshots or demo if provided).

### 4. Complexity — is it as simple as it could be?

- [ ] No function or method is doing too much. Single responsibility is preserved.
- [ ] No clever code that requires a comment to decode. If a comment is needed to explain *what* the code does, the code should be rewritten.
- [ ] No over-engineering: no unnecessary layers, interfaces, or indirection added.
- [ ] A new reader could understand each changed section in under 2 minutes.

### 5. Tests — are they real and sufficient?

- [ ] Tests accompany every non-trivial change.
- [ ] Tests are testing behavior, not implementation details.
- [ ] Tests would actually catch a regression if the code were broken.
- [ ] No tests that always pass regardless of the code under test.
- [ ] Test names describe what is being tested and what the expected outcome is.

### 6. Naming — are names honest and precise?

- [ ] Variables, functions, and classes are named for what they *are*, not what they *do to get there*.
- [ ] No misleading names (e.g., a function called `getUser` that also writes to the database).
- [ ] Abbreviations are not used unless they are universally understood in this domain.

### 7. Comments — do they explain *why*, not *what*?

- [ ] No comments that restate what the code already says.
- [ ] Any non-obvious constraint, invariant, or workaround has a comment explaining *why* it exists.
- [ ] No commented-out code left behind.
- [ ] Public API docs (if applicable) are accurate and complete.

### 8. Code health — does this leave the codebase better?

- [ ] No new TODO/FIXME added without a tracking issue or justification.
- [ ] No dead code introduced.
- [ ] Dependencies added are justified; no bloat.
- [ ] The change does not make future changes harder (no premature lock-in).

### 9. PR description — is the record complete?

- [ ] The description explains *why* the change is being made, not just what files changed.
- [ ] A future engineer searching git history would find this commit useful.
- [ ] If there are follow-up items, they are tracked (linked issues, TODOs with tickets).

---

## Verdict

After completing all sections, output one of:

- **APPROVE** — no blocking issues found. List any non-blocking nits clearly labeled `[nit]`.
- **NEEDS CHANGES** — list each blocking issue with: the file + line, what the problem is, and what a correct fix looks like.
- **NEEDS DISCUSSION** — fundamental design or scope question that requires author input before line-level review is useful.

Keep findings specific: file path, line number or function name, and a concrete suggestion. Never just say "this could be better."
