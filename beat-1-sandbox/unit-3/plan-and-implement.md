# Unit 3 — Plan and Build

## Posted upstream

**GitHub username**

qingtaozhou

**Plan comment**

Pending: the posted comment permalink and exact text have not been
provided. No unposted draft is presented as a posted comment.

## Your branch

**Branch**

`fix/68-empty-keyword-index`

https://github.com/qingtaozhou/pathreview-ai301-fa26-s3/tree/fix/68-empty-keyword-index

Commit: `7fe5de7`. Only the implementation and tests are committed;
plan.md and comment.md remain untracked in the fork clone.

**Evidence**

# Before and after: issue #68

## Before: saved Unit 2 output

Commit: `2f4e82f52efbcfcc57d65b3fa5348672163ca088`.

```sh
.venv/bin/python -c 'from rag.retriever.keyword_search import KeywordSearcher; KeywordSearcher().index([])'
```

```text
Traceback (most recent call last):
  File "<string>", line 1, in <module>
  File "/private/tmp/repro-issue-68/rag/retriever/keyword_search.py", line 25, in index
    self.bm25 = BM25Okapi(tokenized_corpus)
                ^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/private/tmp/repro-issue-68/.venv/lib/python3.11/site-packages/rank_bm25.py", line 83, in __init__
    super().__init__(corpus, tokenizer)
  File "/private/tmp/repro-issue-68/.venv/lib/python3.11/site-packages/rank_bm25.py", line 27, in __init__
    nd = self._initialize(corpus)
         ^^^^^^^^^^^^^^^^^^^^^^^^
  File "/private/tmp/repro-issue-68/.venv/lib/python3.11/site-packages/rank_bm25.py", line 52, in _initialize
    self.avgdl = num_doc / self.corpus_size
                 ~~~~~~~~^~~~~~~~~~~~~~~~~~
ZeroDivisionError: division by zero
```

```sh
.venv/bin/python -m pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index --runxfail -v --tb=short
```

```text
============================= test session starts ==============================
platform darwin -- Python 3.11.15, pytest-9.1.1, pluggy-1.6.0 -- /private/tmp/repro-issue-68/.venv/bin/python
cachedir: .pytest_cache
hypothesis profile 'default'
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: /private/tmp/repro-issue-68
configfile: pyproject.toml
plugins: hypothesis-6.168.3, cov-7.1.0, asyncio-1.4.0, platformdirs-4.12.3, benchmark-5.3.0, pytest_httpserver-1.1.5, anyio-4.15.1
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collecting ... collected 1 item

tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index FAILED [100%]

=================================== FAILURES ===================================
_____________________ TestKeywordSearcher.test_empty_index _____________________
tests/unit/test_keyword_search.py:140: in test_empty_index
    searcher.index([])
rag/retriever/keyword_search.py:25: in index
    self.bm25 = BM25Okapi(tokenized_corpus)
                ^^^^^^^^^^^^^^^^^^^^^^^^^^^
.venv/lib/python3.11/site-packages/rank_bm25.py:83: in __init__
    super().__init__(corpus, tokenizer)
.venv/lib/python3.11/site-packages/rank_bm25.py:27: in __init__
    nd = self._initialize(corpus)
         ^^^^^^^^^^^^^^^^^^^^^^^^
.venv/lib/python3.11/site-packages/rank_bm25.py:52: in _initialize
    self.avgdl = num_doc / self.corpus_size
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^
E   ZeroDivisionError: division by zero
=========================== short test summary info ============================
FAILED tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index
============================== 1 failed in 0.58s ===============================
```

```sh
.venv/bin/python -c 'from rag.retriever.keyword_search import KeywordSearcher; print(KeywordSearcher().search("python"))'
```

```text
2026-10-04 20:23:26 [warning  ] keyword_search_empty_index
[]
```

## After: real changed code, 2026-10-11

Branch: `fix/68-empty-keyword-index`.

```sh
.venv/bin/python -c 'from rag.retriever.keyword_search import KeywordSearcher; KeywordSearcher().index([])'
```

```text
2026-10-11 14:08:17 [info     ] keyword_index_built            chunk_count=0
Exit code: 0
```

```sh
.venv/bin/python -m pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index --runxfail -v --tb=short
```

```text
============================= test session starts ==============================
platform darwin -- Python 3.11.15, pytest-9.1.1, pluggy-1.6.0 -- /Users/qingjiezhao/Desktop/CodePath/qingtaozhou-pathreview-ai301-fa26-s3/.venv/bin/python
cachedir: .pytest_cache
hypothesis profile 'default'
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: /Users/qingjiezhao/Desktop/CodePath/qingtaozhou-pathreview-ai301-fa26-s3
configfile: pyproject.toml
plugins: pytest_httpserver-1.2.0, platformdirs-4.13.0, cov-7.1.0, hypothesis-6.169.0, asyncio-1.4.0, benchmark-5.3.0, anyio-4.15.1
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collecting ... collected 1 item

tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index PASSED [100%]

============================== 1 passed in 0.12s ===============================
Exit code: 0
```

```sh
.venv/bin/python -c 'from rag.retriever.keyword_search import KeywordSearcher; print(KeywordSearcher().search("python"))'
```

```text
2026-10-11 14:08:18 [warning  ] keyword_search_empty_index
[]
Exit code: 0
```

```sh
.venv/bin/python -c 'from rag.retriever.keyword_search import KeywordSearcher; s=KeywordSearcher(); s.index([]); print(s.search("python"))'
```

```text
2026-10-11 14:08:18 [info     ] keyword_index_built            chunk_count=0
2026-10-11 14:08:18 [warning  ] keyword_search_empty_index
[]
Exit code: 0
```

```sh
.venv/bin/python -m pytest tests/unit/test_keyword_search.py -v -rx --tb=short
```

```text
============================= test session starts ==============================
platform darwin -- Python 3.11.15, pytest-9.1.1, pluggy-1.6.0 -- /Users/qingjiezhao/Desktop/CodePath/qingtaozhou-pathreview-ai301-fa26-s3/.venv/bin/python
cachedir: .pytest_cache
hypothesis profile 'default'
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: /Users/qingjiezhao/Desktop/CodePath/qingtaozhou-pathreview-ai301-fa26-s3
configfile: pyproject.toml
plugins: pytest_httpserver-1.2.0, platformdirs-4.13.0, cov-7.1.0, hypothesis-6.169.0, asyncio-1.4.0, benchmark-5.3.0, anyio-4.15.1
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collecting ... collected 20 items

tests/unit/test_keyword_search.py::TestKeywordSearcher::test_results_sorted_by_score_descending PASSED [  5%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_query_matching_no_documents PASSED [ 10%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_query_matching_multiple_documents PASSED [ 15%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_case_insensitive_matching PASSED [ 20%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_top_k_limit PASSED [ 25%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_top_k_larger_than_results PASSED [ 30%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_results_have_bm25_score PASSED [ 35%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_results_preserve_chunk_fields PASSED [ 40%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index PASSED [ 45%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index_clears_previous_index PASSED [ 50%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_nonempty_index_after_empty_index PASSED [ 55%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_repeated_empty_index PASSED [ 60%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_index_not_called_returns_empty PASSED [ 65%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_multi_word_query PASSED [ 70%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_tokenization PASSED [ 75%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_tokenization_case_handling PASSED [ 80%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_large_corpus PASSED [ 85%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_special_characters_in_query PASSED [ 90%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_exact_phrase_matching PASSED [ 95%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_single_word_chunks PASSED [100%]

============================== 20 passed in 0.10s ==============================
Exit code: 0
```

## Eval iterations

**Run history**

The first full harness attempt errored on all 20 packages: Claude was
not logged in. Its displayed agreement was `0/0 scored items`, not a
valid scored run. The harness did not save eval-run.txt. Later login
checks also failed. A successful full run and its actual agreement score
are still required; the existing eval-run.txt scaffold is not a result.

**Package analysis**

Manual rubric application to scored package `pkg-01`: reject; the gold
label is reject. This is a manual analysis, not a completed harness run.
The package's Repro evidence says:

> `--debug` on the failing run shows the error is raised by argparse's `parse_args` while consuming positionals; the request items are never handed to HTTPie's item parser.

The plan instead says:

> The `REQUEST_ITEM` tokenizer in `httpie/cli/requestitems.py` is the problem.

Diagnosis fails because a tokenizer change cannot address an error
that occurs before that tokenizer receives the items. The no-flag
control also shows those item strings already parse successfully.

**Check rationale**

Exact current Diagnosis row from tools/plan-check/rubric.md:

| Diagnosis | Candidate plan's cause and approach, compared with Issue, Thread highlights, and Repro evidence (including controls, timings, and artifacts). | The proposed cause explains the reproduced failure and relevant controls without contradicting them. The change addresses that cause rather than merely hiding the symptom. A thread claim alone does not outweigh contrary reproduction evidence. | required |

The worksheet's sample passed any plan that named a cause. I replaced
that condition with a comparison against reproduction results and
controls so a specific but contradicted explanation cannot pass.
This rejects the pager explanation in calib-03 and the tokenizer
explanation in pkg-01. Naming a source file alone is not proof.

**Trade-offs**

Manual verification is allowed when it repeats the original trigger
and specifies an observable expected result. This avoids rejecting
calib-01 solely because it has no automated test. Required unclear
checks hold the package, which can delay a sound plan whose evidence
is missing. The rubric does not require exact filenames when concrete
areas suffice. No successful full eval or canary run is claimed, so
these choices still require harness validation.
