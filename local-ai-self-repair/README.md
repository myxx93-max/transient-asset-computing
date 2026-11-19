# Self-Repairing Local AI Systems

**Research track — discussion and theory stage**

## Research question

Can a locally operated AI system observe its own task performance, diagnose failures across model, inference-runtime, and agent-workflow layers, propose a bounded repair, validate that repair independently, and safely promote or roll it back?

This track focuses on **operational self-repair**, not simply faster inference or unconstrained self-modification.

## Why investigate this?

Local AI systems combine several layers whose failures can look similar from the outside:

- model behavior and prompt/context effects;
- inference runtime, quantization, memory pressure, and device placement;
- tool adapters and agent orchestration;
- task definitions, evaluation data, and external dependencies.

A weak task result does not by itself identify which layer failed. A repair that improves one example may also regress other tasks. The research problem is therefore to establish a controlled loop with independent evidence and reversible changes.

## Proposed loop

1. **Observe** — collect task outcomes, runtime signals, resource measurements, and intervention records.
2. **Localize** — distinguish model, runtime, tool, orchestration, and task-specification failures.
3. **Propose** — generate a bounded repair hypothesis and an explicit change set.
4. **Isolate** — apply the candidate in a disposable or versioned environment, not directly to the trusted baseline.
5. **Validate independently** — use frozen holdout tasks, regression tests, safety checks, and resource measurements.
6. **Decide** — promote only when predefined criteria pass; otherwise reject and roll back.
7. **Record** — retain provenance, metrics, failure explanations, and the exact change lineage.

## Research boundaries

The loop may propose several distinct classes of change. They must not be conflated:

- **Inference configuration:** batching, context limits, device placement, quantization/runtime options.
- **Agent workflow:** tool routing, retry policy, context construction, task decomposition.
- **Model artifact:** adapters, patches, weight-space edits, or fine-tuning.
- **Evaluation system:** test coverage, benchmark validity, and regression detection.

A successful configuration change does not prove that model weights improved. A successful benchmark run does not prove better real-world task performance.

## Initial hypotheses

- H1: Layer-aware diagnosis reduces repair attempts applied to the wrong subsystem.
- H2: Independent frozen evaluation reduces false promotion compared with self-evaluation by the repairing agent.
- H3: Reversible changes and explicit rollback reduce the operational cost of failed repairs.
- H4: Some apparent model failures are caused by runtime or workflow conditions rather than model parameters.
- H5: For some workloads, the cost and complexity of self-repair exceed the benefit; a fixed, manually maintained configuration remains preferable.

These are hypotheses, not results.

## What would count as evidence?

For each repair attempt, record:

- task family and baseline version;
- observed failure and diagnostic evidence;
- suspected failure layer;
- proposed change and rationale;
- isolated execution environment;
- frozen evaluation set and acceptance thresholds;
- before/after quality, latency, memory, throughput, and regression results;
- promotion or rollback decision;
- reproducibility instructions.

Include failed repairs and neutral results. Do not report only successful examples.

## Current status

This is an open research direction. No claim is made that the local system already autonomously repairs itself, that weight-space editing has demonstrated reliable gains, or that any particular GPU configuration is optimal. A reference implementation and controlled evaluation are future work.

## Relationship to Transient Asset Computing

The two tracks are related but distinct:

- **Transient Asset Computing** studies how task-specific software compositions form, adapt, and retire around changing demand.
- **Self-Repairing Local AI Systems** studies how the execution substrate diagnoses and safely repairs failures.

A future system could use validated self-repair procedures as persistent capability assets and invoke them inside task-scoped compositions. That integration is a research possibility, not an implemented capability.
