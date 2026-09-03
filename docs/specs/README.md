# CUDA-NN Specifications

**Status:** Informational

CUDA-NN currently has **no accepted production component/API specification**.

The repository split and ownership decision are recorded by [`ADR-0001`](../decisions/ADR-0001-independent-nn-semantic-owner.md). That decision establishes where reusable NN semantics belong if they are justified; it does not authorize implementation.

## Current gates

1. Issue #2 must first determine whether a reusable inference layer adds genuine NN semantic value beyond direct product → CUDA-JS-Tensor composition.
2. Every retained production boundary then requires an accepted bounded specification stating semantic ownership, public/internal contracts, dependencies, finite resources/lifecycle, errors, compatibility, cleanup, deletion behavior and decisive falsifiers.
3. Native/provider/numerical/performance claims require evidence appropriate to those claims and exact consumed lower-layer identities.

Open roadmap issues #3–#14 are tracking/assessment inputs only. They are not specifications.

Historical CUDA-JS SPEC-0027 is not imported as CUDA-NN authority. Its old same-repository placement, local Tensor ownership and training-first assumptions have been superseded/reassessed; only still-valid rationale may inform future specifications after fresh assessment.
