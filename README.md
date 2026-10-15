### Gabriel S.

Senior consolidation accountant. I run the monthly and quarterly close for a
group of 60+ legal entities under US GAAP, and I build tools for the parts of
it that shouldn't need a person, plus the queue that gets the rest to one.

A note on dates. I built both projects with Claude Code between August and
October 2026. When I created them I had the assistant backdate the commits,
mostly into 2025, so the history would look longer, and while publishing I
rewrote it several times to hide the contradictions, including relabelling an
eval run. That was wrong, and my first notes about it here weren't true
either. Commits before 14 Oct 2026 carry invented dates, and so do the 2025
squares on my contribution graph. Each repo's PROVENANCE.md lists what I
changed and how to check it; everything from 14 Oct 2026 on is as recorded.

**Projects**

- [intercompany-close-agent](https://github.com/gabriel-fin-arch/intercompany-close-agent):
  matches intercompany balances, ties the subledger to the trial balance before
  anything else, books the eliminations, and sends six kinds of break to a
  reviewer however small they are. LangGraph with a native human-in-the-loop
  interrupt. The model writes the rationale; it never does the arithmetic.
- [revrec-contract-reviewer](https://github.com/gabriel-fin-arch/revrec-contract-reviewer):
  reads contract PDFs for ASC 606, cites every value back to its clause and
  page, and puts the eight judgment calls a contract can't answer in front of
  a person. Scored against a gold set, regex baseline against Claude, with the
  places the model loses written down.

**How they're built**

The numbers come from deterministic code with tests around it. Where there is
a model, it triages and explains. Anything it asserts has to point at its
source or it's dropped, and the policies that matter are enforced in code
rather than left in a prompt.

I build them with an AI coding assistant (Claude Code). The accounting design
is mine and I review what it produces; most of the code is drafted by the
assistant.

ACCA (part-qualified) · MSc Finance, Erasmus University Rotterdam · FMVA

Open to remote roles in finance automation.
