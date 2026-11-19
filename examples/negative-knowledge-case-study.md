# Anonymized Negative-Knowledge Case Study: A False Correlation in an Attention-Flow Analysis

**Evidence class:** historical engineering finding, summarized at a non-sensitive level  
**Purpose:** illustrate why failed assumptions should be retained as counterexamples rather than silently discarded.

## Problem

An analysis pipeline identified an apparent relationship between attention-flow signals and downstream outcomes. The initial interpretation risked treating correlated observations as evidence of a causal mechanism.

## Failure mode

The analysis contained a pseudo-correlation weakness: the observed association was not sufficient to establish that the attention-flow signal caused the downstream behavior. Without stronger controls, the system could overstate a mechanism from coincident or confounded signals.

## Corrective principle

Separate:
- directly observed facts;
- associations found in the data;
- causal claims;
- unresolved alternatives.

A signal name, event field, or correlation is not itself proof of an algorithmic mechanism. Mechanism claims require independent evidence, controls, and a defensible causal chain.

## What should be retained?

| Item | Treatment |
|---|---|
| Original observation and its provenance | Retain as evidence, subject to data policy |
| Incorrect causal interpretation | Mark as rejected or superseded; do not erase its history |
| Identified confounder or methodological weakness | Retain as negative knowledge |
| Corrected analysis procedure | Candidate reusable asset after independent validation |
| Sensitive raw data and internal paths | Not included in this public case study |

## Why this matters to transient asset composition

A task-specific analysis granule may be retired after its task ends, but its validated counterexample can remain useful. The system should not preserve every temporary script and intermediate file. It should preserve the compact, traceable lesson that prevents the same invalid inference from being repeated.

This suggests a distinction between:
- **composition retirement** — remove task-specific executable structure;
- **knowledge retention** — preserve selected evidence and validated negative lessons;
- **asset promotion** — make a corrected method reusable only after validation.

## Limitations

This is an anonymized, high-level summary. It does not expose source data, project paths, proprietary implementation details, or a complete experimental record. It is not presented as a peer-reviewed case study or as proof of TAC's effectiveness.
