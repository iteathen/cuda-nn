# CUDA-NN specifications

**Architecture/ownership authority is accepted; production NN specifications remain separately gated.**

- [`SPEC-0001-native-boundary-and-js-only-implementation.md`](SPEC-0001-native-boundary-and-js-only-implementation.md) — accepted cross-cutting rule that CUDA-NN remains JavaScript/TypeScript, CUDA-JS owns native CUDA/provider integration, and NN semantics/planning stay above the native boundary. This specification does not authorize production NN implementation.

The [bootstrap and activation program](https://github.com/iteathen/cuda-nn/issues/1) organizes assessment. Production implementation still requires bounded, consumer-backed semantic contracts accepted under the [development instructions](../../AGENTS.md).

Start with the [project charter](../PROJECT_CHARTER.md) and [architecture decisions](../decisions/README.md) to understand the intended scope.
