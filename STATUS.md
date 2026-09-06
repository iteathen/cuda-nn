# CUDA-NN Status

**Updated:** 2026-09-05

## Current state

CUDA-NN has an **integrated architecture/governance owner**. The current governance baseline includes the optional RNG/communication composition reconciliation at `main@ac97fee981b7789e11af2ec4a7ca40799eb08ddd`.

There is still no production NN source, package, public API, provider implementation, native qualification, training implementation or performance claim.

CUDA-JS completed the matching repository-placement reconciliation through its accepted external-NN ownership authority. Historical CUDA-JS ADR-0004/SPEC-0027 remain provenance only for their superseded same-repository placement.

Issue #2 remains the required consumer-backed inference-layer justification gate before production NN implementation. UCI-Arena-Vector is the first concrete model consumer: its protected LatticeKnight mapping is now specific enough to test whether a reusable NN layer adds independent model/layer/inference semantics or merely renames Tensor operations. A valid outcome is that direct product-to-Tensor composition remains sufficient and production CUDA-NN inference stays deferred.

## Ownership

- CUDA-JS owns generic CUDA runtime/compiler/Device-JS/memory/execution/native-provider/resource mechanisms.
- CUDA-JS-Tensor owns generic Tensor dtype/shape/layout/math/planning/execution.
- `cuda-rng` owns reusable generator/distribution/seed/split/reproducibility semantics.
- `cuda-comm` owns reusable group/team/rank, collective/P2P/PGAS/RMA communication semantics.
- CUDA-NN may own reusable model/layer/inference/autodiff/training meaning only through accepted CUDA-NN contracts, including NN-specific policy that consumes RNG/communication semantics without absorbing those reusable semantic owners.
- CUDA-MCGS owns search semantics.
- downstream products retain concrete model/domain meaning.

ADR-0002 now records the optional composition rule: accepted NN profiles may depend on `cuda-rng` and/or `cuda-comm`, but CUDA-NN does not recreate their generator/distribution/reproducibility or communication/group/collective/PGAS/RMA state machines. CUDA-JS still owns the lower native/provider/device/resource mechanics behind any future accelerated realization.

## Repository governance state

The repository settings remain **not yet aligned** with the established protected CUDA repositories. Current live readback still shows `main` unprotected and issue #17 owns the control-plane gap. Do not describe CUDA-NN as protected-main or repository-setting parity until those settings are changed and read back.

## Current authority

Root `AGENTS.md`, `docs/PROJECT_CHARTER.md`, ADR-0001 and integrated ADR-0002 define the current ownership/dependency model. Open roadmap issues are planning/assessment trackers, not implementation specifications.

## Current executable decision gate

Issue #2 should compare, against the concrete Vector model evidence:

1. direct product -> CUDA-JS-Tensor composition; and
2. a minimal reusable CUDA-NN inference layer above Tensor.

Retain only concepts with independent NN meaning that survive first-consumer deletion, improve ownership/reuse/testability, and do not hide product model/head/provenance semantics. Reject abstractions that merely rename generic Tensor operations. Training, autodiff, provider breadth and distributed training are not prerequisites for deciding this inference boundary.

## Explicit non-claims

- no reusable NN inference layer has yet been proven necessary;
- no accepted CUDA-NN production specification exists;
- no Tensor/RNG/communication semantic primitive has moved into CUDA-NN;
- no CUDA/provider primitive has moved out of CUDA-JS;
- no product is required to adopt CUDA-NN;
- no training/autodiff/provider/distributed capability is implementation-ready;
- no native CUDA/provider/platform support is claimed.
