# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

Eval: read Plan context (repro, approach, scope, exclusions, test plan and any deviation notes) beside Candidate PR → Diff, Commits and Description. Live: read plan.md including ## Deviations and the issue thread beside `git diff main...HEAD`, `git log main..HEAD` and pr_draft.md.

Good: each material addition or omission is within the accepted boundary or explicitly explained as a deviation with its reason. Claims about implemented or unchanged behavior agree with the hunks. A necessary supporting edit need not have been named as an exact filename; an unacknowledged behavior change or missing planned behavior is silent drift. An honest, bounded reduction can pass; claiming full fidelity while delivering less cannot.

## Test evidence (harness category: not-tested)

Eval: compare Plan context's reproduction and Test plan with Candidate PR → Test evidence and Description's testing claims; find required commands in Repo facts and thread instructions. Live: compare plan.md and the issue's posted repro (or supplied house repro pack) against test_evidence.md and pr_draft.md; read the target repo's PR template and docs/CONTRIBUTING.md for required checks.

Good: runnable actions and observed before/after results demonstrate the original behavior and relevant controls, and repo check outcomes are visible. Command output, a concrete manual observation or other reproducible artifact can prove behavior; “tests pass” alone cannot. Reported failures and concrete blocked-check reasons are evidence, not automatic rejection. A skipped optional smoke check need not erase decisive repro proof; a limitation that leaves no observable proof does not pass merely because it is disclosed. Repository-check evidence and behavior-specific proof are distinct requirements.

## Diff quality (harness category: unreviewable)

Eval: inspect every Candidate PR → Diff hunk and the Commits list against Plan context and the issue; the description cannot substitute for reading them. Live: inspect the full committed `git diff main...HEAD` and `git log main..HEAD`, comparing with plan.md. Uncommitted work is outside the graded branch diff.

Good: the fix and necessary supporting tests/docs are easy to isolate, with no debug leftovers, dead or commented-out implementation, unrelated formatting churn or drive-by edits. Judge actual relevance and reviewer burden, not raw line count or number of commits. Explaining unrelated debris in the description does not remove it.

## Standards and comms (harness category: standards-wall)

Eval: Repo facts states template asks, contribution instructions and any AI-use policy; Thread highlights supplies relevant maintainer direction. Compare these with Candidate PR → Title and Description. Live: read the issue's whole thread, target .github/PULL_REQUEST_TEMPLATE.md and docs/CONTRIBUTING.md against pr_draft.md; scope.md supplies the course house rules and voice-guide.md supplies separate personal feedback.

Good: each stated section contains substantive applicable content or a reasoned N/A, issue linkage and disclosures meet the stated requirements, and maintainer constraints are respected. No policy means no invented disclosure requirement in eval. In live Path Review, include the course's AI-use disclosure in Notes for Reviewers. Compare description-versus-diff claims under Plan fidelity; report personal voice separately without changing this rubric's verdict.
