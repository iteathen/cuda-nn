# Evidence status

This repository follows the shared [iteathen evidence and validation policy](https://github.com/iteathen/.github/blob/main/EVIDENCE_POLICY.md).

## Current posture

CUDA-NN is currently an architecture/planning repository. Its intended scope is documented, but there is no production neural-network implementation, public API, installable package, native-provider qualification, training qualification, or performance claim.

## Registered claims

| Claim | Evidence class | Status |
| --- | --- | --- |
| `CUDA-NN-PLAN-001` — intended scope: reusable neural-network model/layer representation and inference composition above CUDA-JS-Tensor | **UNVALIDATED** | planning hypothesis / project boundary |

The claim record is machine-readable in [`evidence/claims.json`](evidence/claims.json).

## What current evidence establishes

The repository establishes the current project boundary, planning state, architecture decisions, and the requirement that reusable NN behavior be justified beyond direct Tensor composition.

## What it does not establish

It does not establish a production NN layer, API usefulness, training support, native GPU behavior, performance, or external reproduction.

## Path to stronger evidence

If implementation is justified and authorized, claims should advance through deterministic internal qualification first, then consumer/reference tests and hardware-measured evidence where applicable.

## Non-mutation rule

Evidence work may inspect, test, benchmark, and document CUDA-NN. It must not change substantive operational behavior merely to make an evidence claim pass.
