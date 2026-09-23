# Install: breakthrough-evaluator-agent

You are a Claude Code session installing this for the owner, live, with them. Read this whole file before you do anything. It is short on purpose: the playbook it installs is the product, and this file only decides where the playbook lands and asks the one question only the owner can answer.

## 0. Get the payload

This needs the network, so ask the owner's yes before you run it (or let them run it themselves):

```
npx skills add breakthrough-edu/breakthrough-evaluator-agent -g -a claude-code -y
```

Then confirm it landed:

```
ls ~/.claude/skills/breakthrough-evaluator-agent/playbook/evaluator-agent/
```

You should see two files: `evaluator-agent-playbook.md` and `_Evaluator-Agent-Guide.md`. If the CLI reported a different install location, look there instead. If the files are not there, stop and tell the owner exactly what you saw.

## 1. Find out where the owner keeps their judgment

Read only. Write nothing yet. Report what you found in two lines before going further.

- **Case A, a my-second-brain vault.** The test is one file: `99_Meta/structure-doctrine.md`. Look from the working directory. If it is not there, ask once, as a locating prompt and not as the install question: "Where is your vault?" If they have none, this is case C. When the doctrine is there, read it: section 1 for the real path of the methodology layer (it sits inside a business wing, never at the vault root) and section 9 for playbook folders and their door. If the vault has more than one business wing, ask which wing this belongs to, and default to the one whose folder starts with `04_`. Also check that `99_Meta/Templates/Playbook.md` and `99_Meta/Templates/Playbook-Guide.md` exist and that `99_Meta/bootstrap-progress.md` says `setup_complete: true`. All of that true: case A.
- **Case B, another notes system.** An Obsidian vault (a `.obsidian/` folder) or a notes folder the owner names, with no doctrine file. ⭐ This is also the one fallback for a my-second-brain vault that does not pass every check above (templates missing, setup not finished, an older vault that lacks the `playbook` family): say which check failed, then treat it as case B.
- **Case C, nothing.** No vault and no notes folder at all.

⛔ Never decide the case from how the folders look. The doctrine file is the test, and reading it is how you learn that vault's rules.

## 2. Case A: install as a playbook folder in their vault

Follow the rules of THIS vault as you read them today. Its `CLAUDE.md` and doctrine outrank anything below, and where they differ, do what they say and tell the owner.

1. **Already there?** If `<methodology>/Playbooks/evaluator-agent/` exists, stop and follow "Updating" below. ⛔ Never overwrite.
2. **Ask one question**, in the owner's own language, and only this one:
   "Name three real jobs in your business where you would want a judge that is not the author: a finished thing you want checked, or a batch you want audited against its source of truth. For each one, what goes wrong today without that check?"
   Their answer, in their words, fills "Your three real jobs" in the playbook's "When to run it" section, replacing the three placeholder lines and the paragraph that tells a reader to ask for them. Mark each job evaluator or audit mode yourself, from what they said. ⛔ Do not walk them through the playbook's rules one by one, and ⛔ never invent the jobs yourself. If they skip the question, keep the placeholders; the playbook asks again at first use and does not block on it.
3. **Show the exact list of what you will write, then ask for one yes:**
   - New file `<methodology>/Playbooks/evaluator-agent/evaluator-agent-playbook.md`: the seed exactly as shipped, except the three jobs filled in from step 2. Keep `confirmed_by_owner: false`, `references: []` and the seed stamp. Keep `lane: build` if the doctrine lists a `build` lane; if its lanes are named differently, use the one that governs building and fixing the business's own systems, and name your choice in this list.
   - New file `<methodology>/Playbooks/evaluator-agent/_Evaluator-Agent-Guide.md`: the door seed, with `updated:` set to today and exactly one row under "Recent runs": `| [[evaluator-agent-playbook]] (installed <today>) | A clean session does one of my three jobs from this playbook alone, without coming back to ask | At its first real use | | |`
   - Edit `02_Command-Base/Home.md`, one line, show the diff. If a line starting ``- `04_Methodology/Playbooks/`:`` exists, append `, evaluator-agent` to it. If not, add one line directly under the `04_Methodology` line, indented two spaces, like the sub-lines under `02_Work/`: ``- `04_Methodology/Playbooks/`: evaluator-agent``.
   - The memory pointer: read the vault's `CLAUDE.md` for where pointers to playbooks go and when. The usual rule is one line in Claude's own auto-memory, pointing at the FOLDER (never the playbook file inside it), written in the words the owner would use to ask for it. If their rule says pointers land only once a playbook is confirmed, do not write it now: tell the owner it will be written in the session where they say yes to the playbook.
   - Edit `99_Meta/filing-log.md`: append one line, in the shape that log already uses.
4. **Write the two new files with the Write tool, and change `Home.md` and `filing-log.md` with the Edit tool** (⛔ never overwrite either of them whole). Never use `cat >`, `cp` or any other shell command: a my-second-brain vault's frontmatter guard refuses notes born through the shell, and it should.
5. **Read the two files back** and show the owner the playbook whole. If they read it now and say yes to it, you may set `confirmed_by_owner: true` then, and write the memory pointer if it was waiting on that. Otherwise say plainly: `confirmed_by_owner` stays false until they have read it and said yes. Either way, the door's first row is the test of whether it works for them. Tell them the `[untested]` rule too: after their first real use, each `[untested]` sentence that run exercised either loses its tag (it held) or gets deleted or rewritten (it did not).

## 3. Case B: offer to save a copy in their notes

1. **Already saved?** First look for the pointer that `SKILL.md` step 1 would find (in their memory, or in the `CLAUDE.md` of the folder they work from). If it names a copy that exists, stop and follow "Updating" below instead of offering to save another copy.
2. Tell the owner: "The playbook works straight from the skill with nothing saved. If you want your three jobs and a log of past runs kept, I can save a copy in your notes. Updating the skill replaces its own copy, so anything you add there would be lost." Offer this once.
3. **If they want a copy:** ask where, ask the same one question from case A step 2, then show the exact list and get one yes:
   - The two files in the folder they named, with the three jobs filled in, stamps kept, and the door's `updated:` set to today.
   - One durable pointer, so a later session finds the copy instead of the seed. Put it where their setup already keeps standing instructions: their memory system if they use one, otherwise one line in the `CLAUDE.md` of the folder they work from. The line names the copy's folder, for example: ``For an evaluator, reviewer, auditor or judge, read the door and playbook in `<folder>` first.`` If that `CLAUDE.md` exists, add the line with the Edit tool; never overwrite it.
   Then write with the Write tool, read the files back, and follow case A step 5.
4. **If they do not:** say plainly that nothing is kept between runs and nothing was written, then tell them how to use it (below).

## 4. Case C: the skill is the source

Nothing to write. Tell the owner: "The playbook lives at `~/.claude/skills/breakthrough-evaluator-agent/playbook/evaluator-agent/`. When you want a judge, say 'send a judge' or 'audit this', and the skill reads that folder. Nothing from a run is kept." Offer once to save a copy as in case B, in a folder they choose; if they say yes, follow case B step 3.

## 5. What you never do

- ⛔ Never install through a subagent. Every value written above is one this session saw with its own eyes.
- ⛔ Never overwrite a file that already exists, and never touch a door's "What we have learned" or "Recent runs" during an update.
- ⛔ Never invent or amend the owner's doctrine. Every current my-second-brain vault already has the `playbook` family and `guide_family: playbook`; if this one lacks them, it is case B.
- ⛔ Never write anything the owner has not seen first. Show the list, get the yes, then write.
- ⛔ Never fetch anything from the network without the owner's yes, updates included.
- ⛔ Never set `confirmed_by_owner` to true unless the owner has read the playbook and said yes to it.
- ⛔ Never run the playbook during the install. Installing it is not using it.

## Updating

With the owner's yes (it uses the network):

```
npx skills update breakthrough-evaluator-agent -g -y
```

The skill's seed is replaced by the new version. The owner's saved copy (case A or case B) is never touched by that command. Compare the stamps of each of the two files separately: `grep -m1 'seed:'` on the owner's copy and on the matching new seed. If a stamp is missing from the owner's copy, or is newer than the payload's, stop and show the owner what you found; do not merge. If the seed is newer:

1. Read the entries in the skill's `CHANGELOG.md` between the two versions.
2. `diff -u` the owner's copy against the new seed.
3. Merge one section at a time, showing each change and getting the owner's yes before applying it with the Edit tool. A section they decline stays as they have it.
4. Bump the stamp in the owner's copy of that file to the new version. The stamp records which version they have ruled on, not which text they took.
