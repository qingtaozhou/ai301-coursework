# Procedure: how this skill grades a plan package

## Read order

1. Identify live or eval mode. In live mode, read `scope.md` first, confirm the issue belongs to its repository, and record the house rules. Stop without grading if scope is unfilled or the issue is outside it. Eval mode ignores scope and uses only the supplied bundle, without browsing or fetching.
2. Read `rubric.md` and `references/evidence-guide.md`; list the checks, weights, and verdict rule. Stop if checks or procedure steps are empty. In live mode also read `voice-guide.md` for the later comment review.
3. Read the issue and thread highlights, then repo facts. Record the reported failure, expected behavior, relevant maintainer direction, and contribution constraints.
4. Read the reproduction evidence before the candidate plan. Record the trigger, actual and expected outcomes, artifacts, and controls. This anchors diagnosis in observed behavior before the proposed explanation can influence the grade.
5. Read the entire candidate plan and then its draft comment, noting cause, boundaries, implementation approach, tests, unknowns, and any deviations. Grade the complete package in both modes; there is no claim-only exemption.

## Evidence gathering

1. Use the guide's locations for each rubric row. In eval mode cite section names and short quotes or concrete facts from the bundle. In live mode gather the issue body/thread and relevant repo documentation; use the student's posted reproduction comment, or the house repro evidence quoted in the drafts. Treat drafts as what they contain or quote, without filling gaps from other working files.
2. For Diagnosis, put the claimed cause and fix beside the reproduction's failure and each relevant control. Record any fact that supports or contradicts the cause, distinguishing thread speculation from observed results.
3. For Scope and Executability, extract the targeted areas, proposed operations, limits, and work sequence. Compare the work to the reproduced issue and record unrelated expansion or a missing actionable starting point.
4. For Test plan, extract the commands or manual actions, triggering inputs, and expected observable result. Match them to the original reproduction and relevant controls or neighboring paths affected by the change.
5. For Honesty, compare confidence, assumptions, unknowns, promises, and recorded deviations with the evidence already collected. Record unsupported certainty or how a material unknown will be resolved.
6. For Comms, compare the comment with the actual plan, relevant thread requests, and stated repo policies. Record any mismatch or ignored constraint. An empty thread or absence of a policy does not create a requirement.
7. If a fact needed by a check cannot be found after reading its mapped locations, record which fact is absent. Do not invent evidence or fetch outside an eval bundle.

## Check execution

1. Run every rubric row in table order: Diagnosis, Scope, Executability, Test plan, Honesty, Comms. Use gathered evidence; reread only the relevant sections if a comparison needs clarification.
2. Apply the row's stated pass condition to the substance, not headings, length, tone of confidence, or the mere presence of a cause, filename, or automated test. Check the plan and comment together wherever the row names both.
3. Grade `pass` when the available evidence satisfies the complete condition. Grade `fail` when evidence shows a contradiction, inadequate approach, unrelated expansion, ineffective test, unsupported claim, or policy mismatch under that row.
4. Grade `unclear` (the worksheet's `?`) when a necessary fact is genuinely missing or ambiguous after looking in the mapped locations. A known bad outcome is `fail`, not `unclear`. A missing optional section is not itself a failure.
5. Record each check's exact name, grade, and one-line deciding quote or fact with its source section. Never stop early after a failure, invent additional requirements, or override a passing condition with intuition. Report any procedure gap in the summary.

## Verdict assembly

1. Apply the rubric's verdict rule: all required checks must pass for `accept`; any required fail or unclear produces `reject`. Preferred checks never change this decision.
2. Before the machine result, optionally summarize grades and the deciding evidence, including which required failures or unknowns caused the hold. In live mode also quote any violated voice-guide rule; voice notes do not independently change the verdict because the rubric does not grade personal voice.
3. Set `item` to the eval bundle ID or live issue URL. Emit every check once, using its rubric name and `pass`, `fail`, or `unclear`, plus the one-line evidence.
4. Finish with a valid fenced JSON block containing `item`, `checks` (objects with `name`, `grade`, `evidence`), and `verdict` (`accept` or `reject`). Write nothing after that block. Do not post a comment or implement a fix as part of grading.
