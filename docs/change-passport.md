# Change Passport

A Change Passport is a single evidence-backed record for one software change. It binds intent, authority, observed change, evidence, policy, and outcome so that the basis of a decision can be inspected as one coherent record.

It is not a claim that the software is flawless. It records what was evaluated, against which boundary, using which evidence, and with what result.

## Record contents

| Field | Purpose |
| --- | --- |
| **Change ID** | Stable identifier for the evaluated change |
| **Repository** | Repository in which the change was observed |
| **Base revision** | Immutable revision from which evaluation begins |
| **Head revision** | Immutable revision containing the proposed result |
| **Request** | The outcome the change was intended to achieve |
| **Authorized scope** | Approved boundary for the change |
| **Actual changed files** | Files observed between base and head revisions |
| **Evidence** | Verifiable signals available to the evaluation |
| **Policy** | Policy context applied to authority and evidence |
| **Approval requirements** | Human approvals required by the evaluated conditions |
| **Outcome** | ALLOW, REQUIRE APPROVAL, BLOCK, or NOT VERIFIED |
| **Provenance / evidence identity** | Identity and origin needed to relate evidence to this specific change |

## Why bind these fields together?

A decision is meaningful only when its inputs refer to the same change. Revision references anchor the observed diff. The request and authorized scope establish the intended boundary. Evidence and its provenance show which signals were evaluated. Policy and approval requirements explain how the outcome was reached.

Keeping these elements together reduces ambiguity such as:

- evidence from a different revision being treated as current;
- a changed-file list being detached from its repository;
- an approval being applied without its required context;
- an outcome being shown without the authority boundary behind it.

## Evidence-backed, not evidence-assumed

The passport distinguishes evidence that is present and attributable from evidence that is merely expected. When required evidence cannot be bound to the evaluated change, the appropriate outcome may be **NOT VERIFIED** rather than an inferred approval.

## Decision record

The Change Passport is the durable explanation surface for an authority decision. A GitHub Check can present the immediate result; the passport preserves the connected record that supports it.

The public concept intentionally omits private schemas, proprietary policy implementation, internal storage design, signing details, and production topology.

## Related documents

- [Authority model](authority-model.md)
- [Architecture](architecture.md)
- [Shadow Mode](shadow-mode.md)
- [Worked authority scenario](../examples/authority-scenario.md)
- [Repository overview](../README.md)
