# Rubric: is this a good first issue?

Measure recency against the bundle capture date in eval mode and today's
date in live mode. Use only bundle evidence in eval mode. Apply the
live scope's house rules when interpreting claim evidence.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer activity | Repo facts: last 5 default-branch commits and maintainer first-response sample; issue comments with Owner, Member, or Collaborator association. Live: the corresponding commit history and issue threads in references/evidence-guide.md. | At least one human maintainer commit, merge of a human-authored PR, or substantive maintainer issue response in the past 90 days. Automated commits alone do not pass. | required |
| Repository in use | Repo facts: archived flag, latest release, last push, stars, and human commit history; issue body/thread for reports of current use; live: repository banner, Releases, branch history, and Used by counter. | Repository is not archived and has either a release within 365 days or human development within 90 days together with evidence of adoption (at least 100 stars, at least one dependent repository, or a concrete report of current use). A recent automated push alone does not establish use. | required |
| Newcomer scope | Issue body, comments, creation date, and closed unmerged PR history. | Work is one bounded contribution with an identifiable outcome. Reject umbrella/tracking issues, unresolved design debates, maintainer-confirmed core-internals changes, and pure usage/support questions. Also reject issues open more than 2 years with at least 2 abandoned implementation PRs. A short description, absent reproduction steps, or lack of a good-first-issue label alone does not fail a bounded task. | required |
| Available work | Repo facts: issue state, assignees, linked PR states; full comment thread including PR mentions and claim/release comments. Live: issue sidebar, Development panel, and thread. | Issue is open, has no assignee, no open implementation PR (including one mentioned only in comments), and no unresolved claim within 30 days or older claim explicitly confirmed as active. Explicit withdrawal or maintainer reopening of work clears a claim; closed unmerged PRs are not active claims. Apply live scope house rules to student claims. | required |
| Compatible contribution policy | Repo facts: contribution policy; live: CONTRIBUTING.md, linked contributor policies, AI policy files, and PR templates as described in references/evidence-guide.md. | No explicit ban on the intended AI-assisted contribution. Disclosure, personal understanding, testing, and human review conditions pass and must be reported as obligations. An explicitly silent policy in a bundle, or no restriction found after checking the live policy sources, passes. Inaccessible sources or a missing bundle policy entry are unclear. | required |
| Newcomer support | Issue labels and maintainer comments in the body/thread; live: issue labels and thread. | A good-first-issue label or a maintainer's explicit offer of guidance is present. | preferred |

## Verdict rule

Accept only if every required check passes. Any required fail or unclear
means reject. Grade unclear only when the evidence needed to decide is
missing; do not invent facts. Preferred checks never change the verdict;
use them only to rank accepted issues. Report one concrete evidence quote
or fact for every check, including any contribution-policy obligations.
