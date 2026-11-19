# Related Work: Positioning and Boundaries

This note is a conceptual map, not a systematic literature review. It identifies adjacent paradigms and the comparison that a rigorous review should investigate.

| Area | Established concern | TAC's proposed emphasis | Key question for review |
|---|---|---|---|
| Component-based software engineering | Reuse and composition of components | Distinct lifecycle for durable assets and task-bounded compositions | How much of TAC is already covered by dynamic component systems? |
| Dynamic reconfiguration | Change component structure at runtime | Task identity, explicit finalization, and selective promotion | Are lifecycle and promotion already first-class in reconfiguration systems? |
| Microservices/SOA | Independently deployed services and service composition | Assets need not be services; task composition need not become a permanent service | Does service composition already provide equivalent lifecycle boundaries? |
| Serverless/FaaS | Invocation-oriented execution and infrastructure abstraction | Composition lifecycle and asset governance, not just compute lifetime | Can serverless orchestration implement TAC without additional concepts? |
| Workflow engines | Durable orchestration, retries, compensation, state | Treat task-specific workflow graph as a transient object with governed retirement | How do workflow definitions and instances map to TAC assets/compositions? |
| Software product lines | Reuse and variability across a product family | Runtime task-specific composition under changing evidence and constraints | Is this merely a runtime product configuration problem? |
| Containers and sandboxes | Isolation and disposable execution environments | Lifecycle of composition and its knowledge, not only the environment | What does environment destruction leave behind in external systems? |
| Agent runtimes | Planning, tool selection, and multi-step task execution | Governance around asset selection, adaptation, provenance, and retirement | Which agent frameworks already implement equivalent controls? |
| Transaction processing | Atomicity, recovery, compensation, durable state | Explicit terminal handling for task compositions | How should long-running tasks reconcile retirement with durable recovery? |

## Cautious novelty statement

The proposal should not be described as the first system to dynamically assemble software, execute ephemeral workloads, or reuse capabilities. Those ideas have substantial prior art. The candidate contribution is the explicit combination of:

1. a durable, governed capability-asset layer;
2. a task-scoped executable composition assembled from those assets;
3. controlled runtime adaptation under a task authorization boundary;
4. explicit finalization and retirement of task-specific structure; and
5. selective promotion of validated outputs into longer-lived assets.

Whether this combination is sufficiently distinct or useful remains an open research question. A systematic review should search for equivalent combinations, including terminology not using the phrase "transient asset computing."
