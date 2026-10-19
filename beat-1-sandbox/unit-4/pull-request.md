# Unit 4 — Test and Submit

## Your pull request

**Pull request**

Pending: PR has not been opened. Target: codepath/pathreview-ai301-fa26-s3, base main, issue #68. Replace this note with the PR's own URL after creation; this is not a completed submission yet.

**Branch**

fix/68-empty-keyword-index

## Eval iterations

**Run history**

The initial attempt had 20 execution errors because the sandbox could not access Claude's login. It produced no valid scored run and did not write eval-run.txt. After running with authenticated access, the first completed full Sonnet run scored 18/20. No rubric revisions, partial retries, or further full runs were made. The final saved transcript says: "agreement: 18/20 scored items  (bar: 18/20: PASS)". Categories matched: clear-accept 5/7, not-tested 4/4, silent-drift 4/4, standards-wall 2/2, unreviewable 3/3. Codex authored the skill and executed these runs with AI assistance.

**Package analysis**

pkg-08: the rubric run returned reject; the gold label was accept. Standards and communication failed because the grader interpreted "plan posted on the thread" as contradicted by the thread highlights. The package's Plan context explicitly says: "The accepted plan this PR claims to implement, excerpted from the posted plan (with the repro evidence it built on):". The description says "(#5883, plan posted on the thread)". The run overtreated the limited thread highlights as exhaustive evidence against that supplied plan context. The implementation and behavior proof passed the other checks. I retained this false rejection in the saved 18/20 run rather than claiming a perfect result.

**Check rationale**

The uploaded rubric contains this exact table row:

| Plan fidelity | Plan context's scope, approach, exclusions and deviations beside the complete diff and description's implementation claims. | The diff implements the accepted plan within its boundary, or material changes/omissions are explicitly disclosed with what changed and why and remain a bounded response to the issue. Description claims match what the diff actually delivers. Necessary supporting edits need no separate deviation when consistent with the plan. Silent additions, silent omissions, and claims of unchanged behavior contradicted by the diff fail. | required |

This adapts Unit 3's scope and honesty checks to the actual diff. I chose to allow explicit, reasoned deviations rather than reject every departure from the original plan, while retaining a hard boundary against silent additions, omissions, or misleading claims. The row was not revised after the completed eval run.

**Trade-offs**

The evidence requirements favor verifiable readiness but can overreject terse evidence. pkg-19 is the second false rejection: the package says "Controls
(double-quoted twin; single-quoted without the trailing blank line)
unchanged." The grader rejected Behavioral evidence because these controls had no commands/output, although the original before/after proof and suite results were present. I retained this stricter result for this iteration. No checks were loosened, so there was no loosening canary run. The complete run still matches every rejection category (including both standards-wall packages), while accepting 5 of 7 clear-accept packages. These limits explain the two misses rather than conceal them.
