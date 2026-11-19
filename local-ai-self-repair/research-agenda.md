# Research Agenda: Self-Repairing Local AI Systems

## Research questions

- **RQ1 — Fault localization:** Can a system distinguish model-behavior failures from inference-runtime, tool, orchestration, and task-specification failures?
- **RQ2 — Repair quality:** Which classes of repair improve held-out task performance rather than overfitting observed failures?
- **RQ3 — Independent validation:** How much does frozen, independent evaluation reduce false-positive repair promotion?
- **RQ4 — Reversibility:** What provenance, snapshots, and rollback guarantees are required for safe experimentation?
- **RQ5 — Economics:** Under which workload conditions does automated diagnosis and repair cost less than manual intervention or a fixed configuration?

## Baselines

1. Manual diagnosis and repair.
2. Agent-proposed repair evaluated by the same agent.
3. Agent-proposed repair with independent frozen evaluation and rollback.
4. No-repair baseline.

## Failure taxonomy

| Layer | Example symptom | Candidate evidence |
|---|---|---|
| Model | Inconsistent reasoning or instruction following | Frozen task set, output comparisons |
| Inference runtime | OOM, unstable throughput, incorrect device placement | Runtime logs, memory and device metrics |
| Agent workflow | Tool misuse, repeated calls, context loss | Tool traces, state transitions |
| Task specification | Ambiguous or contradictory acceptance criteria | Task contract and clarification history |
| External dependency | API, data source, or service unavailable | Dependency status and error records |
| Evaluation | Misleading score or contaminated holdout | Dataset lineage and evaluator audit |

## Required safeguards

- Keep a known-good baseline immutable.
- Apply candidate repairs in isolated worktrees, containers, or equivalent disposable environments.
- Freeze evaluation tasks before tuning.
- Separate diagnostic data from holdout evaluation data.
- Require explicit acceptance thresholds before experiments.
- Track regressions across unrelated task families.
- Preserve exact artifact hashes and configuration lineage.
- Roll back automatically when hard safety or regression gates fail.
- Never allow the repairing agent to expand its own permissions.
- Treat model-generated explanations as hypotheses, not evidence.

## Metrics

- fault-localization accuracy;
- repair acceptance and false-promotion rates;
- held-out task quality;
- regression rate;
- repair time and human interventions;
- inference latency, throughput, memory, and compute cost;
- rollback success and recovery time;
- reproducibility across repeated runs.

## Weight-space editing as a sub-track

Weight-space programming and model-weight edits are one possible repair class, not the definition of self-repair. They require separate controls:

- immutable source checkpoint and cryptographic identity;
- sparse, bounded, reversible patch representation;
- layer/tensor-level change manifest;
- deterministic patch application and reversal;
- task-specific and general regression suites;
- evaluation across multiple seeds where stochasticity matters;
- explicit comparison against non-weight alternatives such as prompt, runtime, and workflow changes.

No weight modification should be promoted based on a single task or self-reported improvement.

## Negative results

Publish failed localization, neutral repairs, regressions, and cases where manual or fixed configurations outperform automation. These are central evidence, not incidental implementation details.
