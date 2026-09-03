# ADR-0001: Independent CUDA-NN Semantic Owner

**Status:** Accepted

**Date:** 2026-09-02

## Context

CUDA-JS historically accepted ADR-0004 and SPEC-0027 to keep a future application-neutral NN training product as a separate publish unit inside the CUDA-JS repository. That was a reasonable isolation step before the ecosystem had an independent Tensor repository and before NN ownership was compared directly with CUDA-MCGS's already-separated semantic framework.

The current architecture now has clearer lifecycle and semantic layers:

- `iteathen/CUDA-JS` is the generic CUDA runtime/compiler/Device-JS/memory/execution/provider foundation;
- `iteathen/CUDA-JS-Tensor` is the generic tensor mathematics/planning/execution layer;
- `iteathen/CUDA-MCGS` is an independent search-semantic framework over generic CUDA mechanisms;
- downstream products such as UCI-Arena-Vector own concrete model/domain meaning.

Keeping a future NN product physically inside CUDA-JS would place a higher semantic layer with its grandparent dependency while the immediate Tensor abstraction lives elsewhere. It would also leave CUDA-JS carrying model/training governance and issue traffic that does not belong to the runtime's lifecycle.

Project-owner direction therefore created `iteathen/cuda-nn` and selected it as the independent NN semantic owner.

## Decision

CUDA-NN is an independent repository and semantic product, not a CUDA-JS subpackage or workspace.

### Dependency and ownership direction

```text
CUDA-NN
   ↓ public contracts
CUDA-JS-Tensor
   ↓ public contracts
CUDA-JS
```

CUDA-NN may consume a public CUDA-JS contract directly when a required mechanism is genuinely generic CUDA/runtime behavior rather than Tensor mathematics. No dependency may use a sibling repository's private/deep source path.

CUDA-MCGS remains a sibling semantic framework rather than an NN dependency. A product may compose CUDA-MCGS, CUDA-NN and/or CUDA-JS-Tensor as its own architecture requires.

### CUDA-NN semantic boundary

CUDA-NN may own reusable NN concepts such as model/layer graph semantics, parameter roles, provider-neutral inference composition, NN-specific lowering/provider selection and—when separately selected—autodiff, gradients, losses, optimizers, training RNG, checkpoints and training lifecycle.

It does not own generic CUDA mechanisms, generic Tensor mathematics, search semantics or concrete product/model-head/domain meaning.

### First-consumer inference gate

Creating an independent repository establishes where reusable NN semantics belong **if they are needed**. It does not prove that a reusable NN layer is currently necessary.

Before production CUDA-NN source or a public NN API is authorized, issue #2 must compare a concrete consumer using direct CUDA-JS-Tensor composition with the same problem expressed through a reusable CUDA-NN layer. Retain only abstractions that add independent NN semantic ownership/reuse/testability rather than renaming Tensor operations.

A conclusion that direct Tensor composition is currently sufficient is valid and leaves CUDA-NN implementation deferred.

### Training independence

Inference does not require autodiff, optimizer state, training RNG, training checkpoints or distributed training. Training remains a separately removable capability and, if later reprioritized, begins from a small deterministic FP32 baseline rather than inheriting the historical training-first roadmap automatically.

### Historical CUDA-JS NN authority

CUDA-JS ADR-0004 and SPEC-0027 remain immutable historical accepted records in their repository. Their **same-repository product-placement decision is superseded** by this independent repository decision and the corresponding CUDA-JS successor governance change.

Their reusable isolation rationale remains informative where it agrees with current owners, but their old component allocation is not imported as CUDA-NN authority. In particular:

- generic Tensor semantics previously described as local `nn.tensor` responsibility now belong to CUDA-JS-Tensor;
- generic cuBLASLt/cuDNN/NCCL runtime/provider mechanisms remain CUDA-JS-owned when selected;
- provider-specific NN mapping remains CUDA-NN-owned;
- the historical training-first ordering is replaced by the consumer-backed inference gate;
- concrete product/model/search meaning remains outside CUDA-NN.

## Lower-layer capability escalation

If an NN design naturally requires a consumer-neutral CUDA or Tensor mechanism not available through accepted public contracts, CUDA-NN stops at that boundary and routes the gap to the natural owner before implementing a local workaround.

A lower-layer proposal must remain coherent if CUDA-NN is deleted. Conversely, a CUDA-NN semantic contract must remain coherent if the first product consumer is deleted.

## Source rule

CUDA-NN production is JavaScript/ESM plus restricted Device-JS only through accepted public CUDA-JS contracts when needed. CUDA-NN does not maintain C/C++, CUDA C++, `.cu`/`.cuh`, hand PTX, native addons, direct FFI/Driver calls or subprocess-native NN implementations. Python is prohibited across the repository/tooling/CI surface.

## Consequences

- CUDA-JS can remove NN product/package/component ownership from its active charter and registries while preserving historical ADR/spec provenance.
- CUDA-JS-Tensor remains the generic mathematical middle layer rather than being duplicated inside CUDA-NN.
- CUDA-NN has an independent release/compatibility lifecycle if implementation becomes justified.
- Product consumers are not forced through CUDA-NN.
- Training breadth cannot become a prerequisite for inference merely because it existed in the old roadmap.
- Missing lower-layer mechanisms become explicit cross-repository dependencies instead of local escape paths.

## Alternatives considered

### Keep a separate NN publish unit inside CUDA-JS

Rejected for current architecture. The independent Tensor repository and NN semantic lifecycle now make the physical placement misleading and leave unrelated runtime governance coupled to a higher semantic product.

### Rename CUDA-NN as `cuda-js-nn`

Rejected. Repository names primarily identify the semantic capability they own rather than encoding the entire dependency chain. This is consistent with independent `cuda-mcgs` ownership.

### Put NN semantics into CUDA-JS-Tensor

Rejected. Tensor mathematics is useful outside neural networks. Model/layer/autodiff/training meaning would contaminate the generic mathematical owner.

### Implement nothing and leave NN issues in CUDA-JS

Rejected as an ownership state. Implementation may remain deferred, but reusable NN semantics require a natural tracker/authority owner so runtime and Tensor repositories are not polluted by a second product roadmap.

## Validation

A conforming split must prove:

- CUDA-NN root authority and charter encode the dependency/ownership direction;
- CUDA-JS active governance no longer claims a future same-repository NN product;
- CUDA-JS historical ADR/spec records remain traceable as superseded placement authority;
- CUDA-JS-Tensor remains the owner of generic Tensor semantics;
- old CUDA-JS NN issues are reconciled to CUDA-NN or the correct lower-layer owners;
- no production CUDA-NN API/source is implied until the inference gate and later accepted specifications exist;
- repository setting/protection deficits are reported truthfully rather than treated as accepted parity.

## Revisit criteria

Revisit only if the semantic/lifecycle boundary itself proves wrong—for example, reusable NN semantics cannot be separated naturally from Tensor mathematics or a future language-independent NN framework requires a different repository mission. Dependency inconvenience alone is not sufficient.
