# SPEC-0001: Native Boundary and JavaScript/TypeScript Implementation

**Status:** Accepted architecture/ownership authority; production NN implementation remains separately gated.

**Version:** 1.0.0

**Owner:** CUDA-NN

**Lower authority:** `iteathen/CUDA-JS` SPEC-0032

## Purpose

CUDA-NN owns reusable neural-network/model/layer/inference/autodiff/training semantics only when independently justified. CUDA-JS is the sole native CUDA/provider integration owner.

## Repository implementation rule

Maintained CUDA-NN source is JavaScript/TypeScript. Restricted Device-JS generation may be used only through public CUDA-JS contracts.

CUDA-NN does not maintain C, C++, CUDA C++, PTX, N-API addons, direct native FFI, Driver/provider bindings, native handles/pointers, ABI structs or platform discovery code. Native evidence may be produced externally and recorded, but native oracle/provider source is not maintained here.

A missing native mechanism routes to CUDA-JS before any local workaround.

## CUDA-NN owns

- reusable NN value/parameter/state/layer/model/graph meaning when justified;
- inference/training composition semantics;
- autodiff, gradients, optimizer, loss, RNG/checkpoint/training-state semantics when selected;
- NN-specific memory/liveness/resource requirements and execution plans;
- semantic provider eligibility, fallback, numerical policy and equivalence;
- NN conformance and JS/TS reference evidence.

## CUDA-NN does not own

- generic Tensor mathematics, which belongs to CUDA-JS-Tensor;
- native allocations, views, transfers, streams, events, graphs, provider handles or compiler artifacts;
- cuBLASLt/cuDNN/TensorRT/NCCL or other native provider lifecycle;
- generic physical memory-management strategy merely because NN has memory pressure;
- product model/checkpoint provenance, feature encoding, search or application meaning.

## Provider boundary

CUDA-NN may decide that an accepted NN operation/subgraph is eligible for a provider profile and define NN-visible precision/fallback/equivalence policy. CUDA-JS owns the bounded native provider resource, ABI, workspace, enqueue, failure and teardown. Generic Tensor math eligibility remains with CUDA-JS-Tensor where appropriate.

## Memory boundary

NN owns semantic lifetime classes such as parameters, activations, residuals, gradients, optimizer state and checkpoint staging. It may project generic size/alignment/access/lifetime/placement constraints.

Native memory primitives remain CUDA-JS-owned. A future cross-domain physical-memory planner is not NN-owned merely because NN motivates it; if independently justified it must be a JavaScript/TypeScript layer consuming public CUDA-JS and must not require NN vocabulary.

## Activation gate preservation

This specification does not resolve the repository's consumer-backed inference-abstraction gate and does not authorize production NN source. Existing issue/specification prerequisites remain in force.

## Supersession

Any historical plan that places native provider/runtime implementation in CUDA-NN is superseded by this boundary. Semantic ownership remains unchanged.

## Non-goals

No native CUDA-NN backend, no Tensor duplication, no provider passthrough, no new production API, and no support/performance claim.
