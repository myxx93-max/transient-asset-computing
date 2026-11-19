# TAC Architecture

## Logical model

The architecture separates two lifecycles:

- **Persistent capability assets**: governed, versioned, discoverable capabilities and knowledge.
- **Transient task compositions**: executable structures assembled for a bounded task and retired during finalization.

The five logical planes are responsibilities, not required infrastructure products.

| Plane | Responsibility | Key outputs |
|---|---|---|
| Asset | Discover, version, govern, and authorize reusable capabilities | Asset metadata, contracts, provenance |
| Task intent | Define objective, constraints, authority, and acceptance | Task specification |
| Composition | Select compatible assets and connect them | Task-scoped execution graph |
| Execution/observation | Execute, monitor, record transitions and exceptions | Outputs, traces, intervention records |
| Finalization/learning | Compensate, revoke, retire, classify, and selectively promote | Retired composition, retained evidence, candidate assets |

## Lifecycle

1. Declare task and authorization boundary.
2. Discover candidate assets and inspect contracts.
3. Compose a task-scoped graph.
4. Validate interfaces, policy, permissions, and preconditions.
5. Execute with observation.
6. Adapt only through recorded and validated transitions.
7. Finalize success, failure, cancellation, or blocked state.
8. Classify outputs for discard, retention, archive, quarantine, or promotion.
9. Retire task-specific executable structure and temporary grants.

## Key separation

Retiring a composition is not equivalent to deleting all task data. The system may retain final deliverables, audit evidence, and reproducibility records according to policy. Temporary credentials must be revoked. A discovered rule is only a candidate until validated and promoted.

## Architectural invariants

- Every composition has a task identity and terminal policy.
- Assets are reused through declared contracts and compatibility checks.
- Task authority is explicit and least-privilege.
- Provenance connects outputs to asset versions and composition decisions.
- Runtime adaptation is recorded and cannot silently expand authorization.
- Failure and cancellation have explicit cleanup and recovery semantics.
- Promotion is gated; successful execution alone is not proof of reusable correctness.
- Concurrent compositions are isolated.
- Composition growth is bounded and observable.

## Non-goals

TAC does not require microservices, serverless infrastructure, LLM planning, a particular asset registry, or deletion of all state at task end. It is compatible with fixed workflows when task requirements are stable and composition overhead is not justified.
