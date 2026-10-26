# How I work

How a change to my two projects gets from an idea to `main`, who does what,
and the rules the work follows. The projects' READMEs say what each one does
and how it was built; their `PROVENANCE.md` says what happened to their
history. This page links to them rather than repeating them.

## How a change gets made

1. **An issue.** Claude Code drafts it from a review of the repo: the problem,
   acceptance criteria, a priority. I approve the scope, change it or drop it
   before any work starts. So far I haven't dropped any, but I changed two:
   the Docker images issue, which I moved up to be done from `main` without
   waiting for the `demo` command, and the journal export issue, where I
   scoped the formats myself before anything was written — Dynamics 365 and
   a generic CSV, plus a note on Lucanet.
2. **A branch and a pull request**, one per issue, never a push to `main`.
   Every PR follows the
   [template](https://github.com/gabriel-fin-arch/intercompany-close-agent/blob/main/.github/pull_request_template.md):
   what the issue asked, what the assistant drafted, what I changed or
   rejected in review, and how it was verified.
   Example: [revrec-contract-reviewer#20](https://github.com/gabriel-fin-arch/revrec-contract-reviewer/pull/20).
3. **CI** on every PR:
   - the pre-commit hooks;
   - mypy;
   - the tests with coverage and no API key;
   - the offline pipeline end to end;
   - the container image;
   - the tests again on the oldest dependency versions the project allows.
   
   ([intercompany](https://github.com/gabriel-fin-arch/intercompany-close-agent/blob/main/.github/workflows/ci.yml),
   [revrec](https://github.com/gabriel-fin-arch/revrec-contract-reviewer/blob/main/.github/workflows/ci.yml))
4. **My review**, then **my merge**, with a merge commit. Then I fill in
   "What I changed or rejected in review", including "nothing" when that's
   the answer.

## Who does what

**Claude Code** (Claude Opus 5.5, in the desktop app) drafts:
- the code, the tests and the docs;
- the commit messages, the PR descriptions and the issue drafts.

Every commit it has drafted since 15 October 2026 carries a
`Co-Authored-By: Claude` line. The commits of August to mid-October don't; each
`PROVENANCE.md` covers that history and how it was built.

**I**:
- choose what gets done;
- make the accounting and design decisions;
- decide what the gold sets say a contract requires;
- decide when to spend on the API;
- review and merge.

The decisions I always keep: the accounting design and the materiality
policy, the gold — what it says a contract requires —, the ERP export
format, the API spend, merges and releases, and the GitHub settings
(enabling Pages, permissions, branches).

What I don't do: I don't write the projects' code or tests, and I don't
touch the CI configuration except to approve it. Merges and releases I do
from the GitHub web. The exception is my own commits of 20 October 2026,
made with git on my PC: the Harbourline and Tessellate gold corrections
([revrec-contract-reviewer#27](https://github.com/gabriel-fin-arch/revrec-contract-reviewer/pull/27)
and [#28](https://github.com/gabriel-fin-arch/revrec-contract-reviewer/pull/28)),
the fix that passes the preparer to the sample results, and the two
releases. The gold is my accounting judgment. The code, the test and the
rescored runs that came with it I wrote with an LLM's help, and those
commits carry no `Co-Authored-By` line to say so. The PR descriptions of
that day that don't follow the template I drafted myself, in a hurry.

## The rules the assistant works under

- Nothing is pushed, merged, released, created on GitHub or changed in its
  settings without my go-ahead in the chat, each time.
- No call to the Anthropic API without:
  - a cost estimate first ([`revrec estimate`](https://github.com/gabriel-fin-arch/revrec-contract-reviewer/blob/main/docs/evaluation.md#how-a-model-run-is-measured) works it out without calling the API);
  - my approval, with a ceiling.
  
  Each run is saved with every call's tokens, cost and seconds.
  Example: [revrec-contract-reviewer#19](https://github.com/gabriel-fin-arch/revrec-contract-reviewer/pull/19).
  My own limit: no run above USD 5 unless I say so explicitly, and if the
  month's spend went past USD 20, everything stops and we talk. No run has
  come close so far.
- Tests and CI run with no API key; the CI workflows use no secrets.
- The key lives in a `.env` file that I edit and that the assistant doesn't
  read or show. The commands read it themselves; I never paste it in the
  chat or in any file that gets pushed.
- Real dates, and no history rewrites since the restoration of 15 October 2026 that
  [PROVENANCE.md](https://github.com/gabriel-fin-arch/intercompany-close-agent/blob/main/PROVENANCE.md)
  describes.

## How the numbers stay honest

- **The README figures.** Every figure in a README is rendered by a script from a run, and a test fails if the
  README and the run disagree:
  - [`sample_results.py`](https://github.com/gabriel-fin-arch/intercompany-close-agent/blob/main/src/intercompany_close_agent/sample_results.py)
    reruns the sample close;
  - [`evaluate/published.py`](https://github.com/gabriel-fin-arch/revrec-contract-reviewer/blob/main/src/revrec_contract_reviewer/evaluate/published.py)
    reads the saved evaluation runs.
- **The saved runs.** Model runs are saved with what the model returned and every call it made, in
  [`evals/results/`](https://github.com/gabriel-fin-arch/revrec-contract-reviewer/tree/main/evals/results),
  so a score can be recomputed without calling the model again.
- **The held-out test set.** It was written and committed with its answers before anything ran on it, and
  nothing is tuned on it
  ([revrec-contract-reviewer#18](https://github.com/gabriel-fin-arch/revrec-contract-reviewer/pull/18)).
  A prompt change argued from the development set was measured on both sets and dropped
  ([#20](https://github.com/gabriel-fin-arch/revrec-contract-reviewer/pull/20)).

## How I review

- **CI first.** If it's not green I don't even open the PR. Then "What to
  look at in review", which tells me where to look, then Files changed. I
  read the description last, once I already know what's inside.
- **Line by line only what touches accounting**: the matching rules, the
  elimination calculations, the materiality policy, the gold judgments and
  anything that writes a journal entry. The rest — CLI, formatting,
  infrastructure tests — I skim and trust CI with.
- **I run it myself when the PR touches something you can see or run**: the
  demo, the dashboard, the journal exporter. When the PR is CI,
  configuration or docs, green CI and reading the diff is enough.
- **The accounting gets checked with pen and paper, literally.** I take two
  or three items and redo the calculation by hand — an intercompany pair's
  elimination against the ledger, or an ASC 606 judgment against the
  contract clause. Materiality I check against the policy file, not against
  my memory. If my hand-computed figure and the code's don't match, it
  doesn't get merged.
- **Published figures, both ways.** The test that fails when the README and
  the run disagree is the everyday guarantee; but in the PR that introduces
  or changes a published figure I run the script once myself and see the
  figure come out for real. After that I trust the test.
- **What makes me ask for a change**: a figure that doesn't tie, an
  accounting judgment badly reasoned, or docs that promise something the
  code doesn't do. A real example: the gold corrections for Harbourline and
  Tessellate, which I decided and committed myself — they show in
  [revrec-contract-reviewer#27](https://github.com/gabriel-fin-arch/revrec-contract-reviewer/pull/27)
  and [#28](https://github.com/gabriel-fin-arch/revrec-contract-reviewer/pull/28).
- **What I leave to CI**: style and formatting (the pre-commit hooks),
  types (mypy), coverage, whether the Docker image builds, and the tests
  against the oldest allowed dependency versions. I say nothing about those
  unless CI fails.

## Why

Because this portfolio is precisely about audit trails: if I can't defend
every figure, every date and every decision as mine, it's worth nothing.
Working this way is what lets me defend it.

Two things changed because they didn't work. On 20 October I resolved merge
conflicts in the GitHub web UI and I won't do that again — it's slow and
done with no tests, blind —; from now on the assistant fixes conflicts in
its own environment with green CI and I just review the PR. I also changed
the order of releases: everything gets merged first and published after,
not the other way round.
