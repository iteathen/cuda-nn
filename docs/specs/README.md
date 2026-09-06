# CUDA-NN specifications

**Architecture/ownership authority is accepted; production NN specifications remain separately gated.**

- [`SPEC-0001-native-boundary-and-js-only-implementation.md`](SPEC-0001-native-boundary-and-js-only-implementation.md) — accepted cross-cutting rule that CUDA-NN remains JavaScript/TypeScript, CUDA-JS owns native CUDA/provider integration, and NN semantics/planning stay above the native boundary. This specification does not authorize production NN implementation.

The [bootstrap program](https://github.com/iteathen/cuda-nn/issues/1) owns repository/authority progression. The [inference justification assessment](https://github.com/iteathen/cuda-nn/issues/2) still determines whether a reusable NN layer adds value beyond direct Tensor composition. Retained capabilities then require bounded, consumer-backed accepted contracts and appropriate qualification under [AGENTS.md](../../AGENTS.md).

The [architecture decisions](../decisions/README.md) establish ownership and optional RNG/communication composition. Roadmap issues organize work and do not authorize implementation. Historical CUDA-JS SPEC-0027 does not govern this repository.

Start with the [project charter](../PROJECT_CHARTER.md) for the complete semantic boundary.
