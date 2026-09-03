# CUDA-NN

CUDA-NN is the independent repository for **reusable neural-network semantics** in the CUDA-JS ecosystem.

## Current status

**Architecture/bootstrap only. No production NN package, public NN API, native/provider support, training implementation, or performance claim exists yet.**

The repository was created to give NN semantics a natural owner instead of placing them inside the generic CUDA-JS runtime repository. Production implementation remains gated by a consumer-backed assessment: a reusable NN layer must show value beyond a product directly composing `cuda-js-tensor` programs.

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

CUDA-MCGS is a sibling search-semantic framework over generic CUDA mechanisms. Concrete products such as UCI-Arena-Vector retain model-package provenance, feature encoding, policy/action mapping, output-head meaning and other product semantics.

## What belongs here

Only reusable NN meaning that survives first-consumer deletion: model/layer graph semantics, parameter roles, inference composition, NN-specific lowering/provider selection, and—when independently justified—autodiff, gradients, optimizers, RNG, checkpoints and training lifecycle.

Generic CUDA mechanisms route to [`iteathen/CUDA-JS`](https://github.com/iteathen/CUDA-JS). Generic Tensor mathematics routes to [`iteathen/CUDA-JS-Tensor`](https://github.com/iteathen/CUDA-JS-Tensor).

## Development authority

Read [`AGENTS.md`](AGENTS.md) first. The project charter is [`docs/PROJECT_CHARTER.md`](docs/PROJECT_CHARTER.md), and the repository split is recorded by [`ADR-0001`](docs/decisions/ADR-0001-independent-nn-semantic-owner.md).

Open issues are planning/tracking artifacts, not implementation specifications. In particular, issue #2 must resolve the inference-layer justification question before production NN source is authorized.

## Current roadmap

- #1 — repository bootstrap and ownership program
- #2 — consumer-backed inference-layer justification gate
- #3–#9 — potential NN value/graph/lowering/memory/data/execution semantics
- #10 — deferred training state
- #11–#12 — deferred provider mapping/fusion research
- #13 — inference-first qualification
- #14 — deferred distributed training
- #15 — bootstrap authority packet

The roadmap is intentionally inference-first. Training/autodiff/provider breadth is not required merely because the repository exists.
