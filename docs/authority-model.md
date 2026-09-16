# The SENTARYN Authority Model

SENTARYN evaluates AI-generated software changes against explicitly delegated authority. Its model separates what was requested, what was authorized, what actually changed, what can be evidenced, and what policy decides.

> **Requested → Authorized → Actual → Evidence → Decision**

## Requested

**Requested** captures the intended outcome of the change in context: the task, issue, instruction, or objective an agent was asked to address.

A request explains purpose, but it is not necessarily a complete authorization. “Fix authentication timeout,” for example, does not imply permission to change deployment workflows, dependency policy, billing code, or every other reachable part of a repository.

## Authorized

**Authorized** defines the approved boundary for the change. Depending on policy, that boundary may include allowed paths, prohibited paths, permitted change types, required evidence, approval conditions, or other public control concepts.

Authorization should be specific to the change and evaluated independently of the agent's technical capabilities.

## Actual

**Actual** is the observed change between defined base and head revisions. It represents what happened—not what the request or agent description says happened.

At a minimum, actual scope can include the files changed. An authority evaluation relates that observed scope back to the authorized boundary.

## Evidence

**Evidence** consists of verifiable signals used to support evaluation. Examples may include revision identity, changed-file data, test results, review state, or provenance information.

Evidence must remain distinct from the conclusion drawn from it. Passing tests can support a correctness claim, but cannot by themselves establish that every changed path was authorized.

## Decision

**Decision** is the explicit outcome produced after authority, evidence, and policy evaluation:

- **ALLOW** — authorized conditions are satisfied.
- **REQUIRE APPROVAL** — a designated approval is required before proceeding.
- **BLOCK** — an authority or policy boundary was violated.
- **NOT VERIFIED** — the evidence is insufficient for a reliable determination.

In Shadow Mode, the first three outcomes are reported as **WOULD ALLOW**, **WOULD REQUIRE APPROVAL**, and **WOULD BLOCK** without enforcing them.

## Access != Authority

Access determines what an identity or tool is technically capable of doing. Authority determines what that actor is permitted to do for a particular change.

Broad repository access may be operationally necessary for an agent to work, but it should not silently expand the scope of every task. An actor can have permission to write a file at the platform level while lacking authority to modify it in the current change.

## Correctness != Authority

Correctness asks whether a change behaves as intended. Authority asks whether the observed change remained within its approved boundary.

A change can be:

- correct and authorized;
- correct but unauthorized;
- incorrect but authorized in scope; or
- both incorrect and unauthorized.

Tests, static analysis, and review contribute valuable correctness evidence. They do not replace authority evaluation.

## Capability != Authorization

Capability describes what an AI agent can accomplish. Authorization defines which of those possible actions it may take now.

As agent capabilities grow, this distinction becomes more important. SENTARYN is designed as an independent authority layer so that confidence in a model, tool, or agent does not become an implicit grant of unrestricted authority.

## Related documents

- [Architecture](architecture.md)
- [Change Passport](change-passport.md)
- [Shadow Mode](shadow-mode.md)
- [Worked authority scenario](../examples/authority-scenario.md)
- [Repository overview](../README.md)
