# CUDA-NN Status

**Updated:** 2026-09-06

## Current state

CUDA-NN has an accepted **semantic ownership boundary**, but no production CUDA-NN inference/training implementation is currently selected.

The first concrete consumer gate is complete: UCI-Arena-Vector's frozen LatticeKnight-4M model reached complete public CUDA-JS-Tensor operation/spec/resource/callable-workspace coverage through direct product -> Tensor composition without demonstrating a reusable NN semantic layer that survives the ownership/deletion tests. Issue #2 therefore concluded that direct Tensor composition is sufficient for the demonstrated first consumer and production CUDA-NN remains deferred.

There is no production NN source, package, public API, native/provider implementation, training implementation, qualification program or performance claim. The dependent inference/training/provider/optimization issues are closed `not_planned` as dormant retained research and may be reopened only from new consumer evidence.

## Ownership

- CUDA-JS owns all maintained native CUDA/runtime/compiler/Device-JS/memory/execution/provider/resource mechanisms under protected SPEC-0032.
- CUDA-JS-Tensor owns generic Tensor dtype/shape/layout/math/planning/execution/item ABI/workspace semantics.
- `cuda-rng` owns reusable generator/distribution/seed/split/reproducibility semantics when independently activated.
- `cuda-comm` owns reusable group/team/rank, collective/P2P/PGAS/RMA communication semantics when independently activated.
- CUDA-NN is the reserved owner for reusable model/layer/inference/autodiff/training semantics **only if a future consumer independently demonstrates that such a layer adds meaning beyond direct Tensor composition**.
- CUDA-MCGS owns search/evaluator/search-lifecycle semantics.
- downstream products retain concrete model/checkpoint/feature/head/domain/product meaning.

Accepted CUDA-NN SPEC-0001 fixes the repository implementation boundary: maintained source is JavaScript/TypeScript plus restricted Device-JS through public CUDA-JS only. No upper-local C/C++/CUDA/PTX/native FFI/provider binding is permitted.

## Repository governance state

Repository controls are aligned with the CUDA-family baseline. `main` is protected; the selected merge/signoff/update-branch/merged-head-cleanup/wiki/discussions settings were read back and issue #17 is closed completed. No local CI workflow currently exists, so no required status-check name is fabricated.

## Current authority

Root `AGENTS.md`, `docs/PROJECT_CHARTER.md`, accepted SPEC-0001 and the accepted ADRs define the durable ownership/dependency model. Closed roadmap/feature issues are retained provenance and design research, not implementation authority.

Historical CUDA-JS ADR-0004/SPEC-0027 remain provenance only for the superseded same-repository NN placement.

## Reactivation rule

There is **no active CUDA-NN production work**.

Reopen the inference justification gate or create a bounded successor only when a materially different consumer, or repeated semantics across multiple consumers, demonstrates reusable NN concepts that:

1. are not generic Tensor mathematics/planning;
2. are not native CUDA/provider mechanisms;
3. are not product-specific model/checkpoint/head meaning;
4. survive first-consumer deletion;
5. improve ownership/reuse/testability enough to justify another semantic layer.

Provider availability, training aspirations, or shorter application code are not sufficient activation evidence by themselves.

If reactivated, accept the smallest semantic specification first. Training/autodiff/provider/distributed lanes remain independent and dormant until their own consumer evidence exists.

## Explicit non-claims

- no reusable NN inference layer is currently selected;
- no accepted CUDA-NN production capability specification exists beyond the architecture/ownership boundary;
- no Tensor/RNG/communication semantic primitive has moved into CUDA-NN;
- no native CUDA/provider primitive has moved out of CUDA-JS;
- no product is required to adopt CUDA-NN;
- no training/autodiff/provider/distributed capability is implementation-ready;
- no native CUDA/provider/platform or performance support is claimed.
