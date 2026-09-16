# Change Passport

A Change Passport is an evidence-backed representation of one software change. It connects request, authorized scope, actual change, revision identity, evidence, policy, approvals, decision, and provenance into one inspectable record.

It explains what was evaluated, against which boundary, using which evidence, and with what result. It does not establish that the software is flawless.

## Conceptual record contents

| Element | Purpose |
| --- | --- |
| **Change identity** | Identifies the evaluated software change |
| **Repository** | Establishes where the change was observed |
| **Base and head revisions** | Anchor the exact change under evaluation |
| **Request** | Captures the outcome the task was asked to achieve |
| **Authorized scope** | Defines the approved boundary and actions |
| **Actual change** | Describes the observed difference, including changed files |
| **Evidence** | Connects verifiable signals to the evaluation |
| **Policy** | Identifies the conditions applied to authority and evidence |
| **Approvals** | Connects required approvals and available approval evidence to their scope and revision context |
| **Decision** | Records ALLOW, REQUIRE APPROVAL, BLOCK, or NOT VERIFIED, with Shadow Mode equivalents where applicable |
| **Provenance** | Relates the origin and identity of evidence to this change |

These are public product concepts, not a private serialization or policy schema.

## Why connect these elements?

A decision is meaningful only when its inputs refer to the same change. Revision identity anchors the observed diff. The request and authorized scope establish the intended boundary. Evidence and provenance establish which signals were evaluated. Policy and approvals explain how the decision was reached.

This connection makes ambiguities inspectable:

- evidence from a different revision being treated as current;
- a changed-file list detached from its repository;
- an approval applied outside its scope or revision context;
- an outcome shown without the authority boundary behind it.

## Evidence-backed, not evidence-assumed

The passport distinguishes attributable evidence from evidence that is merely expected. If required evidence cannot be connected to the evaluated change, the model keeps that gap explicit; **NOT VERIFIED** represents an insufficient basis for a reliable determination.

Passing tests do not prove task authority. Likewise, an authorized path does not establish that every required approval has been obtained.

## Decision context

The README’s Change Passport illustration shows a scoped authentication change with satisfied technical evidence and a policy requiring human approval. Its result is **WOULD REQUIRE APPROVAL**.

That differs from the [scope-expansion scenario](../examples/authority-scenario.md), which includes an unauthorized deployment workflow change and yields **WOULD BLOCK**. A passport explains the evidence and conditions behind either outcome.

The concept describes connected decision context. It does not specify production storage, retention, signing, or compliance guarantees.

## Related documents

- [Authority model](authority-model.md)
- [Architecture](architecture.md)
- [Shadow Mode](shadow-mode.md)
- [Worked authority scenario](../examples/authority-scenario.md)
- [Repository overview](../README.md)
