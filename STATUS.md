# CUDA-NN Status

**Updated:** 2026-09-02

## Current state

CUDA-NN is in **repository/authority bootstrap**. There is no production NN source, package, public API, provider implementation, native qualification, training implementation or performance claim.

The project-owner has selected `iteathen/cuda-nn` as the independent reusable NN semantic owner. Issue #1 owns the migration program and issue #15 owns this bootstrap authority packet. Issue #2 remains the required consumer-backed inference-layer justification gate before production NN implementation.

## Ownership

- CUDA-JS owns generic CUDA runtime/compiler/Device-JS/memory/execution/provider/resource mechanisms.
- CUDA-JS-Tensor owns generic Tensor dtype/shape/layout/math/planning/execution.
- CUDA-NN may own reusable model/layer/inference/autodiff/training semantics only through accepted CUDA-NN contracts.
- CUDA-MCGS owns search semantics.
- downstream products retain concrete model/domain meaning.

## Repository governance state

The repository was newly created and its GitHub settings are **not yet aligned** with the established CUDA repositories. At the bootstrap baseline:

- `main` is unprotected;
- merge commits are enabled;
- auto-merge is disabled;
- automatic merged-head branch deletion is disabled;
- update-branch support is disabled;
- web commit signoff is disabled;
- Wiki is enabled and Discussions are disabled.

The connected GitHub integration used during bootstrap can read these settings but does not expose repository-settings mutation. Do not claim parity until the settings are changed and read back.

This bootstrap therefore uses a focus branch and PR voluntarily, but integration cannot be described as protected-main acceptance until protection/settings are configured.

## Current authority

On the bootstrap branch, root `AGENTS.md`, `docs/PROJECT_CHARTER.md` and `docs/decisions/ADR-0001-independent-nn-semantic-owner.md` establish the intended durable authority. They become repository-integrated authority only after exact-head review/integration/readback.

Historical CUDA-JS ADR-0004/SPEC-0027 remain provenance in CUDA-JS; their same-repository NN placement is being superseded through CUDA-JS issue #165 after this bootstrap owner exists.

## Explicit non-claims

- no reusable NN inference layer has yet been proven necessary;
- no accepted CUDA-NN production specification exists;
- no Tensor operation has moved into CUDA-NN;
- no CUDA/provider primitive has moved out of CUDA-JS;
- no product is required to adopt CUDA-NN;
- no training/autodiff/provider/distributed capability is implementation-ready;
- no native CUDA/provider/platform support is claimed.
