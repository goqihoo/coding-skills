---
name: small-fix
description: Make a small, localized code fix with one durable regression guard and proportional verification.
---

# Small Fix

A small fix is a **tight patch**: one observable defect, one public seam, one durable guard, one minimal change.

## Bound the fix

Before editing, name:

- the exact user-visible or externally observable defect;
- the narrowest public seam that should prove the behavior;
- the tight command that can go red on this defect.

Treat an explicit acceptance statement from the user as agreement on the seam. If several seams are plausible, confirm which behavior is the contract before writing a test.

Upgrade the flow when the work stops being small:

- Use `/diagnosing-bugs` when the cause is unclear, intermittent, performance-related, or resists the first tight loop.
- Use `/implement` when the fix expands into broad or coupled behavior, an architectural refactor, a cross-process or security boundary, persistence or migration logic, destructive file operations, provider protocols, or full delivery work.

## Run one red-green loop

1. Reproduce the defect through the narrowest existing test or feedback surface.
2. Add one regression guard at the public seam. Prove it goes **red because of this defect**, and keep the loop to this one tracer-bullet slice.
3. Make the smallest production change that turns the guard green. Leave adjacent cleanup for a separate task unless it is required to expose the correct seam.
4. Rerun the exact red test, then the nearest cheap check affected by the change, such as the touched test file, typecheck, lint rule, or existing visual/accessibility contract.
5. Stop when the stated behavior is protected and the tight checks pass.

For copy or visual-only polish with no meaningful automated public seam, use the nearest existing screenshot, accessibility, localization, or component contract. Prefer an explicit verification gap over a brittle assertion against implementation details.

## Keep verification proportional

Stay in the current context and run targeted checks by default. Run the full suite, app-level regression, packaging, review agents, or commit flow only when the user asks, the repository explicitly requires that relevant layer, or the tight check cannot establish confidence.

If broader verification fails for an unrelated reason, report it separately; do not expand the fix to absorb unrelated work.

## Hand off

Report:

- the behavior fixed;
- the regression guard added or the reason no durable guard was appropriate;
- the exact checks that passed;
- broader checks deliberately deferred;
- any evidence that the work should be upgraded to another Matt flow.
