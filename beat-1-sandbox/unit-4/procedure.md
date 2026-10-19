# Procedure: how this tool grades a PR package

## Read order

1. Identify live or eval mode. In live mode read scope.md first and stop without grading for a placeholder or out-of-scope repo. In eval mode ignore scope and personal voice; the bundle alone supplies evidence.
2. Read the rubric, this procedure, and evidence guide. Refuse empty authored checks or procedure. In live mode read voice-guide.md for the outgoing-text review.
3. Read issue, thread and repo standards; record expected behavior, relevant constraints, required checks, template asks and AI policy. Read the repro and accepted plan before the candidate claims so the proposed scope anchors the comparison. Record planned behavior, boundaries, tests, and deviations.
4. Read every commit and diff hunk, then the title and description and all test evidence. In live mode gather the exact inputs and committed diff named by SKILL.md. Missing or inaccessible evidence remains a recorded gap; do not replace committed changes with working-tree changes.

## Evidence gathering

1. Use the evidence guide's four families. For Plan fidelity, pair each material planned behavior with the implementing hunks; list additions and omissions and pair each with any deviation explanation. Compare each material title/description claim against the diff, especially promises of unchanged behavior.
2. For Behavioral evidence, pair each repro trigger and planned test/control with the reported command or manual action, expected result, actual before/after and any limitation. Distinguish executed observations from proposed tests. Check whether the remaining proof actually demonstrates the behavior when a check is incomplete.
3. For Repository checks, list each explicitly required applicable check and its reported outcome, failure explanation, or concrete reason for omission. Keep an honest failure separate from absent evidence and from an unsupported success claim.
4. For Reviewable diff, inspect all hunks and commits for the fix, supporting edits, unrelated changes, debug prints, dead/commented-out code and formatting churn. Cite actual hunks, not a favorable description of them.
5. For Standards and communication, pair every stated template/policy ask and relevant maintainer constraint with the text satisfying or ignoring it. In live mode also record personal voice violations separately. An empty thread or absent policy creates no extra requirement.
6. Record source section and deciding quote/fact for every row. If a necessary fact cannot be found in its mapped sources, name the missing fact. Do not fetch outside an eval bundle or infer a successful run from a test's existence.

## Check execution

1. Grade all rows in order: Plan fidelity, Behavioral evidence, Repository checks, Reviewable diff, Standards and communication. Reuse gathered pairings; reread relevant sections when needed rather than inventing requirements.
2. Apply each complete pass condition to substance. A known contradiction or unmet condition is fail; missing necessary evidence is unclear; satisfied conditions are pass. Do not fail merely for brevity, lack of automation, absent optional sections, or honestly reported limitations that meet the row's condition.
3. For every check record its exact name, grade and one-line source-backed deciding fact. Do not stop after a failure or relax a row because other checks pass. Report procedure gaps instead of inventing steps; if a gap prevents verification of a required condition, grade it unclear.

## Verdict assembly

1. Apply the verdict rule: all required pass means accept; any required fail or unclear means reject. Preferred results never change it.
2. Summarize every check with its deciding evidence. For a reject lead with the first non-passing required check in rubric order, then mention other required holds. Report live personal voice violations separately; they do not independently gate this rubric.
3. Use the bundle ID for eval item; for live use the PR URL if available, otherwise the supplied issue URL identifying the draft. Emit every check once in order.
4. End with the exact fenced JSON schema from SKILL.md, valid JSON and no following text. Grading does not post, modify code, or open a PR.
