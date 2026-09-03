# CUDA-NN Agent Instructions

This file is mandatory startup authority for every agent working in this repository.

## Authority order

Use this order when sources conflict:

1. explicit current project-owner instruction;
2. this root `AGENTS.md`;
3. accepted ADRs in `docs/decisions/`;
4. accepted normative specifications in `docs/specs/`;
5. `docs/PROJECT_CHARTER.md` and current ownership/status documents;
6. architecture/research documents;
7. plans, issues, PR text, comments, status summaries and handoffs.

Issues, plans, PR descriptions and previous-agent conclusions are tracking/evidence artifacts. They are not specifications and do not authorize implementation by themselves.

## Governing execution method

For every meaningful unit of work use:

**assess → research → reassess → plan → execute → qualify → review → cleanup/document**

Before changing code or contracts, inspect the actual current repository state, governing authority, lower-layer public contracts, relevant tests/evidence and exact dependency state. Falsify assumptions before implementation. Never repair a diagnosis merely because an issue asserts it.

## Design hierarchy

Use **LEGO → SOLID → CUPID → KISS**.

One semantic fact, state machine, lifecycle, resource, compatibility fact or failure meaning has one visible owner. Prefer small independently replaceable bricks and explicit ports over duplicated interpreters, hidden coupling, cross-layer convenience or speculative abstraction.

A capability moves downward only when its semantics are naturally consumer-neutral. First-consumer pressure is evidence to assess ownership, not permission to contaminate a lower layer.

## Repository mission

CUDA-NN is the potential reusable neural-network semantic layer in the CUDA ecosystem. It is **not** the generic CUDA runtime, generic Tensor library, generic RNG library, or generic communication library.

Base dependency direction is:

```text
cuda-nn
  ↓ public contracts only
cuda-js-tensor
  ↓ public contracts only
cuda-js
```

Optional semantic composition, only when an accepted NN profile needs it:

```text
cuda-nn -> cuda-rng   (generator/distribution/reproducibility semantics)
cuda-nn -> cuda-comm  (collective/P2P/PGAS/RMA communication semantics)
```

Those optional dependencies do not reverse direction and do not make CUDA-NN their semantic owner. CUDA-MCGS is a sibling semantic framework. Product repositories such as UCI-Arena-Vector remain owners of concrete model/package/domain meaning.

### CUDA-NN may own, when justified by accepted contracts

- reusable model/layer/NN graph semantics;
- parameter and NN-state roles above generic Tensor values;
- provider-neutral inference composition and NN execution planning;
- autodiff, gradients, losses, optimizers, checkpoints and training lifecycle;
- NN-specific stochastic policy and association of accepted RNG streams/state with initializers, dropout, sampling or training steps;
- NN-specific distributed-training meaning such as gradient aggregation/update ordering, global-batch equivalence and checkpoint/world-state semantics;
- NN-specific provider selection/mapping and conformance.

### CUDA-NN does not own

- CUDA threads/blocks/warps, launch mechanics, atomics/barriers, compiler/linker/artifact mechanics, memory allocation/views, streams/events/operations, native provider handles or generic resource lifecycle — `iteathen/CUDA-JS`;
- generic Tensor dtype/shape/layout/view/broadcast/reduction/matmul/gather/concat/convolution/fusion/FFT/sparse/solver semantics — `iteathen/CUDA-JS-Tensor` when naturally generic;
- reusable generator/distribution/seed/split/reproducibility semantics — `iteathen/cuda-rng`;
- reusable group/team/rank, collective/P2P/PGAS/RMA communication semantics — `iteathen/cuda-comm`;
- graph-search/evaluator/progress/search-session semantics — `iteathen/CUDA-MCGS`;
- concrete model architecture/package provenance, feature encoding, policy/action mapping, output-head meaning, chess/UCI or product tolerances — downstream product owners.

If implementation pressure suggests C/C++, CUDA C++, hand PTX, direct FFI/Driver access, a private/deep lower-layer import, duplicated launch/provider/resource lifecycle, or an awkward workaround around a public lower-layer gap, **stop at that boundary and classify ownership first**. Route genuine generic gaps to the natural lower or sibling semantic owner.

## Current implementation gate

Repository creation does not prove a reusable NN abstraction is needed.

Before production NN source or public NN API is authorized, issue #2 must establish a consumer-backed reason to insert CUDA-NN above direct product → CUDA-JS-Tensor composition. Direct Tensor composition remains a valid outcome.

Training/autodiff is not an inference prerequisite. Training work stays independently removable and deferred until explicitly reprioritized behind accepted authority.

## Language and native-source rule

Python is prohibited in this ecosystem repository, including production source, tests, tools, CI, generators, experiments and one-off scripts.

Maintained CUDA-NN production source must not contain C, C++, CUDA C++, `.cu`/`.cuh`, hand-authored PTX, native addons, direct FFI/Driver access or subprocess-native NN implementations. CUDA-specific realization belongs behind versioned public CUDA-JS contracts. Restricted Device-JS may be used only through accepted public lower-layer contracts.

## Contract and compatibility rules

- Do not deep-import sibling repositories or their private paths.
- Do not copy lower-layer schema/limit/provider facts into CUDA-NN as new authority.
- Do not recreate RNG or communication semantic state machines that belong to `cuda-rng` or `cuda-comm`.
- Public compatibility records must identify exact consumed lower-layer/semantic contract revisions when material.
- Preserve exact ownership of failure, cancellation, pressure, cleanup and unproved-resource state; never fabricate successful cleanup or intact mutable training state.
- Finite resources, bounds and lifecycle are mandatory for every accepted mutable/native-backed capability.
- Provider availability never authorizes provider-specific semantics in a generic contract.

## Implementation authorization

No production component enters the repository until its semantic owner, dependencies, finite lifecycle, errors, compatibility, deletion behavior and decisive falsifiers are accepted in repository authority. Open roadmap issues are planning/assessment trackers, not implementation specifications.

## Validation and review

Qualification must match the claim:

- portable/reference evidence cannot be relabeled as CUDA/native/provider evidence;
- mocks prove orchestration, not GPU correctness or performance;
- numerical, lifecycle, compatibility and performance claims remain separate;
- cross-repository claims pin exact compatible revisions;
- performance optimization follows a trustworthy correctness baseline.

Review exact changed content against the governing owner boundary before integration. Protected-branch or expected-head governance must be followed wherever configured. Current repository protection/settings deficits must be reported truthfully rather than ignored.

## Cleanup

After work, reconcile branches/PRs/issues/docs, remove accidental or superseded temporary state, preserve evidence/provenance, and leave one clear next step. Never weaken a test, authority gate or ownership rule merely to make work appear complete.
