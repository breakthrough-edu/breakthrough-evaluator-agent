---
type: playbook
lane: build
status: forming
confirmed_by_owner: false
references: []
tags: []
---
<!-- seed: breakthrough-evaluator-agent playbook/evaluator-agent/evaluator-agent-playbook.md v0.1.0 -->

# Playbook: send a judge that is not the author

**Read this first.** This playbook arrived as a seed, distilled from published research on evaluator agents (LLM-as-judge, verifiers, critics). Untagged sentences are the working rules of the method. A sentence tagged `[untested]` is a claim carried over from research that you have not yet seen hold in your own work. ⭐ After your first real use, go through every `[untested]` sentence that run actually exercised: if it held, remove the tag; if it did not, delete the sentence or rewrite it to say what did happen. Sentences the run never touched keep their tag until a later run touches them.

## When to run it

**Two modes, one core.**

- **Evaluator mode**: one finished piece of work, pass criteria written before it was made. The maker says "done" and you send a judge. The verdict goes back to the maker, who fixes and hands it back for another round, until it passes or hits the round cap.
- **Audit mode**: a batch of things (a folder, a registry, a database table, the tail end of a move or rename) checked against its long-standing source of truth. The exception list goes to the owner. No back and forth.

**Your three real jobs.** These are also the baseline this playbook gets checked against later: a clean session should be able to do any one of them from this playbook alone, without coming back to ask.

1. <A real job that needs an independent check.> What goes wrong today without one: <in the owner's words>. (<evaluator or audit> mode)
2. <A real job that needs an independent check.> What goes wrong today without one: <in the owner's words>. (<evaluator or audit> mode)
3. <A real job that needs an independent check.> What goes wrong today without one: <in the owner's words>. (<evaluator or audit> mode)

If the three lines above still show placeholders, ask the owner once for their three real jobs; this does not block the run, and if they skip the question, carry on with the job in front of you. The shape of a good answer, for reference only: "a finished landing page gets a judge before it goes live, because the session that built it checks its own work and cannot see the assumptions it made" (evaluator mode); "check the list of background jobs I keep by hand against what is actually running on the machine, because entries go missing" (audit mode); "after moving or renaming a folder, search for every old name and attach the real search output, because searching only the new paths leaves the old names behind" (audit mode).

**When it is not worth sending one** `[untested]`. Sending a judge here only buys leniency or wasted spend.

| Situation | Use instead |
|---|---|
| A check a machine can run (tests, schema validation, a search that must return zero, your own validation script) | Run the check |
| Hundreds of identical units to verify | Batch screening, which this playbook does not cover: run independent passes over every unit and send only the units where they disagree to a person; a judge reviews only that method's calibration sample |
| Pure taste, with no source of truth to cite | Judge it yourself a few times and write down why, then decide whether a judge is worth it |
| The judge could not solve the task either, and there is no reference answer | A person |
| Only the same model rereading the same text | Do not send one; first find something that can be run or checked |
| Cost or time is tight | One review at the very end, no loop |

## What to weigh

**The spine: fixed gates, open path.** Fixed, every time: what counts as a pass, what evidence looks like, what gets reported, the format, when to stop, and what to do when the judge cannot answer. Open, left to the model: how to investigate and where else to look. Rules written onto the search scope lower what the judge finds `[untested]` (one code review product loosened its agent to hunt freely and filtered the results downstream, and its resolution rate rose from 52% to over 70%). Rules written onto the evidence bar are what make its judgment trustworthy.

**The shared core. Both modes follow all of it.**

- **Independent.** Send a new subagent. ⛔ Never a fork: a fork carries the author's whole line of reasoning into the judge. The brief carries no author reasoning, no draft history and no self-assessment. **Judge the files and the real data, never the report of the agent that did the work**: that report is only a second copy of the same opinion.
- **Evidence, and missing evidence is a FAIL.** Every PASS and every finding carries evidence that someone else can rerun or locate within a minute: a command plus its real output, a screenshot path, a `file:line`, or a quoted line from the source of truth plus its path. A judge that can reach the primary source can catch fabrication (for example, `grep` plus `git log -S` shows whether something reported as deleted ever existed). **Write the sampling floor into the brief, at least 12 items.** "I ran it" is not evidence.
- **No source to cite means UNKNOWN** `[untested]`. When the information is not there, or the judge could not do the task itself, it says where it got stuck and hands the call to a person. It never guesses.
- **The judge never fixes anything.** It produces evidence only, and writes only to the scratchpad path the brief gives it. ⚠️ A general-purpose subagent has write tools, so this is an instruction, not a lock. The backstop is the caller checking, after the report comes back, that the work's modification time has not moved.
- **Reasons first, verdict last**, and the output follows the schema below exactly `[untested]`.

**Evaluator mode adds:**

- The pass criteria are **written before the work is made**. Criteria the author adds afterwards do not count `[untested]`.
- 3 to 10 gates, each judged pass or fail only, and at least one of them a penalty gate (errors, padding, claims with no support) `[untested]`. A checklist of only "did it do X" gets gamed.
- From round 2 on, only blocker and important findings can block. Every round re-checks every gate, because a fix often breaks a neighbour `[untested]`.
- A finding stays reported unless new evidence disproves it. The author arguing against it is not evidence `[untested]`.
- Not reported: style preferences, problems that were there before, anything a linter catches, anything outside the criteria.

**Audit mode adds:**

- **The auditor is never the session that built the thing.** The builder remembers how the rules were meant to be, and fills any drift back in without noticing it is there.
- **Problems that were there before are exactly what to report**, the opposite of evaluator mode.
- The population and the sample are fixed in the brief, and the report says which items it looked at and how it chose them.
- When a hand-kept registry reads zero for something that plainly exists, first ask what the registry was meant to cover (its scope), then how long since it was updated. Missing entries that predate its last update point at scope, not staleness.

**What counts as evidence when the work is not code.** A judge is only as reliable as the line of a source of truth it can quote. The values being judged against live in their own sources of truth; this table only says what the evidence looks like.

| What is judged | Counts as evidence | Does not count |
|---|---|---|
| Landing page or HTML page | A screenshot path, taken after fonts and images finished loading; a visual judgment quotes the line of your brand style guide plus its path; the number from `grep -c 'src='` (a page with zero images was never designed) | Reading the HTML and saying it looks right |
| Page in a hosted page builder (GHL and similar) | Only the published URL, fetched or screenshotted (the preview is not the published page); settings read back through the API and set beside the matching line of your settings registry; a test payment that actually reaches the thank you page | What the builder's editor shows |
| Content (post, script) | The original sentence from your brand positioning or target audience notes, plus its path; banned words and banned punctuation counted with `grep -c` returning 0 | "The tone is right" with no quote |
| SOP | Every step run once for real; for a step that cannot be run, `ls` the file or command it points at | Reading it through and finding it clear |
| Folder move or rename | Old paths, old folder names, old type names, template names and every link pointing in, each searched to zero, command and output pasted; file contents compared by hash sets (md5), not by path | "Upstream finished, so this finished too" |
| Database (Lark, Airtable, Notion and similar) | Record count and field list read back through the API or CLI; after a write, the record read back by its ID; at least 12 records compared field by field | The script exited 0 |
| Reconciliation | Each side's total plus the command that produced it; every exception carries a record ID plus the statement line number | "Roughly matches" |
| Background jobs (schedulers, watchers, bots) | The scheduler's own status line (on a Mac, `launchctl print`), a timestamped log tail, process start time compared with build time | It ran right after install; an HTTP 200 |
| A parser or prompt that eats model output | At least one real model output run through it, the raw text saved | Hand-written test fixtures all pass |

## The moves

1. **Fill the brief.** Six fields; a missing field means the judge sends the brief back. Copy the block and fill it in:

```
MODE: evaluator | audit
1. What is being judged: <path / URL / how the population is defined>
2. Judged against: <evaluator: the gate list, written before the work was made | audit: the sources of truth, with paths>
3. How to run or compare it: <command / preview URL / path of the source of truth>
4. What counts as a finding and what does not: <this playbook's "adds" list for the mode, plus anything specific to this job>
5. Round number / round cap (default 3) / sampling floor (at least 12) / scratchpad path where the evidence goes
6. The previous round's findings plus the author's reply to each (fixed / skipped with a reason / no change needed); in round 1 write "none"
Before you start, read "What to weigh" in: <path of this playbook, filled in by whoever sends the judge>. You did not make this thing and you have not seen the reasoning behind it.
```

2. **Send.** A new general-purpose subagent, given the brief and nothing else. ⛔ Never attach the author's reasoning or conversation.
3. **Receive.** Read the tally, then **pick one piece of evidence and rerun its command yourself** before trusting anything else in the report. If it does not reproduce, send the whole report back. Then check that the work's modification time has not moved. Why this step exists: a report can contain numbers the judge never actually produced, and a confident tally reads the same either way `[untested]`.
4. **Evaluator mode loops.** The findings go back to the maker, who replies to each one; that reply becomes field 6 of the next brief, and the same judge continues through SendMessage. Stop when every gate passes with no blocker, when a round produces no new finding of important or worse, or when the round cap is reached. At the cap with a blocker still open, stop and hand it to a person; do not add rounds `[untested]` (more rounds of revision measurably make the work worse). If the same problem has been corrected more than twice, the context is full of failed attempts: start a fresh judge rather than continuing `[untested]`.
5. **Audit mode does not loop.** The exception list lands in the project folder the audit belongs to (no project: the inbox) and goes to the owner.
6. **Register on the door.** Every audit run gets one row, marked `[A]` at the start of its first column. An evaluator verdict lives in the project folder of the work it judged; the door gets a row, marked `[E]`, only for the runs that carried a bet.

**Output schema.** The judge fills it in exactly:

```yaml
mode: evaluator | audit
tally: "0 blocker, 2 important, 1 nit"
overall: PASS | FAIL | UNKNOWN        # PASS only when every gate is PASS
sample: "population N, looked at n, how they were chosen"
gates:
  - id: G1
    criterion: "..."
    verdict: PASS | FAIL | UNKNOWN
    evidence: "rerunnable command plus real output / screenshot path / file:line / quoted line of the source of truth plus its path"
findings:
  - id: F1
    gate_or_category: G2 | open-hunt
    severity: blocker | important | nit | pre-existing
    location: "file:line / URL plus state / section heading"
    summary: "one sentence"
    evidence: "..."
    verified: yes | no
    suggested_fix: "..."
    confidence: high | medium | low
unknowns:
  - "what could not be checked, why, and who should decide"
```

**Calibration, solo version** `[untested]`. No labelled dataset. Each report gets three things, two minutes in total: rerun one piece of evidence; in the door row's "What happened", write "it passed N that I would fail, it blocked M that I would pass"; keep at most three examples per mode in this folder (a correct FAIL, a correct PASS, a correct UNKNOWN), and swap one out rather than add a fourth. When you move to a new model, rerun those kept examples once: the line between work that needs a judge and work a single agent handles alone moves with every model generation `[untested]`.

<!--
Rules live here only. Any skill or agent file that runs this playbook is a pointer to this file,
  never a copy of it, so there is one place to change a rule and nothing else drifts.
No dedicated agent file is needed to start: a general-purpose subagent plus the brief above is
  enough. If one is made later (for example with its write tools removed), it points here.
Two modes share one folder because they are one kind of work: brief an agent that is not the
  author to judge. The door keeps one record for both.
-->
