# CUDA-NN Project Charter

**Status:** Accepted architecture; production implementation not authorized

## Purpose

Provide a reusable, application-neutral neural-network semantic layer over public CUDA-JS-Tensor and CUDA-JS contracts without turning lower layers into an NN framework and without absorbing concrete product/model meaning. Optional reusable RNG and communication semantics are consumed from their independent semantic owners when an accepted NN profile needs them.

CUDA-NN exists because reusable NN semantics have an independent conceptual and release lifecycle from the generic CUDA runtime. Repository existence does not prove that every current consumer needs the layer; production implementation remains subject to the inference justification gate in issue #2.

## Product boundary

### CUDA-NN owns, when selected by accepted contracts

- reusable NN model/module/layer graph semantics;
- parameter and NN-state roles above generic Tensor values;
- provider-neutral inference graph normalization/composition;
- NN-specific lowering and provider-selection semantics;
- NN execution-plan semantics above generic Tensor/CUDA execution;
- autodiff, gradients, losses, optimizers, checkpoints and training lifecycle when explicitly selected;
- NN-specific stochastic policy and association of accepted RNG streams/state with initializers, dropout, sampling or training steps;
- NN-specific distributed-training semantics such as gradient aggregation/update ordering, global-batch equivalence, checkpoint/world-state meaning and training failure policy;
- NN-specific numerical, lifecycle, compatibility and conformance evidence.

### CUDA-NN does not own

#### CUDA-JS ownership

- CUDA Driver/runtime/compiler/linker/artifact mechanisms;
- Device-JS language and generic scalar/device helpers;
- threads/blocks/warps, launch validation and physical execution primitives;
- atomics, barriers, memory scopes, publication primitives;
- memory allocation, typed device views, streams/events/operations/prepared-DAG mechanics;
- generic CUDA-library/native-provider handles, plans, workspace/resource leasing, native errors and teardown.

#### CUDA-JS-Tensor ownership

- generic tensor dtype/shape/layout/stride/view/alias semantics;
- broadcasting, reductions, matmul, gather, concat, convolution, FFT, sparse, solver/factorization and other mathematical Tensor operations when useful independent of NN meaning;
- generic TensorProgram/TensorPlan semantics, tensor material/liveness/workspace planning and tensor execution equivalence.

#### CUDA-RNG ownership

- reusable generator/profile, seed/sequence/offset, split/fork, distribution/sampling and reproducibility semantics independent of NN meaning.

CUDA-NN retains only the NN-specific policy/identity linking accepted RNG state/streams to NN parameters, layers, examples or training steps.

#### CUDA-COMM ownership

- reusable group/team/rank membership, collective/P2P/PGAS/RMA communication semantics, ordering/completion/failure composition and provider-neutral communication equivalence.

CUDA-NN retains only the NN-specific meaning of communication for distributed training/inference state.

#### CUDA-MCGS ownership

- Search IR, graph/search policy, evaluator batching/publication, resource/progress/session/stage/channel/search-lifecycle meaning.

#### Downstream product ownership

- concrete model architecture/package provenance unless explicitly represented through a reusable accepted NN contract;
- feature encoding, policy/action mapping, output-head interpretation, chess/UCI or other domain semantics;
- product-specific quality/tolerance/deployment/service behavior.

## Dependency direction

CUDA-NN consumes only versioned public contracts from lower/sibling semantic owners.

```text
product/model consumer
        ↓ optional
     CUDA-NN
        ↓
CUDA-JS-Tensor
        ↓
     CUDA-JS

CUDA-NN -> cuda-rng   optional stochastic profiles
CUDA-NN -> cuda-comm  optional distributed profiles
```

A direct product → CUDA-JS-Tensor path remains valid. CUDA-NN must earn its place through reusable semantics; it is not a mandatory wrapper merely because it exists.

CUDA-NN may consume a public CUDA-JS contract directly only when the required generic mechanism is not naturally Tensor/RNG/COMM-owned. It must never deep-import another repository or duplicate another owner's lifecycle to avoid a missing public primitive.

## First-consumer deletion rule

A capability belongs in CUDA-NN only when deleting the motivating product leaves a coherent reusable NN concept. If its description fundamentally requires the product's model head, feature encoding, chess/search/domain policy or deployment meaning, it remains downstream.

Deleting CUDA-NN must leave CUDA-JS, CUDA-JS-Tensor, CUDA-RNG and CUDA-COMM coherent general-purpose libraries.

## Inference-first gate

Before production NN source or a public NN API is accepted, the project must compare:

1. a product directly constructing CUDA-JS-Tensor programs; and
2. the same product using a reusable CUDA-NN inference layer.

Retain only NN abstractions with demonstrated ownership/reuse/testability value beyond aliases for Tensor operations. A conclusion that direct Tensor composition is currently sufficient is valid.

Inference must not depend on autodiff, optimizer state, training RNG policy, training checkpoints or distributed-training machinery.

## Training rule

Training is an independently removable later capability. If reprioritized, begin with the smallest deterministic FP32 vertical sufficient to prove forward/backward/state/update/checkpoint ownership. Reusable randomness or communication, when needed, must consume accepted `cuda-rng`/`cuda-comm` semantics rather than recreating them. Do not require mixed precision, provider breadth, fusion or distributed scale-out before the baseline is trustworthy.

## Lower-layer/sibling escalation rule

A requirement that would otherwise invite direct CUDA/native code, private imports, duplicated compiler/load/launch/provider/resource lifecycle or distortion of NN semantics is an ownership signal.

- generic CUDA mechanism → assess in CUDA-JS;
- generic Tensor mathematics/planning → assess in CUDA-JS-Tensor;
- reusable RNG/distribution/reproducibility semantics → assess in cuda-rng;
- reusable collective/P2P/PGAS/RMA communication semantics → assess in cuda-comm;
- NN semantics/policy → remain here;
- product/search meaning → remain with its natural owner.

No workaround is implementation authority.

## Source and language rule

CUDA-NN maintained production source is JavaScript/ESM plus restricted Device-JS submitted through accepted public CUDA-JS contracts when required. Python is prohibited throughout repository source, tests, tools, CI, generators and experiments. CUDA-NN does not maintain C/C++, CUDA C++, native addons, hand PTX, direct FFI/Driver access or subprocess-native NN implementations.

## Resource and lifecycle rule

Every accepted mutable/resource-backed NN capability is finite and declares ownership, borrowing, identity, bounds, failure, cancellation and terminal disposition. JavaScript garbage collection is not authoritative release for scarce/native-backed resources. CUDA-JS remains owner of native/provider resource truth; semantic dependencies remain owners of their reusable state machines; CUDA-NN maps those facts without fabricating semantic success.

## First milestone

Maintain repository governance and ownership, then resolve the consumer-backed inference gate. Only after that may the smallest justified NN contracts be specified and independently qualified. Repository creation, roadmap issues and historical CUDA-JS NN specifications do not themselves authorize production implementation.
