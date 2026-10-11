# Plan and implement

## GitHub username

qingtaozhou

## Plan comment

Pending: posted comment URL and exact posted text have not been provided.
`comment-draft.md` is an unposted draft, not evidence of a posted comment.

## Branch

`fix/68-empty-keyword-index`

Fork: https://github.com/qingtaozhou/pathreview-ai301-fa26-s3

## Evidence

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

## Run history

The first full eval attempt errored on all 20 packages because Claude
was not logged in. The harness saved no eval-run.txt. Later login
checks also failed. No successful or passing eval run is claimed.

## Package analysis

Manual calibration review: calib-03's pager diagnosis contradicts the
slow no-pager highlighting control. Diagnosis therefore compares the
cause to reproduction controls rather than merely asking whether a
cause is stated. calib-01 has a concrete refresh callback change and
a decisive manual check, so automated tests are not mandatory.
No scored-package disagreement analysis is available before a run.

## Check rationale

Diagnosis prevents fixes based on contradicted causes. Scope prevents
unrelated expansion. Executability requires a concrete starting point.
Test plan requires observable verification of the reproduced failure.
Honesty keeps claims within evidence. Comms checks the actual comment
against maintainer direction and repository policies.

## Trade-offs

Every required check must pass; unclear evidence holds the package.
This favors verifiable readiness over accepting unverifiable plans.
Manual tests can pass when they reproduce the trigger and name a
clear expected result. Exact filenames and document headings are not
universal requirements. The blank-text nonempty-corpus case is outside
this fix. These choices have not yet been validated by a full eval run.
