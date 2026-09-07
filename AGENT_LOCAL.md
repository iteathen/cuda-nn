# Repository context: cuda-nn

Universal engineering and design guidance comes from the account-global `AGENTS.md`. This file contains only CUDA-NN-specific context.

## Mission and ownership

CUDA-NN is the reusable neural-network semantic layer when an accepted consumer need justifies it. It may own reusable model/layer/NN graph semantics, parameter/NN-state roles, provider-neutral inference composition, and separately accepted autodiff/training semantics.

CUDA-JS-Tensor owns generic Tensor mathematics. CUDA-JS owns generic CUDA mechanisms. RNG/communication/search/product semantics remain with their natural sibling or downstream owners.

## Local routing

- `docs/decisions/` and `docs/specs/` — accepted repository authority.
- Current ownership/status documents and issues — activation/dependency state.
- Public lower-layer contracts — exact CUDA-JS-Tensor/CUDA-JS dependency truth.

## Local constraints

Python is prohibited in this repository. Maintained production source does not use direct CUDA FFI, C/C++, CUDA C++, hand PTX, native addons, or private lower-layer imports; lower mechanisms are consumed through public contracts.