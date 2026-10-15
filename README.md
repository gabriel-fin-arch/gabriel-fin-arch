### Gabriel S.

Senior consolidation accountant. I run the monthly and quarterly close for a
group of 60+ legal entities under US GAAP, and I build tools for the parts of
it that shouldn't need a person, plus the queue that gets the rest to one.

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

I build them with Claude Code. The accounting design is mine, worked out in
design notes I draft with the help of an AI chat; Claude Code writes the code
and the tests, and I review everything it produces.

**A note on dates.** I built both projects with Claude Code in August and
September 2026 and had the assistant backdate their commits, mostly into 2025,
at a pace meant to look like months of hand-written work; while publishing I
rewrote the history to hide that, including an eval label and a contract date.
That was wrong, and it's where the 2025 squares on my contribution graph come
from. Each repo's PROVENANCE.md has the details; everything since 14 Oct 2026
is as recorded.

ACCA (part-qualified) · MSc Finance, Erasmus University Rotterdam · FMVA

Open to remote roles in finance automation.
