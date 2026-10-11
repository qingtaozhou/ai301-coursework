# Plan: handle an empty keyword index (#68)

Issue: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68

Fork: https://github.com/qingtaozhou/pathreview-ai301-fa26-s3
Clone: `~/Desktop/CodePath/qingtaozhou-pathreview-ai301-fa26-s3`

## Reproduction evidence

Evidence source: the saved Unit 2 report at
`~/Desktop/ai301-unit2-starter/repro.md`. That report was never posted
on #68; my only thread comment so far is the 2026-10-04 claim saying I
had not reproduced it yet. The plan comment therefore includes the facts
below directly, so thread readers can see the basis for the plan.

> Result: reproduced `ZeroDivisionError` from `KeywordSearcher.index([])`.

Tested code state: `2f4e82f52efbcfcc57d65b3fa5348672163ca088`;
macOS 26.6.2 arm64, Python 3.11.15, PathReview 0.1.0,
rank-bm25 0.2.2, NumPy 2.4.6, structlog 26.1.0, pytest 9.1.1.
The report records this direct command:

```sh
.venv/bin/python -c 'from rag.retriever.keyword_search import KeywordSearcher; KeywordSearcher().index([])'
```

Its captured trace includes:

```text
rag/retriever/keyword_search.py:25: self.bm25 = BM25Okapi(tokenized_corpus)
rank_bm25.py:52: self.avgdl = num_doc / self.corpus_size
ZeroDivisionError: division by zero
```

The report quotes the expected result:

> Empty-corpus indexing completes without raising; subsequent keyword search on the empty index returns `[]`.

It also records the existing regression run:

```sh
.venv/bin/python -m pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index --runxfail -v --tb=short
```

> 1 failed in 0.58s

With the xfail marker honored, the file had `16 passed, 1 xfailed`.
The control `KeywordSearcher().search("python")` before indexing
returned `[]`. These are previous observed results, not new test runs.

## Diagnosis

`KeywordSearcher.index` stores the chunks, tokenizes them, and constructs
`BM25Okapi` unconditionally. An empty list becomes an empty corpus;
rank-bm25 divides by its zero corpus size while constructing the index.
This matches the captured traceback. `search` already returns `[]`
when no BM25 model or chunks are present, so the missing behavior is
an empty-input path in `index`, not a scoring or search change.

## Scope and files

One bounded fix: make `index([])` leave the searcher in a valid empty
state without constructing BM25. This must also work after a nonempty
index has previously been built.

Files to change:

- `rag/retriever/keyword_search.py`: add the empty-input path.
- `tests/unit/test_keyword_search.py`: remove #68's strict xfail marker
  and add lifecycle regression coverage.

Out of scope: tokenization changes, score ordering, rank-bm25 internals
or dependency upgrades, handling nonempty lists of blank-text chunks,
other retrievers, APIs, frontend, and unrelated seeded bugs or lint
suppressions. Existing nonempty indexing and search behavior stays the
same.

## Approach

1. In the confirmed fork clone, compare these two files with the Unit 2
   code state and work on `fix/68-empty-keyword-index` from `main`.
2. In `index`, store the supplied chunks as today. For an empty list,
   explicitly set `self.bm25 = None`, log the successful empty index
   consistently with the existing index-built event, and return before
   tokenization or BM25 construction. Clearing the model prevents an old
   index from surviving a nonempty-to-empty transition.
3. Keep the existing nonempty construction and search paths intact.
4. Remove the strict xfail decorator covering `test_empty_index`, as the
   issue and contribution guide require. Retain its assertion that
   search after empty indexing returns `[]`.
5. Add a regression that builds a nonempty index, confirms search has
   results, indexes `[]`, then verifies search returns `[]`. Add coverage
   that indexing nonempty chunks again restores searchable results and
   that repeated empty indexing remains safe.

## Test plan

Use the existing documented virtual environment setup, or create one
with Python 3.11 and install editable development dependencies:

```sh
python3.11 -m venv .venv
.venv/bin/python -m pip install -e '.[dev]'
.venv/bin/python -m pip install 'rank-bm25==0.2.2' 'numpy==2.4.6' 'structlog==26.1.0' 'pytest==9.1.1'
```

First rerun the Unit 2 direct trigger after the fix:

```sh
.venv/bin/python -c 'from rag.retriever.keyword_search import KeywordSearcher; KeywordSearcher().index([])'
```

Expected: exit successfully with no division-by-zero traceback. Then
verify the observable empty-search result:

```sh
.venv/bin/python -c 'from rag.retriever.keyword_search import KeywordSearcher; s = KeywordSearcher(); s.index([]); assert s.search("python") == []; print("empty index: []")'
.venv/bin/python -m pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index --runxfail -v --tb=short
.venv/bin/python -m pytest tests/unit/test_keyword_search.py -v -rx --tb=short
```

Expected: the targeted test passes; the complete keyword-search file
passes, including lifecycle regressions, with no #68 xfail or strict
XPASS. Existing ranking, field preservation, tokenization, and top-k
checks remain green. Rerun the Unit 2 before-indexing control:

```sh
.venv/bin/python -c 'from rag.retriever.keyword_search import KeywordSearcher; assert KeywordSearcher().search("python") == []; print("before indexing: []")'
```

Expected: still `[]`. Lifecycle tests must show that old chunks are not
returned after clearing and that a later nonempty index works.

Before pushing, run the repository's required checks in its configured
environment: `make check`, `make test-unit`, and the frontend test command
from CONTRIBUTING (`cd frontend && npm ci && npm test -- --run`). Confirm
all required CI jobs, including integration tests, are green when a PR
is opened. Record any environment blocker honestly rather than claiming
unrun checks passed.

## Risks and unknowns

- An early return that forgets to clear `self.bm25` can leave stale model
  state. The lifecycle regression will verify clearing and recovery.
- Forgetting the strict xfail removal produces `XPASS(strict)` after the
  fix; remove only the marker associated with #68.
- A nonempty list containing only empty text is a different input and may
  also fail in BM25. This plan does not promise to fix that case.
- Current fork code and dependency versions may differ from the recorded
  reproduction. Compare the two files and record the build environment
  before implementing; update this plan if that changes the approach.
- The fork clone is confirmed; its keyword-search implementation matches
  the code inspected for this plan. The reproduction was never posted
  separately, so the plan comment carries the reproduction facts and
  follows up on my earlier claim. Push only to my fork.
- The local fix has now been implemented and tested; see Build validation below.
  The earlier reproduction remains historical evidence.

AI assistance: Codex read the saved Unit 2 report and local source/tests
and drafted this plan and the accompanying comment. The earlier report
attributes its automated reproduction runs to Codex, and the plan
comment says so. Review both drafts
before posting and retain an accurate disclosure of assistance.

## Build validation

On 2026-10-11, Codex ran the checks in this fork clone with its new
Python 3.11.15 virtual environment. The old reproduction environment
could not run pytest, so dependencies were installed from `.[dev]`.
No dependency declarations or lockfiles were changed.

- Direct empty-index trigger and before-indexing search control: passed.
- Keyword-search test file: 20 passed, with #68's xfail removed.
- Full unit suite: 379 passed, 52 expected failures.
- Ruff: passed; Black check: all 110 files unchanged; mypy: 76 source files passed.
- Frontend suite: 18 passed.
- Integration directory: no tests collected (pytest exit 5), which the
  repository's CI workflow explicitly handles as success.
- Fix committed as `7fe5de7` and pushed to my fork on
  `fix/68-empty-keyword-index`. No PR has been opened, so hosted PR CI
  has not been verified. Plan and comment drafts remain untracked.
- Claude's live plan-check remains blocked by its missing login; no
  `accept` verdict is claimed.

## Deviations

The implementation follows the posted draft approach: an empty-input
return clears the BM25 model, the #68 xfail is removed, and the planned
clearing, recovery, and repeated-empty tests are added. No implementation
scope or approach changed. The test environment was recreated because
the prior reproduction environment lacked pytest; this affected setup,
not the fix. This wording is a draft for my review before submission.
