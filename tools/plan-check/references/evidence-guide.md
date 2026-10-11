# Evidence guide: where evidence lives in a plan package

Eval bundles are frozen evidence: use their text only, even when the
source names a real GitHub issue. In live mode, read the issue body and
thread, relevant linked contribution documents, and the submitted plan
and comment. The reproduction source is the student's posted week-2
report; for a house issue it is the repro pack quoted in the drafts.
Do not supplement drafts with unquoted local files. Missing necessary
evidence is recorded for the rubric rather than supplied by guessing.

## Diagnosis and grounding

**Where it lives:** In an eval bundle, compare `Candidate plan`'s Cause,
Diagnosis, or proposed change with `Issue`, `Thread highlights`, and
`Repro evidence`'s steps, controls, artifacts, and timings. In live mode,
compare the draft cause with the issue/thread and the applicable repro
report quoted or posted on the issue.

**What good looks like:** The cause explains the actual failure and its
controls, and the change addresses that mechanism. In `calib-03`, the
25.8-second highlighted run with no pager and 0.2-second uncolored run
contradict blaming pager key bindings, even though a thread participant
asserts that cause. A named cause is not enough.

## Scope

**Where it lives:** In `Candidate plan`, find Change, Scope, in/out
statements, and affected files or areas; compare them with `Issue` and
`Repro evidence`. In live mode use the corresponding passages of the
draft `plan.md` against the scoped issue and repro report.

**What good looks like:** One identifiable fix has clear boundaries;
necessary tests or documentation can support that fix without becoming
unrelated work. `calib-01` adds the commits context to the successful-push
refresh and excludes changes to push-status computation and other views.
A precise file list or separate scope heading is not the goal.

## Executability

**Where it lives:** Read the candidate plan's approach, numbered changes,
implementation locations, callbacks, and dependencies; use repo facts
and thread constraints for any explicitly required workflow. In live
mode find the same details in the submitted plan and relevant repository
documents.

**What good looks like:** A contributor can identify a starting point
and intended operation. `calib-01` names the sync controller's push
completion callback and the context to add to its refresh scope;
`calib-02`'s promise to poke around editor components leaves the approach
undecided. Do not require exact line numbers or completed implementation.

## Test plan

**Where it lives:** Compare the candidate plan's Test or Test plan with
`Repro evidence`'s trigger, steps, controls, and expected/actual results.
In live mode compare draft verification steps with the student's repro
comment or the quoted house pack; check relevant regression paths named
by the proposed change.

**What good looks like:** The actions can be run and their observable
result distinguishes the bug from a fix. `calib-01` reuses the repro steps
and requires the pushed color at step 3 without leaving the view, plus
checks other paths sharing the callback. Manual checks can pass; a full
suite command alone, as in `calib-04`, does not show the cwd-dependent
glob failure is fixed.

## Honesty

**Where it lives:** Read causal claims, risks, assumptions, unknowns,
certainty, promises, and any deviation notes across both candidate plan
and comment; compare them with the repro and thread. In live mode look
for recorded changes and reasons in the updated submitted plan when
regrading a deviation, not only in an implementation diff.

**What good looks like:** Confidence matches the evidence, and material
unknowns have a bounded verification step rather than being concealed
or replacing the approach. Do not infer dishonesty merely because there
is no risks heading, and do not require a deviation note before any
change has occurred.

## Comms

**Where it lives:** Compare `Candidate plan comment` with `Candidate
plan`, `Thread highlights`, and `Repo facts`'s contribution policy,
explicit template asks, and AI-use requirements. In live mode use the
draft comment, issue discussion, and relevant CONTRIBUTING or linked
policy documents; apply scope's house rules and report personal voice
issues separately as directed by the skill.

**What good looks like:** The comment explains the proposed work and its
basis in the author's own submission, reflects relevant maintainer
constraints, and follows stated policies without inventing new ones.
`calib-01` acknowledges limited review bandwidth while keeping the fix
small. An empty thread needs no invented response; a classmate's plan
does not block the student's own plan under the course house rules.
