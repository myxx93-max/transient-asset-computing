# Transient Asset Computing: An Asset-Centric Architecture for Task-Formed, Ephemeral Software

**Anonymous theory paper — version 0.1 — November 2026**

## Abstract

Software systems increasingly rely on reusable services, tools, models, data resources, and autonomous agents. Yet reuse is commonly organized around persistent applications, services, workflows, or agent environments. This paper proposes **Transient Asset Computing (TAC)** as an architectural perspective in which durable capability assets are composed into temporary, task-specific software structures. The task—not the application boundary—is the primary unit around which executable composition forms. During execution, the composition may be revised as requirements, evidence, and constraints change. At task completion, task-specific orchestration, bindings, and intermediate state are explicitly retired, while reusable assets and selectively promoted outputs remain.

TAC separates the lifecycle of a capability from the lifecycle of the software structure that uses it. It is intended to address a recurring tension: persistent software structures make reuse and governance tractable, but can accumulate task-specific glue, stale assumptions, and maintenance obligations; fully ephemeral execution can reduce residue, but risks losing valuable knowledge and weakening auditability. TAC therefore proposes a two-timescale model: persistent, governed assets and ephemeral task compositions, joined by explicit contracts and lifecycle transitions.

This paper defines the model, its conceptual components, lifecycle, invariants, relationship to adjacent paradigms, and a falsifiable research agenda. It is a theoretical proposal, not an implementation report. No empirical performance, cost, reliability, or novelty claim is made.

**Keywords:** ephemeral software; dynamic composition; asset-centric computing; task-oriented architecture; software lifecycle; autonomous systems; runtime orchestration

---

## 1. Introduction

A task often requires a combination of capabilities that does not justify a permanent application. A one-off investigation may need a data connector, a parser, a classifier, a policy check, a report generator, and a delivery adapter. A recurring but changing task may need a different combination next time. In conventional systems, such work is frequently embedded in a persistent application, a growing workflow, a general-purpose agent environment, or a collection of scripts. These structures are useful, but they can turn temporary coordination decisions into durable maintenance obligations.

The question explored here is:

> Can software be organized so that reusable capabilities persist, while the task-specific software structure that connects them forms only when needed and dissolves when the task is complete?

We call this perspective **Transient Asset Computing (TAC)**. Its central unit is not a permanent application but a **task-scoped composition** assembled from independently governed assets. The composition is executable software: it contains bindings, control flow, temporary state, and execution policy. It has a defined beginning, a mutable working lifetime, and an explicit terminal transition.

TAC does not mean that all software should be short-lived. Nor does it imply that every task should be decomposed into microservices, that all state should be deleted, or that a language model should freely invent and execute code. The proposal distinguishes durable capability assets from temporary composition and treats retention as a governed decision.

### 1.1 Problem framing

Three concerns motivate the model:

1. **Composition residue.** Task-specific adapters, branches, prompts, scripts, and state can remain after their motivating task has ended.
2. **Changing task shape.** A fixed workflow may be poorly matched to tasks whose needed capabilities become clear only during execution.
3. **Indiscriminate persistence.** Retaining every intermediate artifact can create clutter and preserve obsolete or low-confidence assumptions; discarding everything can destroy useful discoveries and evidence.

These are architectural tensions, not claims that existing paradigms cannot address them. TAC asks whether making the lifecycle boundary explicit can improve the trade-off.

### 1.2 Contributions

This theory paper makes five limited contributions:

- Defines a distinction between persistent capability assets and ephemeral task compositions.
- Proposes a lifecycle for task-scoped composition, adaptation, finalization, and selective retention.
- Identifies contracts and invariants needed to make ephemeral composition governable.
- Positions the proposal relative to dynamic software composition, serverless computing, workflow systems, software product lines, microservices, and agent execution environments.
- Provides hypotheses and experiments that could refute or narrow the proposal.

The contribution is a conceptual synthesis and research agenda. Priority and empirical advantage remain unestablished.

## 2. Terminology and conceptual model

### 2.1 Capability asset

A **capability asset** is a reusable, independently identifiable unit that can contribute to task execution. Examples include a data source adapter, a parser, a domain rule set, a model endpoint, a schema, a validation procedure, or a policy module.

An asset is more than a code package. To be safely composable, it should expose metadata sufficient to evaluate its use:

- identity and version;
- capability description and declared inputs/outputs;
- interface or invocation contract;
- preconditions and postconditions where meaningful;
- permissions and policy constraints;
- provenance and trust status;
- dependencies and compatibility declarations;
- lifecycle and ownership information.

Assets may themselves be composed from other assets. TAC does not require a single physical representation or registry technology.

### 2.2 Task

A **task** is a bounded unit of intended work with an objective, constraints, acceptance conditions, and an execution context. A task may be atomic or contain subtasks. A task is not necessarily a user prompt: it may originate from a schedule, event, external signal, or another system.

A task description should distinguish known requirements from unresolved questions. This matters because the composition may need to change as uncertainty is reduced.

### 2.3 Transient composition

A **transient composition** is the task-specific executable structure formed by selecting and connecting assets. It includes, as applicable:

- asset bindings and configuration;
- execution graph or control flow;
- task-local adapters and glue;
- temporary credentials or capability grants;
- working memory and intermediate outputs;
- retry, compensation, and recovery logic;
- runtime monitoring and termination conditions.

The composition is transient in lifecycle, not necessarily brief in wall-clock duration. A long-running task can still have a bounded and explicitly governed composition lifecycle.

### 2.4 Task residue

**Task residue** is any task-specific executable structure or state that remains after the task's intended lifecycle has ended. Residue is not automatically harmful: some outputs must be retained. The design problem is to distinguish reusable assets and justified records from accidental persistence of temporary composition.

### 2.5 Selective promotion

**Selective promotion** is the controlled transition by which an output, observation, adapter, rule, or other task result is evaluated for a longer-lived status. Possible outcomes include:

- discard;
- retain as task record;
- archive as evidence;
- quarantine pending validation;
- promote to a reusable asset with versioning and governance.

Promotion is not automatic. A successful task does not prove that every intermediate component is reusable or correct.

## 3. Architecture

TAC can be described as five cooperating logical planes. These are conceptual responsibilities, not mandatory deployment tiers.

### 3.1 Asset plane

The asset plane stores and governs reusable capabilities. It supports discovery, versioning, provenance, compatibility metadata, permissions, and lifecycle management. Assets should be addressable independently of any one task composition.

### 3.2 Task-intent plane

The task-intent plane represents the objective, constraints, acceptance criteria, known inputs, uncertainty, and authorization boundary. It should preserve the distinction between what the requester authorized and what the runtime infers as a possible implementation.

### 3.3 Composition plane

The composition plane selects assets and creates a task-specific execution graph. It resolves interfaces, constructs dependency relationships, applies configuration, and records why each asset was selected. Composition can be deterministic, policy-driven, planner-assisted, or hybrid.

### 3.4 Execution and observation plane

The execution plane runs the composition. The observation responsibility records state transitions, inputs and outputs at appropriate levels, errors, retries, human interventions, policy decisions, and termination evidence. Ephemeral execution must not mean unobservable execution.

### 3.5 Finalization and learning plane

The finalization plane evaluates completion, performs compensation or cleanup, revokes temporary grants, retires task-specific structures, and classifies outputs for retention or promotion. Promotion creates a governed asset version or evidence record; it does not silently mutate the trusted asset base.

## 4. Lifecycle model

A TAC task composition passes through a bounded lifecycle:

1. **Declare.** Establish task identity, objective, constraints, authorization, and acceptance conditions.
2. **Discover.** Identify candidate assets and inspect their contracts, versions, provenance, permissions, and compatibility.
3. **Compose.** Build a task-scoped execution graph and bind the required assets.
4. **Validate.** Check interface compatibility, policy compliance, resource limits, and preconditions before execution.
5. **Execute.** Run the composition while observing state, outcomes, exceptions, and interventions.
6. **Adapt.** If new evidence or a changed constraint invalidates the current plan, revise the composition through a controlled transition. Adaptation must preserve a recoverable history of relevant changes.
7. **Finalize.** Determine whether acceptance conditions were met; perform required compensation, release resources, and revoke temporary authority.
8. **Classify.** Decide what to discard, retain, archive, quarantine, or promote.
9. **Retire.** Remove the executable composition and task-only bindings from active service, subject to retention, legal, safety, and audit requirements.

A task can fail, be cancelled, or become blocked. These are terminal or suspended states, not successful completion. Cleanup and evidence preservation must be defined for each outcome.

### 4.1 Lifecycle state machine

A minimal state model is:

DECLARED → DISCOVERED → COMPOSED → VALIDATED → RUNNING ↔ ADAPTING → FINALIZING → CLASSIFYING → RETIRED

Exceptional transitions include BLOCKED, FAILED, and CANCELLED. A suspended task may resume only under an explicit policy that revalidates asset versions, permissions, and external assumptions.

### 4.2 Two timescales

TAC separates two lifetimes:

- **Asset lifetime:** potentially long-lived, governed, versioned, and reusable.
- **Composition lifetime:** bounded by a task or explicitly linked task series; task-specific structure is retired after finalization.

This separation is the central architectural claim. It is not a claim that assets are immutable or that compositions cannot be cached. Caching is compatible with TAC if cached structures have explicit identity, validity, isolation, and expiry rules.

## 5. Design principles and invariants

A TAC implementation should be evaluated against the following proposed invariants.

**I1 — Explicit task boundary.** Every composition has a task identity, owner or authority context, and terminal policy.

**I2 — Contract-mediated reuse.** Assets are composed through declared interfaces and constraints, not merely because their names or descriptions appear semantically similar.

**I3 — Least authority.** A composition receives only the permissions needed for its task and loses temporary grants at finalization.

**I4 — Provenance continuity.** The system can trace which asset versions, inputs, policies, and composition decisions contributed to an output.

**I5 — Controlled adaptation.** Changes to a running composition are recorded and validated; adaptation cannot silently expand the task's authorization.

**I6 — Explicit finalization.** Completion, failure, cancellation, and blocking each trigger defined cleanup and retention behavior.

**I7 — Selective persistence.** Reusable knowledge is promoted through validation and governance, not by indiscriminate retention.

**I8 — Recoverability.** The system preserves sufficient state and evidence to diagnose, compensate, or resume when policy allows, without requiring every transient detail to persist forever.

**I9 — Isolation.** Concurrent task compositions do not unintentionally share mutable task-local state or authority.

**I10 — Bounded composition growth.** The system detects unnecessary dependency expansion, unbounded adaptation, and composition complexity that exceeds task constraints.

These invariants are proposed design criteria. Their sufficiency and measurable operational definitions require further research.

## 6. What is transient, and what persists?

The distinction is functional rather than based on file type or storage medium.

| Element | Default lifecycle | Possible longer-lived outcome |
|---|---|---|
| Reusable parser or connector | Asset lifetime | Versioned asset |
| Schema or domain rule set | Asset lifetime | Governed asset |
| Task-specific binding | Composition lifetime | Usually discard |
| Temporary execution graph | Composition lifetime | Archive a description if needed |
| Intermediate result | Task lifetime | Retain as evidence or discard |
| Final deliverable | Task output | Retain under task policy |
| Newly discovered rule | Candidate | Quarantine, validate, then promote |
| Temporary credential/grant | Composition lifetime | Never promote; revoke |
| Execution trace | Task/audit policy | Retain proportionately |
| Failed adapter or recovery procedure | Candidate evidence | Reproduce, validate, then consider promotion |

This table is a default policy, not a universal retention mandate. Legal, safety, operational, and user requirements may override it.

## 7. Relationship to adjacent paradigms

TAC overlaps with established ideas. Its proposed distinction should be assessed as a combination and lifecycle framing, not presumed to be a wholly unprecedented mechanism.

### 7.1 Dynamic software composition and component-based software engineering

Component-based systems already assemble software from reusable components, and dynamic composition can alter components at runtime. TAC shares asset reuse and composition. Its emphasis is the explicit separation between long-lived governed capability assets and task-bounded executable compositions, including a first-class finalization and selective-promotion phase.

### 7.2 Microservices and service-oriented architecture

Microservices decompose systems into independently deployable services. TAC does not require a service boundary per asset or a permanently running service fleet. An asset may be a library, data resource, model, rule set, service, or procedure. The transient composition may invoke existing services without becoming another persistent service.

### 7.3 Serverless and Function-as-a-Service

Serverless systems abstract infrastructure provisioning and scale execution around invocations. TAC can use serverless execution, but the concepts differ: serverless describes an execution/deployment model, while TAC concerns the lifecycle of task-specific software composition and the governance of reusable assets and promoted outputs. A serverless function can be one asset in a TAC composition.

### 7.4 Workflow engines and orchestration

Workflow systems define and execute sequences or graphs of activities, often with durable state and recovery. TAC can use a workflow engine. The proposed difference is that the task composition itself is treated as a temporary object assembled from assets, with explicit rules for adaptation, retirement, and selective promotion. Durable workflow state may still be required for long-running tasks.

### 7.5 Software product lines and configuration systems

Software product lines generate or configure products from shared features and constraints. TAC shares variability management and reuse. It shifts the focal unit from a family of planned products to task-specific compositions that may form dynamically in response to a bounded objective and runtime evidence.

### 7.6 Autonomous agents and tool-using systems

Agents can plan, select tools, and execute multi-step tasks. TAC is compatible with agents but is not defined by an LLM or autonomous planner. A planner may propose a composition; contracts, authorization, validation, observation, and finalization govern it. The proposal deliberately avoids treating model-generated plans as trusted assets by default.

### 7.7 Containers, sandboxes, and ephemeral environments

Ephemeral environments provide isolation and can be destroyed after use. TAC may run a composition inside such an environment. But environment teardown alone does not solve asset discovery, compatibility, selective retention, provenance, or promotion. Conversely, TAC does not require all persistent assets to live outside the execution environment physically, provided their lifecycle and governance remain distinct.

## 8. Potential benefits and trade-offs

The following are hypotheses, not demonstrated results.

Potential benefits include:

- less accumulation of task-specific orchestration;
- easier replacement of one capability without redesigning a permanent application;
- more explicit authority and cleanup boundaries;
- clearer provenance from output to asset versions and composition decisions;
- reuse of validated capabilities without retaining every task-specific implementation;
- improved accommodation of tasks whose required composition changes during execution.

Potential costs and risks include:

- composition and validation overhead;
- asset discovery and metadata maintenance;
- version and compatibility complexity;
- runtime latency and dependency availability;
- difficult recovery for long-running or partially completed tasks;
- accidental deletion of state required for audit or reproducibility;
- security risks from dynamic dependency selection and confused-deputy behavior;
- promotion of low-quality outputs into the reusable asset pool;
- increased observability requirements.

TAC is not necessarily advantageous for stable, high-volume workloads where a fixed application or workflow is simpler and more efficient. A static composition may be the correct result when task shape is stable.

## 9. Research questions and falsifiable hypotheses

A theory proposal becomes useful only if it can be challenged empirically.

**RQ1 — Residue:** Does explicit retirement of task-specific compositions reduce retained task-specific executable artifacts compared with persistent workflow or agent implementations, without increasing loss of required evidence?

**RQ2 — Adaptation:** For tasks with changing requirements, does runtime composition reduce rework or improve completion quality compared with a fixed workflow, after accounting for composition overhead?

**RQ3 — Governance:** Do asset contracts, provenance, and least-authority grants reduce unauthorized or incompatible composition events?

**RQ4 — Recovery:** Can a task composition be retired while preserving enough evidence for reliable diagnosis, compensation, and policy-compliant resumption?

**RQ5 — Promotion quality:** Does a selective promotion process improve the precision of reusable assets compared with automatically retaining successful task artifacts?

### 9.1 Hypotheses

- **H1:** Under variable task requirements, TAC will reduce the amount of task-specific executable structure retained after completion relative to a persistent-composition baseline.
- **H2:** The reduction in retained structure will not necessarily reduce total storage, because audit evidence and reusable assets may still be retained.
- **H3:** Contract and provenance checks will reduce incompatible composition events, at the cost of discovery and validation latency.
- **H4:** Selective promotion will yield fewer invalid reusable assets than automatic promotion of successful task outputs.
- **H5:** For stable repetitive workloads, a fixed composition may outperform TAC on latency, operational simplicity, or cost.

### 9.2 Experimental design

A useful first evaluation would implement the same task families under three conditions:

1. persistent application/workflow composition;
2. ephemeral execution with no explicit asset-promotion model;
3. TAC with governed assets, task-scoped composition, and selective promotion.

Use both stable and variable task families. Include success, partial completion, failure, cancellation, changing requirements, unavailable dependencies, permission changes, and human intervention.

Measure:

- task completion and correctness;
- time to compose and validate;
- end-to-end latency;
- compute and storage consumption;
- number and complexity of retained task-specific artifacts;
- required evidence retained after retirement;
- recovery success and recovery time;
- policy violations and permission scope;
- invalid asset promotions;
- human interventions and maintenance effort.

Pre-register task definitions, acceptance criteria, baselines, and analysis. Include negative results. A benchmark that only measures successful short tasks would be insufficient.

## 10. Threats to validity and open problems

**Definition boundary.** The line between an asset and a composition can be context-dependent. A task-specific adapter may become reusable after repeated validation. The promotion rule needs operational criteria.

**Task granularity.** If tasks are too small, composition overhead dominates. If too broad, transient compositions become long-lived applications under another name.

**Durability.** Some tasks require days or months of execution, durable state, human approval, and external coordination. Their composition can still be task-scoped, but retirement must not be confused with deleting necessary state.

**Security.** Dynamic composition expands the attack surface through dependency substitution, malicious assets, permission escalation, and unsafe adaptation. Signed provenance, policy enforcement, isolation, and revocation need concrete designs.

**Observability.** Ephemerality must not erase evidence needed for accountability. Retention should be proportional and policy-aware.

**Economic trade-off.** Composition-time discovery and validation may cost more than maintaining a stable workflow. The model needs workload-specific break-even analysis.

**Prior art.** The proposed combination may already be present in related systems under different names. A systematic literature review and implementation comparison are required before making novelty claims.

## 11. Conclusion

Transient Asset Computing proposes a lifecycle-oriented architecture in which durable capability assets are composed into temporary, task-specific executable structures. The composition can adapt during execution, but it remains bounded by task authorization, contracts, provenance, and explicit finalization. At the end of the task, temporary structure is retired and outputs are selectively discarded, retained, archived, quarantined, or promoted.

The proposal's central question is not whether software can be made ephemeral—many systems already do this—but whether the lifecycle of task-specific composition can be treated as a first-class architectural concern while reusable capability assets remain independently governed. The answer is not established here. It requires comparison with existing systems, operational definitions, prototypes, and experiments that include failures and recovery, not only successful execution.

---

## References and reading anchors

The following works provide established context. They are not claimed to validate TAC.

1. Szyperski, C. (2002). *Component Software: Beyond Object-Oriented Programming* (2nd ed.). Addison-Wesley.
2. Parnas, D. L. (1972). On the Criteria To Be Used in Decomposing Systems into Modules. *Communications of the ACM*, 15(12), 1053–1058. https://doi.org/10.1145/361598.361623
3. van der Aalst, W. M. P. (2016). *Process Mining: Data Science in Action* (2nd ed.). Springer. https://doi.org/10.1007/978-3-662-49851-4
4. Armbrust, M., et al. (2010). A View of Cloud Computing. *Communications of the ACM*, 53(4), 50–58. https://doi.org/10.1145/1721654.1721672
5. Jonas, E., et al. (2019). Cloud Programming Simplified: A Berkeley View on Serverless Computing. arXiv:1902.03383. https://arxiv.org/abs/1902.03383
6. Clements, P., & Northrop, L. (2001). *Software Product Lines: Practices and Patterns*. Addison-Wesley.
7. Dragoni, N., et al. (2017). Microservices: Yesterday, Today, and Tomorrow. In *Present and Ulterior Software Engineering*. Springer. https://doi.org/10.1007/978-3-319-67425-4_12
8. Bernstein, P. A., & Newcomer, E. (2009). *Principles of Transaction Processing* (2nd ed.). Morgan Kaufmann.
9. Burns, B. (2018). *Designing Distributed Systems*. O'Reilly Media.
10. Amershi, S., et al. (2019). Software Engineering for Machine Learning: A Case Study. *2019 IEEE/ACM 41st International Conference on Software Engineering: Software Engineering in Practice (ICSE-SEIP)*. https://doi.org/10.1109/ICSE-SEIP.2019.00042

**Bibliographic note:** This is an initial reading list, not a completed systematic review. The references should be checked against the final argument and expanded with direct work on dynamic reconfiguration, ephemeral infrastructure, workflow compensation, capability security, agent runtimes, and software architecture before journal or conference submission.
