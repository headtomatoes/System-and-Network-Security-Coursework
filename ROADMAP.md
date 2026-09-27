# Roadmap — pre-course preparation

Prep for a System & Network Security module starting **7 Sep 2026**.
This file holds the plan and the prep-plan vocabulary. Security terminology lives in
[CONTEXT.md](CONTEXT.md) — see the note at the top of that file for why they are split.

## The constraint

Today is 8 Aug 2026. That is 30 days at **4 h/week maximum** = **~17.1 hours, hard
ceiling**. Every decision below is downstream of that number. This is not enough time
to cover a module's worth of material and no plan here pretends otherwise.

## The goal

Close the **Prereq Gap** — not front-run the syllabus, not optimise for marks.
Success is measured in week 1: when a lecturer says "you all know how X works" and
moves on, we do.

Rejected alternatives and why:
- *Front-run the syllabus* — the course teaches that content anyway; the prereqs it
  never will.
- *Build the assessed artifact early* — the brief is unknown; would be guesswork.
- *Optimise for the grade* — efficient for marks, weakest for capability.

## Budget

| # | Block | Hours | Mode | Blocked on syllabus? |
|---|-------|-------|------|----------------------|
| 1 | **Diagnostic** — 8 areas × ~4 questions | 0.75 | I ask, you answer | No |
| 2 | **Lab** — build it | 4 | Build | No |
| 3 | **Glossary** — fill `CONTEXT.md` | 4 | Direct exposition | **Yes** |
| 4 | **Deep Block** — worst diagnosed gap | 7 | Socratic mentor mode | **Yes** |
| | *Slack* | *1.35* | | |

> **Flagged:** the Deep Block was verbally agreed at 8 h, but 8 h leaves only 0.35 h of
> slack — effectively none, which defeats the agreed intent of holding a buffer. It is
> written here as **7 h** to deliver ~1.35 h of real slack. Revert to 8 h if running
> tight is preferred.

Slack is not spare capacity to allocate now. Zero-buffer plans slip; if nothing
overruns it is spent on the Deep Block at the end.

## Vocabulary

**Prereq Gap** — the difference between what the module *assumes* you already know and
what you actually know. The target of all four blocks. Its content is unknown until the
Diagnostic runs.

**Diagnostic** — a ~40-question probe across the eight assumed-background areas, ~4
questions each. Chosen over self-report specifically to surface *unknown* unknowns,
which self-assessment cannot reach. Its single output is the ranked gap list that
selects the Deep Block's subject.

**Assumed-background areas** — the eight candidate prereq areas: TCP/IP & the wire;
applied crypto; OS & memory; C & low-level; Linux CLI & sysadmin; web & HTTP; tooling
fluency; security theory.

**Lab** — the VM environment that must survive the whole module: VMware Workstation Pro
hosting Kali plus Metasploitable 2 on an isolated host-only network. Platform rationale
in [ADR 0001](docs/adr/0001-vmware-workstation-lab.md); safety constraints in
[gotchas](docs/gotchas.md). Built early because setup during term costs an evening
there won't be one to spare.

**Glossary** — Block 3's deliverable: one tight paragraph per term the module will use,
written into `CONTEXT.md`. Targets *recognition*, not recall — a term read once is a
term that no longer stops you mid-slide. Explicitly not a spaced-repetition deck;
recall is not the week-1 bottleneck.

**Deep Block** — the single largest investment, spent on the worst gap the Diagnostic
finds. Run in Socratic mentor mode (see `code-mentor`), because this is the one thing
that must be genuinely owned rather than recognised.

## Sequencing

1. **Diagnostic** — runs on request, independent of the syllabus. Not yet started.
2. **Syllabus arrives** — the hard blocker. Drop the module handbook, unit outline,
   reading list or assessment brief into this directory. Until then Blocks 3 and 4
   cannot start without a substantial share of the 17 h landing off-target, and that
   error is unrecoverable — the runway is gone by 7 Sep.
3. **Lab** — can proceed in parallel with 1 and 2.
4. **Glossary**, then **Deep Block**.

## Open risks

- **Syllabus unread.** Blocks 3 and 4 currently assume a generic module. It would also
  confirm or supersede ADR 0001 if the module mandates a hypervisor or ships images.
- **Budget is a ceiling, not an estimate.** 4 h/week is stated as a maximum. One missed
  week is ~23% of the entire runway; there is no recovery path for two.
- **Metasploitable 2 is dated (2012).** Deliberate — TCP, ARP, DNS and service
  enumeration have not changed, and it is the most-documented target available. It is
  useless for modern web vulnerabilities and for Windows/AD, so if the syllabus covers
  either, the Lab needs a third VM and the 4 h estimate is wrong.
