### Gabriel S.

Senior consolidation accountant, open to remote roles in finance automation.
I run the monthly and quarterly close for a group of 60+ legal entities under
US GAAP, and I build tools that handle the parts that shouldn't need a person
and send the rest to the right one.

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
and the tests, and I review everything it produces. How a change gets made,
who does what, and the rules the assistant works under:
[HOW_I_WORK.md](HOW_I_WORK.md).

**A note on dates.** I first backdated these projects' commits into 2025 and
rewrote the history to hide it. On 15 Oct 2026 I restored the real commit
times from my Claude Code session logs: intercompany-close-agent was built in
August 2026, revrec-contract-reviewer in September. Each repo's PROVENANCE.md
has the details. GitHub has since recounted my contribution graph: it shows no
commits in 2025, only the rebuilt history and the later work in 2026.

ACCA (part-qualified) · MSc Finance, Erasmus University Rotterdam · FMVA
