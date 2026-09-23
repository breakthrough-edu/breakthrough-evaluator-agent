# breakthrough-evaluator-agent

When the AI that built something also checks it, it tends to pass its own work. This kit gives your Claude Code a written way to send a **judge that is not the author**: a fresh agent that never saw how the work was made, checks it against criteria you wrote down beforehand, and brings back evidence for every verdict.

It works in two modes:

- **Evaluator mode**: one finished piece (a landing page, a post, an SOP) judged against pass criteria written before it was made, round by round, until it passes or hits a round cap.
- **Audit mode**: a batch (a folder, a registry, a database table, a folder move) checked against its source of truth, with a list of exceptions handed back to you.

What you get is a playbook (when to send a judge, what to weigh, the moves, a brief to fill in and an output format) plus a small skill that points Claude at it.

## Install

Paste this one line into Claude Code:

```
Read https://raw.githubusercontent.com/breakthrough-edu/breakthrough-evaluator-agent/main/INSTALL.md and install it for me.
```

## What the install will do

- Ask your permission before it downloads anything.
- Check what kind of notes you keep, then do one of three things:
  - **You run a my-second-brain vault:** it asks you one question (three real jobs in your business that need an independent check, and what goes wrong today without it), shows you exactly what it will add (the playbook folder and its door with your answer written in, one line on your Home page, one line in your filing log, and a memory pointer if your vault's rules call for one), then writes them after your yes.
  - **You keep notes some other way:** it offers once to save a copy of the playbook in a folder you name. If you say yes, it asks you the same one question, shows you the files plus one pointer so later sessions find your copy, then writes them after your yes. If you say no, it writes nothing.
  - **You keep no notes:** it writes nothing and the playbook works straight from the skill, with nothing kept between runs. It offers once to save a copy if you want your jobs and past runs kept.

## What it will not do

- Overwrite any file you already have, or change your vault's rules.
- Mark the playbook as confirmed unless you have read it and said yes.
- Run a judge during the install.
- Fix your work. The judge only reports, with evidence. (It runs as an ordinary subagent that could write files, so "never fixes" is an instruction; the playbook tells Claude to check afterwards that nothing was touched.)

## Status

v1.0.0. Sentences marked `[untested]` in the playbook come from published research and have not yet been tried in your business. After your first real use, each one you exercised either loses the tag or gets rewritten.

## License

MIT. See [LICENSE](LICENSE).
