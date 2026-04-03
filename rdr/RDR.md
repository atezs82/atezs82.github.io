# Introduction

Michael Nygard's Architectural Decision Record idea (https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions) is a compelling approach to documenting how and why a codebase's architecture evolves. In practice, ADRs speed up onboarding, reduce the likelihood of repeating past mistakes, and provide the reasoning behind current decisions — even as team composition changes. As LLM-assisted coding becomes more common, ADRs also help guide agents toward changes that are consistent with a project's architectural history.

ADRs have spread widely across the software industry since their introduction, earning recognition as an established best practice. Major cloud providers — including [AWS](https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/welcome.html), [Azure](https://docs.cloud.google.com/architecture/architecture-decision-records), and [GCP](https://docs.cloud.google.com/architecture/architecture-decision-records) — have published dedicated guidance endorsing the approach. The breadth of adoption speaks for itself: the benefits clearly outweigh the discipline required to maintain them. The same core idea translates naturally to research — though the format needs to change.

# What is an RDR?

Tools like MLflow, Weights & Biases, and Neptune do a good job of recording what happened in an experiment: metrics, parameters, artifacts, run history. What they don't capture is *why you tried something* and *why you stopped*. That reasoning lives in the researcher's head, gets mentioned in a Slack message, or disappears entirely when the project moves on.

This gap is small when a single person works on a project from start to finish. It becomes costly when collaborators join mid-project, when a project resumes after months of dormancy, or when an LLM agent is assisting with implementation — none of these can recover intent from a dashboard.

A Research Decision Record (RDR) fills this gap with a short markdown file that logs significant direction changes — not every experiment, but the moments when you pivot, abandon an approach, or make a methodological choice that will shape subsequent work. Each entry answers three questions:

1. What were you trying to achieve?
2. What did you try, and what did you find?
3. Why did you move on?

A minimal entry looks like this:

```markdown
## RDR-003: Switched from SMOTE to class-weighted loss

**Date:** 2025-03

**What we tried:** SMOTE oversampling to address class imbalance in the training set.

**What we found:** Validation AUC improved slightly (+0.02) but calibration degraded significantly. Oversampled minority class examples were synthetic and didn't reflect real distribution tails.

**Why we moved on:** Class-weighted loss achieved comparable AUC with better calibration and no data leakage risk. SMOTE is off the table unless we revisit calibration requirements.
```

That format is deliberately minimal — but it becomes especially useful in LLM-assisted workflows. Experiment trackers don't help an LLM agent avoid repeating abandoned directions, because the agent doesn't query W&B before suggesting an approach — it works from what's in context. A markdown file explicitly included in the project context does.

The benefit is narrow but real: when starting a new session, you can include the reasoning log in context and the agent has a factual basis for knowing that a given approach was tried and rejected, not because it was overlooked. This won't work if the file grows to hundreds of entries and exceeds the context window — which is precisely why the bar for creating an entry should be high.

An example `CLAUDE.md` instruction that supports this workflow looks like [this](./CLAUDE.md).

# When this is worth maintaining

This is worth the overhead when:

- The project involves significant methodological exploration, not just hyperparameter tuning
- Multiple people or sessions are involved
- LLM agents are regularly assisting with implementation

It is probably not worth it for short-lived projects, solo work with continuous context, or domains where the experiment tracker already captures sufficient reasoning in run descriptions.

The discipline cost is real. The template should stay short enough that filling it in takes two minutes, not twenty. If entries start requiring an "alternatives considered" section and a consequences breakdown, the overhead will kill the habit.

# Acknowledgements

Many thanks to [Patrik Egyed](https://www.linkedin.com/in/pregnor) for the original idea back in 2018 when we worked together!
