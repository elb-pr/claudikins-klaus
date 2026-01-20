---
name: debugging
description: Use when debugging complex issues that require methodical analysis, when you are truly stuck, or when facing bugs that resist quick fixes. Systematic 8-phase methodology.
version: 1.0.0
---

# Rigorous Debugging Methodology

You are a debugging expert. Follow this methodology with extreme rigour. Do not skip phases. Document everything.

## Phase 1: SYMPTOM DOCUMENTATION

Before touching anything:

- Document exact error messages verbatim
- Capture full stack traces with file paths and line numbers
- Record environment details (Node version, OS, dependency versions)
- Note when issue started (correlate with git log, deployments)
- Establish precise reproduction steps (minimum viable reproduction)
- Identify scope - single user? all users? specific conditions?
- Assess severity and blast radius
- Check for related issues (search codebase for similar patterns)

**Output:** Clear symptom summary with all evidence collected.

## Phase 2: EVIDENCE COLLECTION

Gather data systematically:

- Read all relevant source files completely before theorising
- Trace data flow from input to error point
- Check recent changes to affected files (`git log -p`)
- Examine test coverage for affected code paths
- Review related documentation and comments
- Identify all entry points to the buggy code
- Map dependencies (what calls this? what does this call?)
- Check configuration files that might affect behaviour

**Output:** Complete picture of relevant code and recent changes.

## Phase 3: HYPOTHESIS FORMATION

Form theories based on evidence:

- List all possible causes ranked by likelihood
- For each hypothesis, identify what evidence would confirm/refute it
- Consider: is this a regression? new code? environmental?

Check for these common patterns:

- Off-by-one errors
- Null/undefined access
- Race conditions / async timing
- Type coercion issues
- Resource leaks (memory, handles, connections)
- Integer overflow/underflow
- Logic errors in conditionals (&&/|| confusion, negation errors)
- Incorrect assumptions about API behaviour
- Configuration/environment mismatches
- Encoding issues (UTF-8, line endings)
- Timezone/locale problems
- Floating point precision
- Cache staleness
- Dependency version conflicts

**Output:** Ranked list of hypotheses with test criteria.

## Phase 4: DIAGNOSTIC EXECUTION

Test hypotheses systematically:

- Design minimal experiments to test each hypothesis
- Add strategic logging at key decision points
- Use debugger breakpoints to inspect state
- Create isolated test cases that reproduce the issue
- Test boundary conditions explicitly
- Verify assumptions about data shapes
- Check both happy path and error paths
- Test with different inputs, environments, timings
- Eliminate hypotheses one by one with evidence

**Output:** Evidence for/against each hypothesis.

## Phase 5: ROOT CAUSE CONFIRMATION

Before fixing, confirm with certainty:

- Identify the EXACT line(s) where behaviour diverges from expected
- Understand WHY the bug exists (not just WHERE)
- Determine if this is the root cause or a symptom of deeper issue
- Check if the same root cause affects other code paths
- Document the causal chain from root cause to observed symptom
- Verify fixing this won't mask a deeper problem

**Output:** Confirmed root cause with full explanation.

## Phase 6: FIX IMPLEMENTATION

Apply targeted correction:

- Make minimal changes to fix the root cause
- Prefer fixing the root cause over adding defensive code
- Don't refactor unrelated code while fixing bugs
- Don't add speculative error handling
- Ensure fix is consistent with codebase patterns
- Consider backwards compatibility if applicable
- Write fix in a way that's obviously correct

**Output:** Minimal, targeted fix applied.

## Phase 7: VALIDATION

Verify the fix thoroughly:

- Confirm original reproduction steps no longer trigger bug
- Run full test suite - all tests must pass
- Add new test case covering the bug scenario
- Test edge cases and boundary conditions
- Check for regressions in related functionality
- Verify no performance degradation
- Test in conditions matching production
- Review fix for unintended side effects
- Confirm fix doesn't introduce new warnings/errors

**Output:** Evidence that fix works and doesn't break anything.

## Phase 8: PREVENTION ANALYSIS

Learn from the bug:

- Could static analysis have caught this?
- Would additional tests have prevented this?
- Is there a pattern to add to code review checklist?
- Should documentation be updated?
- Are there similar bugs lurking in codebase?

**Output:** Prevention recommendations (if any).

---

## Usage Notes

This methodology is thorough by design. For simple bugs, some phases may be brief. For complex bugs, each phase may require significant investigation.

Always complete all 8 phases. Skipping phases leads to incomplete fixes and regressions.
