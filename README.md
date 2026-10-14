### Gabriel S.

Senior consolidation accountant. I run the monthly and quarterly close for a
group of 60+ legal entities under US GAAP, and I build tools for the parts of
it that shouldn't need a person, plus the queue that gets the rest to one.

Both projects predate their public repos; their git histories don't. I
re-created them from my working copies when publishing in 2026, so the commits
before 14 Oct 2026, and the contribution squares for those months, show the
order of the work rather than when each step happened. Some of my rewrites
while publishing went further than they should have; each repo's
PROVENANCE.md says what changed.

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
