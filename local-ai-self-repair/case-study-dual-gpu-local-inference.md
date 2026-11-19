# Case Study: What Actually Improves Local LLM Coding Workloads on a Dual-GPU Workstation?

**An anonymized engineering retrospective — based on bounded local measurements, October 2026**

## Abstract

This case study summarizes local large-language-model inference investigations on a dual-socket workstation with two modified 22-GiB-class RTX 2080 Ti GPUs. The goal was not to maximize a synthetic benchmark score, but to identify which hardware and runtime changes affected a local Coding Agent workload.

The narrow, repeatable finding: increasing llama.cpp micro-batch size from 512 to 1024 produced a **7.1–16.1% prefill-throughput improvement** across tested prompt lengths, while 118K-context decode throughput remained unchanged. This did not establish an end-to-end Coding Agent speedup. Other attractive hypotheses—including deeper CUDA launch queues, batch-only changes, an unvalidated prefill fork, NVLink, and Tensor Core unlocking—were rejected or left unproven after compatibility and critical-path analysis.

This is a bounded engineering report, not a general performance claim or proof of autonomous self-repair.

## 1. System context

The tested platform was a dual-socket workstation with two Xeon E5-2680 v4 processors, 128 GiB system memory, and two RTX 2080 Ti GPUs reporting 22,528 MiB each. Both GPUs use Turing / SM75. The Linux runtime used a CUDA-enabled llama.cpp build and a 128K context configuration.

The GPUs were attached to different CPU root complexes. The measured topology was cross-socket (SYS), and CUDA peer access was unavailable in both directions. GPU-to-GPU copy operations did not imply direct peer-memory access; host staging and overlap had to be considered.

Specific host addresses, usernames, internal paths, model fingerprints, and service identifiers are omitted.

## 2. The measurement question

The investigation separated four questions:

1. **Kernel-level:** Did a specific kernel or microbenchmark become faster?
2. **Inference-level:** Did prefill, decode, or time-to-first-token improve?
3. **Agent-level:** Did a real Coding Agent complete tasks faster or more reliably?
4. **Operational:** Did the change preserve stability, memory headroom, recovery, and the known-good runtime?

A gain at one layer was not promoted as a gain at another without direct evidence.

## 3. Verified micro-batch result

The baseline used batch 2048 / micro-batch 512. A controlled change to batch 2048 / micro-batch 1024 produced the only repeatable positive result in this bounded V1 comparison.

| Workload | Baseline prefill | Micro-batch 1024 | Change |
|---|---:|---:|---:|
| 4K prompt | 2,989 tok/s | 3,200 tok/s | +7.1% |
| 16K prompt | 3,215 tok/s | 3,733 tok/s | +16.1% |
| 64K prompt | 2,443 tok/s | 2,775 tok/s | +13.6% |
| 118K prompt | 1,904 tok/s | 2,106 tok/s | +10.6% |
| 118K decode | 62.3 tok/s | 62.3 tok/s | 0.0% |

Baseline and micro-batch comparisons used three repetitions; reported variation was below 0.5% for the measured prefill cases. Peak VRAM with micro-batch 1024 was approximately 16.8 GiB on the observed peak device, with no CUDA errors, OOMs, or assertions in those runs.

**Interpretation:** the change improved tested prefill throughput. It did not improve the measured long-context decode rate. The report therefore retained 2048/512 as the stable default and treated 2048/1024 as a candidate requiring further OpenCode A/B and long-run memory validation—not an automatic production replacement.

## 4. Negative results and rejected assumptions

### Deeper CUDA launch queues

A 4× launch-queue setting changed prefill by approximately -0.5% to +0.1% and decode by approximately 0.0%, within observed run-to-run noise. It was not a useful lever for this topology and workload.

### Batch-only change

Changing batch size to 4096 while keeping micro-batch at 512 was neutral in the screening measurements. It was pruned rather than promoted.

### Prompt-cache behavior

Exact-prefix reuse and append-only tool-result reuse worked well in the tested configuration. A divergent prefix caused full recomputation in the diagnostic case, and the generic cache-reuse option was disabled by the hybrid/recurrent model context. This was recorded as a runtime/model-specific limitation, not generalized to all models or sessions.

A later separate real-session audit recorded 94.27% prompt-token reuse across 11 sessions and 162 requests, with 151/151 warm requests append-only and zero divergent/full-reprocess events. That later evidence changed the practical priority: a separate paged-KV/cache-service project was stopped for this workload. These measurements describe different test scopes and should not be collapsed into one universal cache claim.

### Tensor Core microbenchmark versus task performance

Earlier work showed large local GEMM microbenchmark gains, but much smaller end-to-end inference gains. In one historical comparison, selected GEMM microbenchmarks improved by roughly 45.7–78.2%, while measured request-level changes were far smaller and varied by workload; one short request was slightly slower.

This illustrates why a kernel percentage cannot be presented as a whole-model or Coding Agent improvement. The accelerated path may cover only part of the actual critical path.

### NVLink and Tensor unlocking

The hardware/runtime audit found no verified direct peer access, inactive NVLink links, uncertain physical bridge compatibility, and substantial recovery/identity blockers for firmware-level experiments. The measured copy activity occupied only a small share of request wall time in the examined traces. The decision was **do not buy an NVLink bridge now** and **no-go for Tensor unlocking** under the available evidence and recovery conditions.

These are workload- and platform-specific decisions, not universal claims that NVLink or Tensor Core work is never useful.

### Newer upstream runtime and prefill fork

A newer upstream build was not produced because the available checkout was shallow and upstream access was unavailable during the experiment. A TurboPrefill fork was reviewed but not built: compatibility with the tested hybrid/MoE model, Q6_K_P quantization, SM75, 128K context, and no-peer-access topology was not established.

The absence of reproducible source and compatibility proof was treated as a blocker, not filled with an assumed version or speculative patch.

## 5. Why the end-to-end result remained unknown

A minimal isolated OpenCode baseline task passed 3/3 acceptance runs, with a median wall time of 16.47 seconds. However, the micro-batch A/B was not run as a matched end-to-end Coding Agent experiment.

Therefore:

- PREFILL_GAIN = VERIFIED for the tested prompt sizes.
- DECODE_GAIN = NOT_OBSERVED at 118K.
- CODING_AGENT_WALL_GAIN = NOT_MEASURED.
- TASK_QUALITY_GAIN = NOT_ESTABLISHED.

A faster prefill may or may not change total agent task time, depending on prompt reuse, decode, tool latency, retries, and task interaction patterns.

## 6. Engineering method that transferred

The reusable contribution is less a particular tuning value than a method:

1. Establish a known-good baseline with model, binary, driver, context, and configuration identities.
2. Measure prefill and decode separately.
3. Inspect topology and peer-access capability instead of inferring it from GPU count.
4. Use Nsight and runtime stage timing, but distinguish cumulative kernel time from wall-clock critical path.
5. Change one variable at a time and repeat measurements.
6. Treat microbenchmarks as mechanism evidence, not workload outcomes.
7. Record negative results and stop low-value branches.
8. Preserve a rollback path and do not replace a stable runtime on an unverified candidate.
9. Promote a tuning candidate only after matched agent-level and long-run validation.

## 7. Relevance to self-repairing local AI systems

This case study does **not** demonstrate an autonomous system repairing itself. The experiments were human-directed and bounded.

It does expose a prerequisite for safe self-repair: a system must distinguish failure layers and produce evidence that can support or reject a repair hypothesis. A slow task might be caused by prefill, decode, cache reuse, GPU topology, tool-call patterns, external dependency latency, or task-definition errors. A self-repairing system that responds to all of these by editing model weights would be unsafe and frequently wrong.

Layer-aware diagnosis, independent evaluation, immutable baselines, and rollback are therefore important research questions.

## 8. Open questions for the community

1. What is the best way to attribute local Coding Agent wall time across prefill, decode, tool calls, and orchestration?
2. Which runtime metrics are reliable enough for automated fault localization?
3. How should a tuning agent distinguish a repeatable mechanism from run-to-run noise?
4. What independent holdout tasks are needed before promoting a runtime or model change?
5. Can a local agent safely manage experiments and rollback without being allowed to modify its own evaluation criteria?
6. Which findings transfer across model architectures, quantization formats, GPU generations, and topologies—and which are strictly local?

Counterexamples and failed optimization attempts are especially welcome.

## 9. Evidence boundaries

This report is a public, anonymized synthesis of local engineering records. It omits private host identifiers, access details, internal filesystem paths, credentials, model hashes, and proprietary implementation specifics.

The numerical results apply only to the measured configuration and test protocol. They are not a benchmark ranking, commercial claim, or promise of performance on other hardware.

The self-repair connection is a research motivation only. No autonomous repair capability is claimed.

## Related materials

- [Self-Repairing Local AI Systems — research track](README.md)
- [Falsifiable research agenda](research-agenda.md)
- [Related-work map](related-work-map.md)
- [Open research discussion](https://github.com/myxx93-max/transient-asset-computing/issues/2)
