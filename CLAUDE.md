# Research reasoning log

Before suggesting a new approach for data preprocessing, feature engineering, model selection, or evaluation methodology, check `RDR.md` for prior attempts in that area. This isn't a formality — if an approach was tried and abandoned, the entry will explain why, and that reasoning should inform what you suggest next.

- Check `RDR.md` at the start of any session where methodology may be discussed
- If an entry is relevant, reference it explicitly before suggesting alternatives
- Do not re-propose an abandoned approach unless the context has materially changed

If the user approves a new direction that represents a significant methodological change, ask whether to add an entry to `RDR.md`. Not every experiment warrants an entry — the bar is whether a future collaborator (human or agent) would benefit from knowing why this path was taken or left.

- Significant changes include: new feature engineering strategies, changes to preprocessing logic, model selection methodology, evaluation metrics, or pipeline architecture
- Routine changes do not need entries: bug fixes, refactors, parameter sweeps, exploratory code that won't be kept
- When in doubt, ask the user

## How to write an entry

Each entry should read as a short story, not a filled-in form. Write in prose and let the reasoning flow naturally from problem to attempt to outcome. The goal is that someone reading it cold — with no other context — understands not just what happened, but why it made sense at the time and what it ruled out going forward.

- Write at least one full paragraph per section; avoid bullet-only entries
- Use past tense: this is a record of what happened, not a plan
- Be specific about numbers, file names, and outcomes where they matter

### Entry structure

Each entry has three prose sections, each followed by supporting bullets.

---

**RDR-XXX: [Title]** | *[YYYY-MM]* | Status: [Implemented / Proposed / Superseded]

**The problem.** Describe what gap or failure motivated this direction. What were we trying to fix or improve, and why did the existing approach fall short? A reader should understand the pressure that made this change feel necessary.

- What the previous state was
- What specific failure mode or limitation drove the change
- Any constraints that shaped the solution space

**What we tried and what we found.** Describe the approach and what happened when it was implemented. Include concrete results — metrics, observations, surprises. If the outcome was negative, say so plainly and explain what made it negative.

- Key implementation choices and why they were made
- Quantitative results where available (e.g., AUC, RMSE, calibration error)
- Anything unexpected that emerged during testing

**Why we moved on (or why we're staying).** Explain the conclusion: was this approach adopted, abandoned, or set aside? If abandoned, what specifically disqualified it, and is there any scenario where it might be revisited? If adopted, what does it leave open?

- Final status and reasoning
- Conditions under which this decision should be reconsidered
- What this rules out going forward

---

Keep entries short enough that filling one in takes five minutes. If it starts to require extensive alternatives analysis or detailed consequence breakdowns, the entry is too ambitious — split the reasoning or summarize more aggressively.
