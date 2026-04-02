# Introduction

Michael Nygard's Architectural Decision Record idea (https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions) is a compelling approach to documenting how and why a codebase's architecture evolves. In practice, ADRs speed up onboarding, reduce the likelihood of repeating past mistakes, and provide the reasoning behind current decisions — even as team composition changes. As LLM-assisted coding becomes more common, ADRs also help guide agents toward changes that are consistent with a project's architectural history.

ADRs have spread widely across the software industry since their introduction, earning recognition as an established best practice. Major cloud providers — including [AWS](https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/welcome.html), [Azure](https://docs.cloud.google.com/architecture/architecture-decision-records), and [GCP](https://docs.cloud.google.com/architecture/architecture-decision-records) — have published dedicated guidance endorsing the approach. The breadth of adoption speaks for itself: the benefits clearly outweigh the discipline required to maintain them.

# What is an RDR?

The same core idea — recording a decision with its status and potential consequences — translates naturally to research projects. Unlike software development, research has no guaranteed path to success; progress comes from iterating through ideas and measuring each against a common baseline. Feature engineering in traditional machine learning is a good example: many approaches are tried before a satisfactory one is found. A Research Decision Record (RDR) documents this search process, capturing what was tried, why, and what was learned — much as an ADR captures how and why an architecture changed over time.

LLM-assisted workflows have dramatically increased the pace at which ideas can be implemented and tested. The downside is that a high volume of experiments can quickly turn a research codebase into a mess. RDRs address this on two fronts: they provide a central record of findings and progress for human collaborators, and they give agents a structured history to consult — so they don't revisit dead ends or lose sight of what has already been established.

For this to work, the record must be kept up to date. One practical way to enforce this is to encode the RDR process in a `CLAUDE.md` file, which causes Claude to append entries automatically at the appropriate points.

```md
# Instructions for Claude

## Research Decision Records (RDR)

**CRITICAL WORKFLOW**: When a user requests something that might be a new research direction, ALWAYS ASK FIRST:

> "This seems like a new research direction. Should I create a new RDR entry for this in RDR.md?"

**Wait for user confirmation** before updating `RDR.md`.

### What Constitutes a Research Direction?

Ask the user about creating an RDR when:
1. Implementing a new feature engineering approach
2. Changing data preprocessing or filtering strategies
3. Modifying model selection or hyperparameter tuning methodology
4. Introducing new evaluation metrics or validation strategies
5. Making architectural decisions about the ML pipeline
6. Choosing between alternative research approaches

### What Does NOT Need an RDR?

Do not ask about RDR for:
- Bug fixes
- Code refactoring without methodology changes
- Documentation updates
- Visualization tweaks (unless new visualization methodology)
- Minor parameter adjustments (unless part of systematic tuning study)
- Exploratory code that won't be kept

### RDR Entry Format (When Approved)

Use this concise template for new entries:

```markdown
---

## RDR-XXX: [Short Title]

**Status:** [Proposed/Implemented/Superseded] | **Date:** YYYY-MM

**Context:** [1-2 sentences: What problem needs solving?]

**Decision:** [2-3 sentences: What was decided? Be specific about implementation.]

**Rationale:** [1-2 sentences: Why this approach?]

**Consequences:**
- ✓ [Positive outcomes, expected benefits]
- ✗ [Negative outcomes, tradeoffs, limitations]

**Open Questions:** [Optional: Unanswered questions or hypotheses to validate]

**Alternatives:** [Brief list of rejected alternatives with reasons]

**Implementation:** [File names and artifacts] → [Outputs]
```

### RDR Numbering

- Continue sequential numbering (RDR-001, RDR-002, etc.)
- Do not reuse numbers even if an RDR is superseded
- Mark superseded RDRs with **Status: Superseded by RDR-XXX**

### Updating Existing RDRs

Update an existing RDR when:
- Adding performance results to "Open Questions"
- Marking status changes (Proposed → Implemented)
- Noting when it's been superseded
- Adding new consequences discovered after implementation

**Format for updates:**
```markdown
**Update [YYYY-MM]:** [Brief description of what changed]
```

---

### Pipeline Usage

```bash
python pipeline.py --feature-generation --visualization --training --version <version_number>
```

---

## Remember

**🚨 ALWAYS ASK USER BEFORE UPDATING `RDR.md` 🚨**

The user decides what constitutes a research decision worth documenting.
```

# Additional usecases

Beyond guiding agents, a central record of ideas also makes individual entries easier to reference across sessions. New directions often build on earlier, less successful attempts, so having them in one place supports the kind of structured exploration that good research requires.

The RDR can also capture the relationships between ideas, making it straightforward to generate a diagram that maps the research landscape — useful for presentations, retrospectives, or simply keeping the bigger picture in view. One such example is shown below:

![RDR example diagram](rdr_example.png)
