# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of the claim and reproduction for issue #68 and the evaluation runs that produced `eval-run.txt`.

Status: draft. The identity and posted-comment fields need verified upstream information. The eval fields below are complete from the saved artifacts. Issue #68 was reproduced in a clean sandbox at commit `2f4e82f52efbcfcc57d65b3fa5348672163ca088`; the local report is `repro-report.md`. Its posted permalink and exact posted text are still pending.

---

## Your identity upstream

**GitHub username**

https://github.com/qingtaozhou/

---

## Posted upstream

**Claim comment**

Pending — paste the claim comment's own permalink, then copy its exact posted text underneath. The accepted local draft remains in `../../claim.md`, and live grading is in `../../claim-grade.txt`; neither proves that a comment was posted.

**Reproduction comment**

Pending — paste the reproduction comment's own permalink, then copy its exact posted text underneath. The actual tested environment, code state, repeatable steps, and captured results are documented in `repro-report.md`. Live full-package grading returned `accept`, with all eight checks passing; see `repro-grade.txt`. Do not treat that local report as posted text until it has been posted and copied back from GitHub.

## Eval iterations

**Run history**

The runs occurred in this order, using Sonnet and the installed canonical rubric and evidence guide:

1. Initial full run: **17/20**. `eval/results-initial.json` records `"agreement": [17, 20]`. Command: `sh run_canonical_eval.sh --out results-initial.json`.
2. Targeted rerun after revisions: **4/4**. `eval/results-revised.json` records `"agreement": [4, 4]`. Command: `sh run_canonical_eval.sh --only pkg-05,pkg-09,pkg-10,pkg-20 --out results-revised.json`. This partial score is not a full-run passing result.
3. Confirming full run: **20/20**. Command: `sh run_canonical_eval.sh --save-run eval-run.txt --out results-final.json`. The last agreement line, quoted exactly from the harness-written `eval-run.txt` in this directory, is:

```text
agreement: 20/20 scored items  (bar: 18/20: PASS)
```

There were two full runs and one four-package targeted run. The transcript was copied byte-for-byte into this directory; it was not hand-edited. The files in `tools/repro-check/` are a submission snapshot of the installed canonical skill. The rubric, evidence guide, and entrypoint fingerprints match the final transcript.

**Package analysis**

I examined **pkg-10**. In the initial run the rubric decided **reject**, while the gold label was **accept**. The initial JSON identifies `outcome-evidenced` as the failed check and gives this exact evidence:

> Prompt shows the resolved physical path and the report admits PWD was not logical, so the issue's trigger was not exercised; the successful render does not show the symptom absent.

The candidate report starts with this text from `eval/packages/pkg-10.md`:

> Result: cannot reproduce on Linux + zsh with the report's exact layout
> and config. What I ran and what differed from the report's environment
> is below.

It also shows the prompt output:

```text
monorepo/packages/app-dir on  master
```

The initial rule required the issue's failure preconditions to be achieved even for an honest failed attempt. That made the grader treat the disclosed Linux/zsh versus macOS/fish difference as insufficient evidence. The report actually includes a relevant attempt, its successful rendering result, and explicit limitations; it does not claim the bug is absent everywhere. After revising that distinction, the targeted run and final full run both accepted pkg-10, matching gold.

**Check rationale**

Here is the complete `outcome-evidenced` row quoted exactly from the submitted `tools/repro-check/rubric.md`:

```markdown
| outcome-evidenced | Repro report's output, logs, screenshots or concrete observation record compared with the issue's expected and actual behavior; Behavior shown in the evidence guide. | Evidence establishes what happened when the relevant trigger was tested. A claimed reproduction shows the issue's distinguishing behavior, not merely any error or adjacent failure. An honest cannot-reproduce report passes when a concrete relevant attempt and its results are shown and differences or unachieved preconditions are stated. It need not prove the exact failure preconditions were achieved; it must limit its conclusion to the attempt, without claiming the bug is absent generally. Bare assertions or inaccessible local artifacts are insufficient. | required |
```

I revised this check after the false rejections of pkg-09 and pkg-10. It still requires a claimed reproduction to show the issue's distinguishing behavior, so a syntax error cannot establish a reported panic. I rejected the requirement that an honest cannot-reproduce report must prove every failure precondition was reached. The revised check accepts concrete, relevant failed attempts when the author states the limitations and confines the conclusion to that attempt.

**Trade-offs**

This revision accepts useful negative findings whose environment or suspected preconditions differ from the reporter's. It gives up certainty that the exact failing path was reached; acceptance therefore means the limited report is ready to post, not that the original bug is disproved. For example, the pkg-10 output above supports a Linux/zsh result only.

The revisions also allowed reconstructible fixtures and substantive diagnostic summaries in follow-up comments. To check that this flexibility did not erase an explicit disclosure requirement, I included pkg-20 as a canary in `--only pkg-05,pkg-09,pkg-10,pkg-20`. The targeted result kept pkg-20 at reject, matching its reject gold label. Its `repo-conventions` evidence is quoted exactly from `eval/results-revised.json`:

> AI_POLICY requires disclosure of all AI usage (tool and extent); neither comment contains a disclosure or a statement of no AI use, so compliance cannot be verified.

The confirming full transcript shows that all categories still matched:

```text
categories: clear-accept 8/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4
```

These checks were revised using this eval set, so overfitting remains a limitation. The full rerun checks for regressions in these 20 frozen packages; it does not establish reliability on every live issue.
