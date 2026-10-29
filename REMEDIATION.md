# Remediation: the commit dates

## The deficiency

I built both projects with an AI assistant — intercompany-close-agent in
August 2026 and revrec-contract-reviewer in September 2026 — and published
them with every commit backdated: September 2025 to February 2026 for the
first, June to November 2025 for the second, spread out to read as months of
hand-written work. It was deliberate, and I kept it up: when the files
contradicted the invented dates I changed the files to fit the dates, not
the other way round — a model label, the date of a corpus contract, tags,
and CI runs I deleted. Until mid-October the READMEs told the same
invented story.

## Root cause

I believed the portfolio would only be credible if it read as long-running,
hand-written work, and I treated the history as marketing instead of as a
record. Precisely in finance, where the trail is the point, that is the
wrong trade, and I knew it at the time.

## Impact

What was affected: commit dates; the model label on revrec's published run
(claude-opus-5 presented as claude-opus-4 so the numbers would fit 2025);
the date of one corpus contract (the Meridian change order, moved from
January 2026 to October 2025; restored); the tags and the CI runs while I
was publishing.
What was not affected: the code, the synthetic data, the corpus and the
gold set, the tests, and every published figure. No number was ever changed
to fit a date — only labels and dates were.

## Remediation

On 15 October 2026 I rewrote each default branch one last time so the
history itself would be true: every commit rebuilt on its own tree with its
real time, taken from my Claude Code session logs, second by second; what
each earlier force-push had changed in the files was recorded as a bridge
commit. No file content changed. Each repo's PROVENANCE.md documents it
all: the force-pushes, the things I said here that weren't true when I said
them, and a commit map.

## Testing the remediation

Nothing here depends on my word. `git log --format='%ad | %cd'` on main
shows author dates as the times the commits were made and committer dates
of 15 October 2026. The Activity tab links every force-push, and the
"before" commits are still reachable (`git fetch origin <sha>`). The commit
map in each PROVENANCE.md pairs every old SHA with its replacement. My
contribution graph shows no commits in 2025 — GitHub recounted it on
26 October 2026.

## Ongoing monitoring

- Branch ruleset `protect-main` on all three repositories since
  28 October 2026: no force-pushes, no deletions of `main`, every change
  through a pull request, with no bypass. It is visible to anyone, logged
  in or not, at github.com/gabriel-fin-arch/<repo>/rules.
- The authorship rule for `recalc/`: those files I write myself, with no
  Co-Authored-By line; it is stated in HOW_I_WORK and in each recalc README.
- A provenance check in CI over all new history fails the build on any
  backdating or rewrite, and `main` now requires it to pass.

## Visible artifacts, explained

- 47 commits of revrec-contract-reviewer share one second — 8 September
  2026, 07:53:48 UTC. They came from one script run replaying that day's
  session log, and they show the real time.
- 69 commits of intercompany-close-agent fall on 5 August 2026. The project
  was built that day; most of it, in fact.
- The architecture decision records are dated 23 October 2026 because
  that is when they were written down: Claude Code drafted all seven in
  one commit from sketches I wrote, and "Accepted" on each is that day,
  not the day the decision was taken — the decisions themselves come
  from my design notes of August and September. The ADR index says
  exactly this at the top.
- Four releases of revrec-contract-reviewer in eight days, 20 to
  27 October 2026: the last stretch of building, after the real dates were
  back. That is simply the pace.

## What I learned

A history you have to engineer is a liability, not an asset: the months it
pretends to add cost more in credibility than they buy. A control only
counts when it can catch you, which is why the ruleset has no bypass and
why the recalculation files are mine alone. And the true version — built
fast, then verified by hand — turns out to be the stronger portfolio.
