# Related-Work Map: Local AI Self-Repair

This is an initial search map, not a completed literature review.

| Research area | Why it matters | Distinction to investigate |
|---|---|---|
| Self-adaptive and autonomic computing | Monitor-analyze-plan-execute loops and feedback control | Whether AI-specific repair needs stronger independent evaluation and artifact provenance |
| Self-healing software | Fault detection, diagnosis, recovery, rollback | Whether repair can span model, runtime, and agent workflow layers |
| Automated program repair | Generate and validate code changes | Whether the repair target includes model/runtime configuration and agent behavior |
| LLM-based agents | Tool use, planning, reflection, and iterative execution | Whether self-critique is sufficiently independent to authorize promotion |
| ML systems operations (MLOps) | Model deployment, monitoring, rollback, drift | Whether the system can diagnose and repair its own execution stack |
| Model editing and weight-space methods | Change model behavior through parameter updates or localized edits | Whether edits are reversible, bounded, and validated on held-out task families |
| Inference optimization | Quantization, batching, memory placement, kernels, serving | Whether runtime optimization is incorrectly attributed to model improvement |
| Software testing and evaluation | Regression suites, holdouts, reproducibility | How to prevent evaluator leakage and reward hacking |

## Cautious positioning

Self-healing systems, autonomic computing, automated program repair, and agent reflection all predate this research direction. The proposed question is not whether an AI system can retry or critique itself. It is whether a local AI execution system can perform **layer-aware diagnosis and bounded repair under independent evaluation, immutable baselines, provenance, and reliable rollback**.

The distinctiveness and usefulness of this combination remain to be established through a systematic review and controlled experiments.
