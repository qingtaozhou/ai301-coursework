# Contribution: Implement TRIX (Triple Exponential Average) oscillator and signal line

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Qingtao Zhou
**GitHub Username:** qingtaozhou
**Issue:** https://github.com/huuan26/polars-anta/issues/20
**Pull Request:** not opened yet

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built and refined issue-scout, then graded three contribution picks**

On 2026-10-25 I built my issue-scout search strategy around three Python data-tool queries and ranking filters, then graded the top five results; all five failed availability because of existing PRs or recent claims, and four came from one repository. I added `-linked:pr` to the queries, capped the top five at two issues per repository, and updated the contribution-policy check to inspect organization-level `.github` policies after finding that a repository's AI-disclosure rules lived there. On 2026-11-06 I used Codex to apply my saved rubric to three Issue Selection picks: [python/pythondotorg#2646](https://github.com/python/pythondotorg/issues/2646) and [pytorch/executorch#10580](https://github.com/pytorch/executorch/issues/10580) were accepted, while [DIGI-UW/OpenELIS-Global-2#3243](https://github.com/DIGI-UW/OpenELIS-Global-2/issues/3243) was rejected because of an unresolved October 28 claim. The direct grades showed that acceptance does not establish practical fit—the Python.org fix needs a CMS editor and may not produce the required PR, while ExecuTorch involves C++ and Qualcomm testing—so I saved the evidence and these limitations in my scan output and dated notes, left the rubric unchanged, and kept my final issue choice pending.

**Unit 6: Installed the voice guard and distilled local repo memory**

I merged my carry-over voice rules into one canonical guide, added claims/questions/pings rules, installed the global Claude Code hook, and verified that the wiring test blocks a body-less comment command. The first real claim passed repro-check but the voice guard stopped its report-back date as a premature deadline, so I revised it to explain the source investigation already completed and distinguish an investigation update from implementation completion. A scoped Claude orientation became a 41-line `CLAUDE.local.md` importing `AGENTS.md`; I verified that `.git/info/exclude` keeps the memory out of my PR. Moving the temporary checkout broke the editable environment, so I installed a fresh `.venv` in the persistent fork instead of relying on the temporary path.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I chose [polars-anta #20](https://github.com/huuan26/polars-anta/issues/20), which asks for a TRIX oscillator and EMA signal line using Polars expressions. My earlier scout grades covered python/pythondotorg#2646, pytorch/executorch#10580 and DIGI-UW/OpenELIS-Global-2#3243: the patched rubric accepted the first two with ambitious notes and rejected OpenELIS for availability, but all three had prior work requests, so I released my course-site reservations. I then reused my saved Python/data-tool queries for discovery (195 unique issues, 71 within the ranking window) and checked threads and timelines before choosing a candidate for direct grading. This was a targeted selection, not a completed top-five graded scan. Claude's direct scout grade accepted #20 with a **moderate** difficulty note: the formula and locations are specified, but implementation, exports, both namespaces, tests and documentation span several files. It had no comments, assignees or implementation PRs at the availability check, the feature was still absent, and the maintainer explicitly invited claims.

This fits my Python/data-tools profile better than a CMS edit or Qualcomm C++ runner. I want to learn how to turn a specified calculation into a native dataframe expression and verify it on grouped data, including null and zero-price edge cases. The scout helped separate fit from availability, but its 30-day claim window accepted two issues that my course's stricter rule treated as taken, and zero comments alone missed work linked through PRs on other candidates. I kept those differences visible rather than silently changing verdicts. On 2026-11-06 I replaced **Newcomer scope** with **scope-feasible**, so a single identifiable task can pass with a difficulty note instead of being rejected for every open edge; future refinement should also make old-claim handling and already-implemented work more explicit. I used Codex and Claude Code to gather evidence and draft this account.

**Claim comment:** https://github.com/huuan26/polars-anta/issues/20#issuecomment-6699580403 (posted 2026-11-06 through Claude Code; voice guard passed). My report-back commitment is November 9, 2026.

**Toolkit**

- Tool: issue-scout, with my saved Python/data-tool queries, patched rubric and direct Claude grading after availability screening.
- What it produced: accepted polars-anta#20 with a moderate difficulty note and explicit contribution-policy obligations; the full read-out is saved locally in scan-output.md.
- Difficulties: prior claims can outlive the rubric's 30-day window; zero-comment issues can already have PRs or be implemented. Acceptance does not establish personal fit.
- What changed: replaced Newcomer scope with scope-feasible and added difficulty notes outside verdict JSON; checked full threads, timelines, PR search and current code before choosing.

---

## Understanding the Issue

**Problem Description**

The library lacks the TRIX oscillator and its signal line requested in #20. This is a missing-feature investigation, not a claim that an existing TRIX implementation computes the wrong values.

**Expected Behavior**

`trix(close, period=15, signal_period=9)` returns a Polars Struct expression with `trix` and `signal` fields. TRIX is the one-bar percentage change of a triple EMA; the signal is its EMA. It must support grouped execution, top-level exports and the expression/DataFrame/LazyFrame namespaces, including unnesting.

**Current Behavior**

At upstream commit `8c593b8fc2a9859d370355c70a95b5bd2963b0de`, the requested entry points are absent. Calling the top-level API raises AttributeError; an existing grouped EMA runs successfully on the same fixture.

**Affected Components**

`src/polars_anta/momentum.py`, `trend.py` (EMA helper), `namespace.py`, and `__init__.py`; tests live in `tests/test_momentum.py`, `test_namespace.py` and `test_dataframe_namespace.py`.

**Toolkit**

- Tool: one scoped Claude Code orientation and source inspection.
- What it produced: the four main integration files, related test patterns and existing EMA/Struct conventions.
- Difficulties: zero-denominator/null behavior needs a deliberate decision; current EMA seeding must not be assumed to match TA-Lib.
- What changed: recorded these boundaries in local memory rather than mapping the whole repository or promising numerical parity.

---

## Reproduction Process

**Environment Setup**

- Upstream: huuan26/polars-anta, master commit `8c593b8fc2a9859d370355c70a95b5bd2963b0de` (package metadata 0.3.1).
- macOS 26.6.2, Apple Silicon arm64; CPython 3.11.15.
- Polars 2.1.0; NumPy 2.4.6; installed editable from the checkout in a fresh virtual environment.
- The issue does not name an OS or dependency version and supplies a proposed function signature, not a runnable failure example. I used a small synthetic two-ticker dataframe to check the requested public entry points. This does not test financial accuracy or the proposed implementation's edge cases.
- Setup completed successfully; the existing grouped EMA expression runs as a control.

**Steps to Reproduce**

From a new working directory:

```bash
git clone https://github.com/huuan26/polars-anta.git
cd polars-anta
git checkout 8c593b8fc2a9859d370355c70a95b5bd2963b0de
python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install 'polars==2.1.0' 'numpy==2.4.6'
python -m pip install -e '.[dev]'
```

Save the following as `reproduce_trix.py` and run `python reproduce_trix.py`:

```python
import importlib.metadata as md
import platform
import polars as pl
import polars_anta as ta
from polars_anta import momentum

print('Python:', platform.python_version())
print('Platform:', platform.platform())
for name in ['polars-anta', 'polars', 'numpy']:
    print(name + ':', md.version(name))
df = pl.DataFrame({'ticker': ['A'] * 4 + ['B'] * 4,
                   'close': [100., 101., 99., 102., 50., 51., 49., 52.]})
print('EMA control:', df.select(ta.ema('close', period=2).over('ticker')).shape)
checks = {
    'top-level polars_anta.trix': hasattr(ta, 'trix'),
    'momentum.trix': hasattr(momentum, 'trix'),
    'expression .anta.trix': hasattr(pl.col('close').anta, 'trix'),
    'expression .ta.trix': hasattr(pl.col('close').ta, 'trix'),
    'DataFrame .anta.trix': hasattr(df.anta, 'trix'),
    'LazyFrame .ta.trix': hasattr(df.lazy().ta, 'trix'),
}
for name, present in checks.items():
    print(name + ':', 'present' if present else 'MISSING')
try:
    ta.trix('close', period=15, signal_period=9)
except AttributeError as exc:
    print('Requested API call:', type(exc).__name__ + ':', str(exc))
print('Feature gap confirmed:', not any(checks.values()))
```

**Reproduction Evidence**

- **Commit showing reproduction:** none
- **Screenshots/logs:** terminal output included below; the upstream commit identifies the version tested, not a reproduction commit in my fork.
- **My findings:** the requested API is absent on the tested commit, while an existing grouped EMA evaluates successfully.

Expected: the issue requests `trix(close, period=15, signal_period=9)` returning a Polars Struct expression with `trix` and `signal` fields, top-level export, namespace integration, grouped execution and unit tests.

Observed output:

```text
Python: 3.11.15
Platform: macOS-26.6.2-arm64-arm-64bit
polars-anta: 0.3.1
polars: 2.1.0
numpy: 2.4.6
EMA control: (8, 1)
top-level polars_anta.trix: MISSING
momentum.trix: MISSING
expression .anta.trix: MISSING
expression .ta.trix: MISSING
DataFrame .anta.trix: MISSING
LazyFrame .ta.trix: MISSING
Requested API call: AttributeError: module 'polars_anta' has no attribute 'trix'
Feature gap confirmed: True
```

The successful EMA control confirms the package imports and evaluates an existing indicator on this input. TRIX is missing from the module, top-level API and the checked expression/frame namespaces, and the proposed top-level call raises AttributeError. This establishes the missing API on this commit; it does not prove behavior on all versions or validate any future TRIX values, null handling, namespace unnesting or grouped implementation.

Next, I will write numerical examples from the issue's formula and compare the existing EMA/Struct conventions before implementing TRIX. The checks still needed include zero/null denominator behavior, grouped execution and namespace parity. No fix has been implemented.

I used Codex to prepare and execute this investigation and Claude Code to grade the draft.

**Toolkit**

- Tool: repro-check via Claude Code, applied first to the claim and then to the complete claim/report pair.
- What it produced: the initial claim-only grade accepted; full-package grading confirmed the environment, input, rerunnable steps and missing-feature evidence, but initially held the report on communication quality. After revision, the complete package passed all eight required checks on 2026-11-06.
- Difficulties: the initial report ended with course-status text and omitted the next investigation step; the first claim's report-back date also triggered the separate voice guard.
- What changed: removed course-status boilerplate from the report, added a concrete next step, and revised the claim to distinguish an investigation update from a fix estimate. Kept the output and version limits explicit; the report stays in the course story and is not posted on the issue.

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
