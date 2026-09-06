# CUDA-NN

CUDA-NN is a planned JavaScript library for reusable neural-network models, layers, and inference above CUDA-JS-Tensor.

## Current state

The repository contains an accepted charter and architecture decisions, development guidance, and planning records. **There is no production NN implementation, public API, or package yet.** Native-provider support, training, and performance are not established.

Before implementation, the [inference justification assessment](https://github.com/iteathen/cuda-nn/issues/2) must establish what a reusable NN layer contributes beyond applications composing Tensor programs directly. Keeping direct Tensor composition is a valid outcome.

## Intended scope

The initial aim is reusable model/layer representation and inference composition. Autodiff and training are deferred and require separate justification.

Generic tensor mathematics belongs to [CUDA-JS-Tensor](https://github.com/iteathen/CUDA-JS-Tensor), while [CUDA-JS](https://github.com/iteathen/CUDA-JS) owns GPU runtime/provider mechanisms. Optional random-generation and communication behavior would use CUDA-RNG and CUDA-COMM; specific models and application outputs remain with consumers.

## Start here

- [Current status](STATUS.md) and [project charter](docs/PROJECT_CHARTER.md).
- [Architecture decisions](docs/decisions/README.md) and [specification status](docs/specs/README.md).
- [Development instructions](AGENTS.md) and [shared contribution guide](https://github.com/iteathen/.github/blob/main/CONTRIBUTING.md).
- [Private security reporting](https://github.com/iteathen/.github/blob/main/SECURITY.md).
- [License](LICENSE).
