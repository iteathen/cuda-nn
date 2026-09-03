# ADR-0002: Compose Independent RNG and Communication Semantic Owners

**Status:** Accepted

**Date:** 2026-09-02

## Context

ADR-0001 established CUDA-NN before `iteathen/cuda-rng` and `iteathen/cuda-comm` existed as independent semantic owners. The original charter therefore used broad terms such as training RNG and distributed collectives without an intermediate semantic home between NN policy and CUDA-native provider mechanisms.

The ecosystem now has integrated owners for reusable RNG/distribution/reproducibility semantics and provider-neutral communication group/collective/PGAS/RMA semantics. CUDA-NN must consume those concepts without surrendering NN-specific stochastic/distributed-training meaning and without pushing them down into CUDA-JS.

## Decision

CUDA-NN may optionally depend on public `cuda-rng` and `cuda-comm` contracts when an accepted NN profile requires them.

### RNG split

`cuda-rng` owns reusable generator/profile, seed/sequence/offset, split/fork, distribution/sampling and reproducibility semantics.

CUDA-NN owns the NN-specific policy/identity that assigns accepted RNG streams/state to initializers, dropout, sampling, examples, parameters or training steps and interprets stochastic effects in NN state.

CUDA-JS owns native/provider/device/memory/operation resources such as a bounded cuRAND mechanism when selected.

### Communication split

`cuda-comm` owns reusable group/team/rank, collective/P2P/PGAS/RMA communication semantics, ordering/completion/failure composition and provider-neutral equivalence.

CUDA-NN owns NN-specific data-parallel/distributed semantics such as gradient aggregation/update ordering, global-batch equivalence, checkpoint/world-state meaning and training failure policy.

CUDA-JS owns physical devices/contexts/memory/streams/operations and bounded native providers such as NCCL/NVSHMEM when selected.

## Dependency direction

```text
cuda-nn -> cuda-rng   optional
cuda-nn -> cuda-comm  optional
cuda-nn -> cuda-js-tensor -> cuda-js
cuda-rng -> cuda-js
cuda-comm -> cuda-js
```

No dependency points from a lower/general owner back into CUDA-NN.

## Deletion tests

Deleting CUDA-NN leaves CUDA-RNG and CUDA-COMM coherent for materially different consumers. Deleting either optional semantic dependency leaves CUDA-NN's baseline inference architecture coherent; only profiles that explicitly selected that dependency become unavailable.

## Consequences

- CUDA-NN no longer needs a private RNG or collective semantic framework.
- reusable RNG/communication semantics remain independently testable and provider-neutral;
- NN-specific stochastic/distributed policy remains NN-owned;
- CUDA-JS remains native/provider mechanism owner rather than semantic communication/RNG framework;
- inference issue #2 remains the production activation gate and is not widened by this composition decision.

## Non-goals

No RNG/communication implementation, provider selection, training activation, inference authorization, or repository-control change is created by this ADR.
