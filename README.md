# CUDA-NN

CUDA-NN is the independent repository for **reusable neural-network semantics** in the CUDA-JS ecosystem.

## Current status

**Architecture/governance is integrated. No production NN package, public NN API, native/provider support, training implementation, or performance claim exists yet.**

The repository gives NN semantics a natural owner instead of placing them inside the generic CUDA-JS runtime. Production implementation remains gated by issue #2: a reusable NN layer must show value beyond a product directly composing `cuda-js-tensor` programs.

## Ownership stack

```text
CUDA-JS
  generic CUDA runtime/compiler/Device-JS/memory/execution/provider mechanisms
        ↑
CUDA-JS-Tensor
  generic tensor dtype/shape/layout/math/planning/execution
        ↑
CUDA-NN
  reusable model/layer/inference/autodiff/training semantics
```

Optional semantic dependencies are selected only by accepted NN profiles:

```text
CUDA-NN -> cuda-rng   reusable RNG/distribution/reproducibility semantics
CUDA-NN -> cuda-comm  reusable collective/P2P/PGAS/RMA communication semantics
```

CUDA-NN retains the NN-specific reason those capabilities matter: initializer/dropout/sampling/training stochastic policy and distributed-training gradient/global-batch/checkpoint semantics. CUDA-JS retains native/provider/device/resource mechanisms such as cuRAND/NCCL/NVSHMEM/TensorRT lower resources.

CUDA-MCGS is a sibling search-semantic framework. Concrete products such as UCI-Arena-Vector retain model-package provenance, feature encoding, policy/action mapping, output-head meaning and other product semantics.

## What belongs here

Only reusable NN meaning that survives first-consumer deletion: model/layer graph semantics, parameter roles, inference composition, NN-specific lowering/provider selection, and—when independently justified—autodiff, gradients, optimizers, NN stochastic policy, checkpoints, distributed-training policy and training lifecycle.

Generic CUDA mechanisms route to [`iteathen/CUDA-JS`](https://github.com/iteathen/CUDA-JS). Generic Tensor mathematics routes to [`iteathen/CUDA-JS-Tensor`](https://github.com/iteathen/CUDA-JS-Tensor). Reusable RNG semantics route to [`iteathen/cuda-rng`](https://github.com/iteathen/cuda-rng); reusable communication semantics route to [`iteathen/cuda-comm`](https://github.com/iteathen/cuda-comm).

## Development authority

Read [`AGENTS.md`](AGENTS.md) first. The project charter is [`docs/PROJECT_CHARTER.md`](docs/PROJECT_CHARTER.md). [`ADR-0001`](docs/decisions/ADR-0001-independent-nn-semantic-owner.md) owns the independent NN repository split and [`ADR-0002`](docs/decisions/ADR-0002-rng-comm-semantic-composition.md) owns optional RNG/COMM composition.

Open issues are planning/tracking artifacts, not implementation specifications. Issue #2 must resolve the inference-layer justification question before production NN source is authorized.

## Current roadmap

- #2 — consumer-backed inference-layer justification gate;
- #3–#9 — potential NN value/graph/lowering/memory/data/execution semantics;
- #10 — deferred training state;
- #11–#12 — deferred provider mapping/fusion research;
- #13 — inference-first qualification;
- #14 — deferred distributed training over `cuda-comm` semantics and CUDA-JS native mechanisms;
- #17 — repository controls/protected `main`;
- #18 — deferred TensorRT semantic eligibility/equivalence;
- #19 — RNG/COMM ownership reconciliation represented by ADR-0002 after integration.

The roadmap is intentionally inference-first. Training/autodiff/provider breadth is not required merely because the repository exists.
