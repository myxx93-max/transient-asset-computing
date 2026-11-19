# Transient Asset Computing

**An asset-centric architecture for task-formed, ephemeral software**

Transient Asset Computing (TAC) is a proposed architectural model in which reusable capabilities remain available as governed assets, while executable software structures are assembled dynamically around a task, adapted during execution, and dissolved when the task ends.

The central distinction is between **persistent capability assets** and **temporary task-specific software**. A task should not require a permanently growing application or a long-lived agent workspace merely because it needs a particular combination of capabilities once. Instead, a runtime can select compatible assets, compose a temporary execution structure, validate its behavior, and retire that structure after completion.

This repository contains a theory paper and a research agenda. It does **not** claim that TAC has been implemented, benchmarked, or proven superior to existing systems.

## Start here

- [Theory paper](paper/transient-asset-computing.md)
- [Architecture model](docs/architecture.md)
- [Related-work comparison](docs/related-work.md)
- [Research agenda and falsifiable hypotheses](docs/research-agenda.md)

## Core proposal

1. **Assets persist:** independently governed capabilities, contracts, policies, schemas, and verified knowledge can outlive individual tasks.
2. **Software forms around tasks:** the runtime selects and composes assets into a task-scoped executable structure.
3. **Composition is dynamic:** the structure may be adapted as evidence, constraints, or task state changes.
4. **Execution has an explicit end:** temporary orchestration, bindings, intermediate state, and task-specific glue are retired at finalization.
5. **Knowledge is selectively retained:** outputs are evaluated and classified for discard, archive, promotion, or quarantine rather than being retained indiscriminately.

## Public examples

- [Dynamic granule lifecycle](examples/dynamic-granule-lifecycle.md)
- [Illustrative asset relation schema](examples/asset-relation-schema.json)
- [Anonymized negative-knowledge case study](examples/negative-knowledge-case-study.md)

These examples are deliberately abstract and contain no production datasets, credentials, internal paths, or platform-operational details.

## Related research track: Self-Repairing Local AI Systems

A separate but potentially complementary research direction asks whether a local AI execution system can diagnose failures across model, inference-runtime, and agent-workflow layers; propose bounded and reversible repairs; validate them independently; and promote or roll them back using explicit criteria.

- [Research track overview](local-ai-self-repair/README.md)
- [Falsifiable research agenda](local-ai-self-repair/research-agenda.md)
- [Related-work map](local-ai-self-repair/related-work-map.md)
- [Anonymized dual-GPU inference case study](local-ai-self-repair/case-study-dual-gpu-local-inference.md)
- [Open research discussion](https://github.com/myxx93-max/transient-asset-computing/issues/2)

This is a research proposal, not a claim that autonomous self-repair or reliable weight-space improvement has already been demonstrated. The TAC and self-repair tracks remain distinct; possible integration is future work.

## Scope and status

This is a theory-first proposal. It defines concepts, boundaries, design questions, and testable hypotheses. It is not a production framework, benchmark, or claim of priority over all related work. The relationship to agent sandboxes, serverless orchestration, dynamic composition, software product lines, and transactional agent runtimes is discussed explicitly.

## Suggested citation

> Anonymous. *Transient Asset Computing: An Asset-Centric Architecture for Task-Formed, Ephemeral Software*. Theory paper, 2026. https://github.com/myxx93-max/transient-asset-computing

## Contributions and discussion

Issues and pull requests are welcome, especially counterexamples, prior art, formalizations, and proposed experiments that could falsify the model.
