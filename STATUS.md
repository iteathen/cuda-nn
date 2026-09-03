# CUDA-NN Status

**Updated:** 2026-09-02

## Current state

CUDA-NN has an **integrated architecture/governance owner** at `main@7d7854697049db38e4a0670b80df9d600cd442c3`. There is no production NN source, package, public API, provider implementation, native qualification, training implementation or performance claim.

CUDA-JS completed the matching repository-placement reconciliation through PR #167 / issue #165 at protected `main@9501b1790ddbe94d0254d89dc33ee6d19f2587f9`. Historical CUDA-JS ADR-0004/SPEC-0027 remain provenance only for their superseded same-repository placement.

Issue #2 remains the required consumer-backed inference-layer justification gate before production NN implementation.

## Ownership

- CUDA-JS owns generic CUDA runtime/compiler/Device-JS/memory/execution/native-provider/resource mechanisms.
- CUDA-JS-Tensor owns generic Tensor dtype/shape/layout/math/planning/execution.
- `cuda-rng` owns reusable generator/distribution/seed/split/reproducibility semantics.
- `cuda-comm` owns reusable group/team/rank, collective/P2P/PGAS/RMA communication semantics.
- CUDA-NN may own reusable model/layer/inference/autodiff/training meaning only through accepted CUDA-NN contracts, including the NN-specific policy that consumes RNG/communication semantics.
- CUDA-MCGS owns search semantics.
- downstream products retain concrete model/domain meaning.

## Repository governance state

The repository settings remain **not yet aligned** with the established CUDA repositories. Current live readback still shows merge commits enabled, auto-merge disabled and update-branch disabled, while `main` remains unprotected. Issue #17 owns this control-plane gap. Do not claim parity until settings and protection are changed and read back.

## Current authority

Root `AGENTS.md`, `docs/PROJECT_CHARTER.md`, ADR-0001 and, after issue #19 integration, ADR-0002 define the current ownership/dependency model. Open roadmap issues are not specifications.

## Explicit non-claims

- no reusable NN inference layer has yet been proven necessary;
- no accepted CUDA-NN production specification exists;
- no Tensor/RNG/communication semantic primitive has moved into CUDA-NN;
- no CUDA/provider primitive has moved out of CUDA-JS;
- no product is required to adopt CUDA-NN;
- no training/autodiff/provider/distributed capability is implementation-ready;
- no native CUDA/provider/platform support is claimed.
