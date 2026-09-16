# Shadow Mode

Shadow Mode lets teams evaluate SENTARYN against software changes without making its decisions blocking. It is an observation and calibration phase for introducing authority controls safely.

## Non-blocking evaluation

In Shadow Mode, the same authority flow can examine the request, authorized scope, actual change, evidence, and applicable policy. The result is reported for inspection, while the existing merge and delivery process remains in control.

Shadow Mode does not silently convert an uncertain result into approval. Missing or insufficient evidence remains visible as **NOT VERIFIED**.

## Shadow outcomes

- **WOULD ALLOW** — the evaluated change is within authority and meets the observed policy and evidence conditions.
- **WOULD REQUIRE APPROVAL** — enforcement would require a designated human approval.
- **WOULD BLOCK** — enforcement would stop the change because an authority or policy boundary was violated.
- **NOT VERIFIED** — available evidence cannot support a reliable decision.

These outcomes describe what the authority decision would be under enforcement; they do not themselves gate the change.

## Observe before enforcement

Teams can begin with representative repositories or workflows and observe how authority decisions behave across real changes. This makes policy effects visible before those policies become merge or delivery gates.

The observation period can reveal where requests are underspecified, authority boundaries are too broad or too narrow, evidence is unavailable, or approval ownership needs clarification.

## Compare with human review

Shadow decisions can be compared with existing human review outcomes. Differences are useful signals:

- a reviewer may identify contextual authority that was not captured;
- SENTARYN may expose scope expansion that a correctness-focused review did not flag;
- both may agree that a change should proceed, require escalation, or stop;
- missing evidence may show that no defensible automated decision is possible yet.

The purpose is not to treat either side as automatically correct. It is to make decision boundaries explicit and inspectable.

## Tune policies before gating

Before enabling enforcement, teams can refine authorized scopes, evidence requirements, exception paths, and approval rules based on observed results. A deliberate transition from shadow evaluation to gating reduces surprises and makes ownership clear.

Shadow Mode provides a practical sequence:

1. Observe real changes without blocking them.
2. Compare authority decisions with human judgment.
3. Investigate disagreements and evidence gaps.
4. Tune policies and approval requirements.
5. Introduce gating only when the decision boundary is understood.

## Related documents

- [Authority model](authority-model.md)
- [Architecture](architecture.md)
- [Change Passport](change-passport.md)
- [Worked authority scenario](../examples/authority-scenario.md)
- [Repository overview](../README.md)
