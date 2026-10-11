# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis | Candidate plan's cause and approach, compared with Issue, Thread highlights, and Repro evidence (including controls, timings, and artifacts). | The proposed cause explains the reproduced failure and relevant controls without contradicting them. The change addresses that cause rather than merely hiding the symptom. A thread claim alone does not outweigh contrary reproduction evidence. | required |
| Scope | Candidate plan's change, boundaries, and affected areas, compared with the issue and reproduction. | The work is one bounded fix for the reproduced problem. Its affected areas and limits are clear enough to distinguish necessary supporting work from unrelated changes. Exact filenames and a separate out-of-scope heading are not required when the boundary is otherwise clear. | required |
| Executability | Candidate plan's approach, implementation locations, and sequence; repo facts and thread constraints where relevant. | Another contributor can identify where to start and what change to attempt without first inventing the diagnosis or approach. Concrete areas or callbacks can suffice; promising to investigate broadly and fix it later does not. | required |
| Test plan | Candidate plan's tests, compared with Repro evidence's triggering steps, expected/actual results, and relevant controls. | The plan specifies a runnable manual or automated check of the original failure with an observable expected result after the fix. It also checks relevant neighboring behavior or controls when the proposed change could affect them. Referring to the reproduced steps is sufficient when those steps and the changed expected outcome are clear; an automated test or full-suite command alone is insufficient. | required |
| Honesty | Candidate plan and comment's causal claims, risks, unknowns, promises, and any recorded deviations, compared with reproduction and thread facts. | Claims do not overstate what the evidence establishes. Material unknowns are identified with a bounded way to resolve them; they do not replace an executable approach. Any stated deviation explains what changed and why. Do not demand a risks section or deviation note when none is relevant. | required |
| Comms | Candidate plan comment compared with the plan, Thread highlights, and Repo facts' contribution policies and explicit asks. | The comment communicates the proposed fix and its basis accurately, respects relevant maintainer constraints and stated contribution or AI-use policies, and does not contradict the plan or promise unwarranted certainty. No reply to an empty thread or unstated disclosure policy is required. | required |

## Verdict rule

Return `accept` (ready) only when every required check is `pass`. Return
`reject` (hold) when any required check is `fail` or `unclear`.
A `?` is reported as `unclear` and counts as a fail for this rule.
Preferred checks, if added later, never change the verdict. Grade every
check even after a required failure; do not use a score or majority vote.
