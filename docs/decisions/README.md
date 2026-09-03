# CUDA-NN Architectural Decisions

**Status:** Informational

Accepted ADRs are durable historical records. Later decisions may supersede or extend them while preserving provenance.

- [`ADR-0001-independent-nn-semantic-owner.md`](ADR-0001-independent-nn-semantic-owner.md) — establishes CUDA-NN as the independent reusable NN semantic owner above CUDA-JS-Tensor/CUDA-JS, keeps direct product→Tensor composition valid, and requires an inference justification gate before production implementation.
- [`ADR-0002-rng-comm-semantic-composition.md`](ADR-0002-rng-comm-semantic-composition.md) — composes optional reusable RNG and communication semantic owners without transferring NN-specific stochastic/distributed policy or CUDA native/provider mechanisms.

No decision in this repository authorizes a production NN API merely by existing. Accepted specifications and qualification remain separate gates.
