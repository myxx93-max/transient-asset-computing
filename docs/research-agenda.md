# Research Agenda

## Research questions

- **RQ1 — Residue:** Does explicit retirement reduce task-specific executable residue without losing required evidence?
- **RQ2 — Adaptation:** Under changing task requirements, does dynamic composition reduce rework enough to offset discovery and validation overhead?
- **RQ3 — Governance:** Do contracts, provenance, and least-authority grants reduce incompatible or unauthorized composition?
- **RQ4 — Recovery:** Can a composition be retired while preserving sufficient evidence for diagnosis, compensation, and permitted resumption?
- **RQ5 — Promotion:** Does gated promotion produce a more reliable reusable asset pool than automatic retention of successful task artifacts?

## Hypotheses

- H1: TAC reduces retained task-specific executable structure for variable task families relative to persistent composition.
- H2: Lower executable residue does not necessarily imply lower total storage because audit records and final outputs may remain.
- H3: Contract and provenance checks reduce incompatible composition events but add discovery and validation latency.
- H4: Selective promotion reduces invalid reusable assets relative to automatic promotion.
- H5: Fixed compositions may outperform TAC on stable, repetitive workloads.

## Baselines

1. Persistent application or workflow composition.
2. Ephemeral execution without explicit asset governance and promotion.
3. TAC: governed assets, task-scoped compositions, controlled adaptation, and selective promotion.

## Workload design

Include both stable and variable tasks, and deliberately test:
- success and partial completion;
- failure and cancellation;
- changed requirements during execution;
- unavailable or version-incompatible dependencies;
- permission revocation;
- human intervention;
- retry, compensation, and resume;
- attempted promotion of incorrect or unsafe outputs.

## Measures

- correctness and task completion rate;
- composition and validation latency;
- end-to-end latency;
- compute and storage consumption;
- retained task-specific executable artifacts;
- evidence sufficiency after retirement;
- recovery success and time;
- permission scope and policy violations;
- invalid asset-promotion rate;
- human intervention and maintenance effort.

## Methodological safeguards

Pre-register task families, baselines, metrics, and acceptance criteria. Separate stable from variable workloads. Report negative results and overhead. Avoid claiming general superiority from a small set of successful demonstrations. Compare equivalent functionality and security boundaries across baselines.

## Open implementation questions

- What is the minimal machine-readable asset contract?
- How should task identity and authority propagate through nested compositions?
- Which state must be durable for long-running tasks?
- How can asset provenance be verified across registries and execution environments?
- What evidence is sufficient to promote a task artifact into a reusable asset?
- How should composition caches expire and be invalidated?
