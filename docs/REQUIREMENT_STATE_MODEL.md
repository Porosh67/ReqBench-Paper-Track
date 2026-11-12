# Requirement-state model

ReqBench models a requirement as more than a sentence retrieved from conversation history. Each requirement has a lifecycle state and a separate role/scope classification.

| Axis | Values | Question answered |
|---|---|---|
| Lifecycle | `active`, `superseded`, `cancelled` | Does this requirement currently govern behavior? |
| Role/scope | `ordinary`, `persistent`, `exception` | How broadly and for how long does it apply? |

The axes are orthogonal. For example, a persistent compatibility constraint can remain `active` after a default changes; a scoped exception can be active only under its stated conditions; a superseded default should not be revived merely because it appears earlier in the transcript.

The benchmark compares how four input protocols communicate this state (A/B/C/D in the main paper). A correct natural-language explanation is not sufficient by itself: the resulting repository patch and regression behavior must be evaluated independently.
