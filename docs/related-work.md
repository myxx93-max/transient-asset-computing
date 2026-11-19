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

## Recent literature requiring direct comparison

1. Ashfaq, M., Sadik, A. R., Das, T., Waseem, M., Mäkitalo, N., & Mikkonen, T. (2026). Runtime composition in dynamic system of systems: A systematic review of challenges, solutions, tools, and evaluation methods. *Journal of Systems and Software*, 232, 112661. https://doi.org/10.1016/j.jss.2025.112661  
   This systematic review screened 1,774 studies from 2019–2024 and analyzed 80 primary studies. It directly overlaps with runtime discovery, integration, and coordination. TAC must distinguish its asset/composition lifecycle and selective-promotion framing from the approaches surveyed there.

2. Coullon, H., Henrio, L., Loulergue, F., & Robillard, S. (2024 issue; published online 2023). Component-based Distributed Software Reconfiguration: A Verification-oriented Survey. *ACM Computing Surveys*, 56(1), Article 2. https://doi.org/10.1145/3595376  
   This survey covers runtime component reconfiguration, lifecycle states, dependencies, and verification. It is central prior art for dynamic composition and lifecycle modeling.

3. Yu, M., Cao, T., Wang, W., & Chen, R. (2023). Following the Data, Not the Function: Rethinking Function Orchestration in Serverless Computing. *USENIX NSDI 2023*. https://www.usenix.org/conference/nsdi23/presentation/yu  
   This work argues for data-centric serverless orchestration and an intermediate data abstraction. It is relevant to the distinction between transient execution structure and persistent/intermediate task data.

4. García López, P., Arjona, A., Sampé, J., Slominski, A., & Villard, L. (2021). Triggerflow: Trigger-based orchestration of serverless workflows. *Future Generation Computer Systems*, 124, 215–229. https://doi.org/10.1016/j.future.2021.06.004  
   This work demonstrates trigger-based orchestration of DAGs, state machines, and workflow-as-code, including scale-to-zero and long-running workflow support. TAC should not conflate transient task composition with short-lived function execution.

5. Ge, Y., et al. (2026). Software Engineering for LLM-Based Agents: A Lifecycle-Oriented Survey. arXiv:2611.23260. https://arxiv.org/abs/2611.23260  
   This survey studies agent requirements, architecture, implementation, testing, assurance, maintenance, and evolution. It is relevant to the lifecycle framing but does not, by itself, establish TAC's asset/composition distinction.

## Cautious novelty statement

The proposal should not be described as the first system to dynamically assemble software, execute ephemeral workloads, or reuse capabilities. Those ideas have substantial prior art. The candidate contribution is the explicit combination of:

1. a durable, governed capability-asset layer;
2. a task-scoped executable composition assembled from those assets;
3. controlled runtime adaptation under a task authorization boundary;
4. explicit finalization and retirement of task-specific structure; and
5. selective promotion of validated outputs into longer-lived assets.

Whether this combination is sufficiently distinct or useful remains an open research question. A systematic review should search for equivalent combinations, including terminology not using the phrase "transient asset computing."
