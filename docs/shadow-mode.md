# Shadow Mode

Shadow Mode is the observation-first concept for evaluating authority policies without making the results blocking. It makes policy effects, evidence gaps, and false positives inspectable before teams rely on enforcement.

## Non-blocking evaluation

The Shadow Mode model compares requested, authorized, actual, evidence, and decision under applicable policy and approval conditions. Results describe the authority determination while the existing merge and delivery process remains in control.

Missing or insufficient evidence remains visible as **NOT VERIFIED**; uncertainty is not silently converted into approval.

## Shadow outcomes

| Outcome | Meaning |
| --- | --- |
| **WOULD ALLOW** | The change is within authority and satisfies required evidence, policy, and approval conditions |
| **WOULD REQUIRE APPROVAL** | A designated human approval is required |
| **WOULD BLOCK** | An authority or policy boundary was violated |
| **NOT VERIFIED** | Available evidence cannot support a reliable determination |

These are observation outcomes. They do not themselves gate the change or assert that authorized code is correct.

## Observe before enforcement

Representative tasks and changes provide a basis for assessing authority policies. Comparing outcomes across those changes can reveal:

- underspecified requests;
- boundaries that are too broad or too narrow;
- missing or outdated evidence;
- unclear approval ownership;
- false positives and missed scope expansion.

The goal is to understand whether the policy captures the team’s intended authority boundary.

## Compare with human review

Differences between shadow outcomes and human review are useful signals. A reviewer may identify authorization context that was not captured. An authority comparison may expose scope expansion that a review focused on behavior did not flag.

Neither side is automatically correct. Investigating disagreements helps distinguish policy problems, evidence gaps, and review omissions.

## Calibrate policies before relying on enforcement

Observation supports refinement of authorized scopes, evidence requirements, exception paths, and approval rules. A useful sequence is:

1. Observe representative changes without gating them.
2. Compare authority outcomes with human judgment.
3. Investigate disagreements, false positives, and evidence gaps.
4. Refine boundaries and approval requirements.
5. Assess whether the policy and evidence are reliable enough to support enforcement.

This sequence describes how to evaluate authority controls; it does not claim a production enforcement deployment.

## Related documents

- [Authority model](authority-model.md)
- [Architecture](architecture.md)
- [Change Passport](change-passport.md)
- [Worked authority scenario](../examples/authority-scenario.md)
- [Repository overview](../README.md)
