# The SENTARYN Authority Model

SENTARYN’s authority model evaluates AI-generated software changes against explicitly delegated authority. It separates what was requested, what was authorized, what actually changed, what the evidence establishes, and what policy decides.

**Requested → Authorized → Actual → Evidence → Decision**

## Requested

**Requested** captures the intended outcome in context: the task, issue, instruction, or objective an agent was asked to address.

A request explains purpose, but is not necessarily a complete authorization. “Fix authentication timeout” does not imply permission to change deployment workflows, dependency policy, billing code, or every reachable part of a repository.

## Authorized

**Authorized** defines the approved boundary for the task. That boundary can include allowed or excluded paths, permitted actions, required evidence, and approval conditions.

Authorization is specific to the task and change. It is evaluated independently of the agent’s technical capabilities and repository permissions.

## Actual

**Actual** is the observed change between defined base and head revisions. It represents what changed, rather than what the request or agent description says changed.

The worked example uses changed-file scope. Comparing those files with the approved paths makes unauthorized scope expansion explicit.

## Evidence

**Evidence** consists of verifiable signals supporting evaluation, such as revision identity, changed-file data, test results, review state, and provenance.

Evidence and its interpretation remain distinct. Passing tests support claims about tested behavior; they do not establish that every changed path was authorized. Relevant evidence must refer to the evaluated repository and revision.

## Decision

**Decision** is the explicit outcome of authority, evidence, policy, and approval evaluation:

| Outcome | Meaning |
| --- | --- |
| **ALLOW** | Authorized scope and required evidence, policy, and approval conditions are satisfied |
| **REQUIRE APPROVAL** | A designated human approval is required before proceeding |
| **BLOCK** | An authority or policy boundary was violated |
| **NOT VERIFIED** | Evidence is insufficient for a reliable determination |

In Shadow Mode, the first three outcomes are **WOULD ALLOW**, **WOULD REQUIRE APPROVAL**, and **WOULD BLOCK** without gating the change. **NOT VERIFIED** remains distinct from approval.

A known scope violation and insufficient evidence are different findings. The authentication-timeout example establishes a scope violation from the actual changed paths; passing tests do not cancel that finding.

## Access is not Authority

Access determines what an identity or tool is technically capable of doing. Authority determines what the specific task permits it to do.

Broad repository access can help an agent complete its work. It does not silently expand task scope. An actor can have platform permission to write a file while lacking task authority to modify it.

## Correctness is not Authority

Tests ask: **Did the implementation behave as expected?**

Authority asks: **Was this task permitted to make this change?**

A change can be:

- correct and authorized;
- correct but unauthorized;
- incorrect but authorized in scope; or
- both incorrect and unauthorized.

Tests, static analysis, and code review remain valuable controls. Authority adds a separate evaluation of permission, scope, evidence, and required approvals.

## Capability is not Authorization

Capability describes what an agent can accomplish. Authorization defines which actions it may take for this task.

The authority model stays independent from the generation tool so that confidence in an agent does not become an implicit grant of unrestricted authority.

## Related documents

- [Architecture](architecture.md)
- [Change Passport](change-passport.md)
- [Shadow Mode](shadow-mode.md)
- [Worked authority scenario](../examples/authority-scenario.md)
- [Repository overview](../README.md)
