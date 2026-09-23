---
type: guide
guide_family: playbook
updated: YYYY-MM-DD
---
<!-- seed: breakthrough-evaluator-agent playbook/evaluator-agent/_Evaluator-Agent-Guide.md v0.1.0 -->

# Evaluator Agent

Sending a judge that is not the author: one finished piece against pass criteria written in advance (evaluator mode), or a batch against its source of truth (audit mode). ⛔ Verifying hundreds of identical units is a different job and does not belong here.

## Read this before working, in this order

1. **Settle what is open.** Read "Recent runs" below. Any row whose date has passed with
   nothing in "What happened" gets looked up where the answer lives (the messages, the
   orders, the sign-ups), drafted, and put to the owner as one question. ⛔ A row with a
   blank date carried no bet: it is an index entry, it is never chased, and it is not
   something to settle.
2. **Revise, if a sentence just came up for the third time.** In "So". The owner's yes
   first, then "How we do this work" changes.
3. **Do the work**, with the section above brought up to date a minute ago.
4. **Register what came out**, in this same session: one row, ⭐ its address in the
   first column, then what the owner expects and when that counts if they have an
   expectation. "Nothing in particular" is a real answer and the row still goes in.

## How we do this work

The full text is in [[evaluator-agent-playbook]]. It arrived as a seed: sentences tagged `[untested]` come from research and have not yet held in your own work, and each one either loses its tag or gets rewritten after the first real run that exercises it. Three bones:

- **Fixed gates, open path.** What counts as a pass, what evidence looks like, what gets reported, the format, when to stop and what to do when the judge cannot answer are written every time. How to investigate and where else to look are left to the model.
- **Judge the files, not the report; missing evidence is a FAIL; the judge never fixes.** The judge is a fresh subagent that cannot see the author's reasoning. Every PASS and every finding carries evidence someone can rerun in a minute, with a sampling floor of at least 12. A judgment with no source of truth to quote comes back UNKNOWN and goes to a person.
- **Two modes, one core.** Evaluator mode judges round by round while the work is being made, with criteria written before the work, and hands to a person at the round cap. Audit mode checks a batch after the fact or on a schedule, is never run by the session that built it, reports problems that were already there, and does not loop.

How to send one: fill the six field brief in step 1 of the playbook's "The moves" and send a general-purpose subagent. No dedicated agent file for now; revisit after a few real uses.

⭐ **Registering runs.** Every audit run gets one row here, with `[A]` at the start of its first column. An evaluator verdict lives in the project folder of the work it judged; it gets a row here, with `[E]`, only when it carried a bet.

## What we have learned

- (Nothing yet. When the same "So" sentence appears for the third time, propose a line here.)

## Recent runs

| What came out | What I expect | When it counts | What happened | So |
|---|---|---|---|---|
