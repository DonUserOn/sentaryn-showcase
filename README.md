# SENTARYN

## Authority for AI-generated software changes.

**Control what AI changes in your software.**

SENTARYN’s authority model connects a task’s intent to the software change it produced, asking:

**Was this change authorized?**

> **Public product showcase**
> This repository demonstrates SENTARYN’s authority model, product concepts, and illustrative evaluation flows. It does not contain proprietary implementation details or customer data.

## The problem

AI coding agents may have broad repository access. That access does not establish whether a specific task authorized changes to a particular file, sensitive workflow, infrastructure, configuration, or deployment process. It also does not establish whether approval-sensitive actions received the required approval.

Tests can pass while task authority was exceeded. Engineering teams need to inspect both the quality of a change and the authority behind it.

## Access is not Authority

**Access is not Authority.**

Repository access describes what an identity or tool can do. Authority defines what a specific task permits it to change, under which evidence and approval conditions.

```text
Can modify repository ≠ Authorized to modify every path
Can open a pull request ≠ Authorized scope was respected
Tests passed ≠ Change was authorized
```

## Core authority model

**Requested → Authorized → Actual → Evidence → Decision**

SENTARYN’s authority model compares five connected elements:

| Element | Question |
| --- | --- |
| **Requested** | What outcome was asked for? |
| **Authorized** | What scope and actions were approved for this task? |
| **Actual** | What did this exact revision change? |
| **Evidence** | What verifiable signals support the evaluation? |
| **Decision** | Does the change satisfy authority, evidence, policy, and approval conditions? |

A request establishes intent. Authorized scope establishes the boundary. The actual change and its evidence establish what can be evaluated. Policy and required approvals determine the authority decision.

See the [authority model](docs/authority-model.md) for the underlying distinctions.

## Worked example: authentication timeout

**Request:** Fix authentication timeout

**Authorized scope:**

```text
src/auth/**
tests/auth/**
```

**Actual changed files:**

```text
src/auth/session.py
tests/auth/test_session.py
.github/workflows/deploy.yml
```

| Signal | Result |
| --- | --- |
| Evidence | Tests **PASSED** |
| Authority | **EXCEEDED** |
| Decision | **WOULD BLOCK** |
| Reason | Unauthorized scope expansion |

The two authentication files are within scope. The deployment workflow is outside the authority granted for this task. Passing tests do not authorize that additional change.

**The code may work. The change can still exceed the authority granted by the task.**

Follow the [full scenario](examples/authority-scenario.md) for the evaluation trace and appropriate next steps.

## Authority decision

This illustrative public product demonstration shows **WOULD BLOCK** for scope expansion, with missing authorization evidence made explicit alongside passing tests.

<p align="center">
  <img src="assets/authority-decision.png" alt="Illustrative SENTARYN authority decision: WOULD BLOCK for an unauthorized deployment workflow change and missing authorization evidence" width="900">
</p>

The model uses a small, explicit decision vocabulary:

| Outcome | Meaning |
| --- | --- |
| **ALLOW** | Authorized scope, required evidence, policy, and approval conditions are satisfied |
| **REQUIRE APPROVAL** | A designated human approval is required before proceeding |
| **BLOCK** | An authority or policy boundary was violated |
| **NOT VERIFIED** | Available evidence is insufficient for a reliable determination |

Shadow Mode expresses the first three as observation outcomes prefixed with **WOULD**. An authority decision does not establish that the implementation is correct or secure.

## Authority Map

The Authority Map makes the difference between **authorized scope**, **actual scope**, and **scope expansion** visually inspectable. In the authentication example, it connects the two authorized files to their approved paths and highlights the deployment workflow outside that boundary.

<p align="center">
  <img src="assets/authority-map.png" alt="SENTARYN Authority Map showing two files within authorized scope and a deployment workflow outside authority" width="900">
</p>

The map explains where actual scope diverges from authority; the connected evidence explains the decision.

## Change Passport

A Change Passport is an evidence-backed representation of one software change. It connects **request, authorized scope, actual change, revision identity, evidence, policy, approvals, decision, and provenance** into one inspectable record.

<p align="center">
  <img src="assets/change-passport.png" alt="Illustrative Change Passport linking a scoped authentication change to revision identity, evidence, policy, provenance, and a WOULD REQUIRE APPROVAL decision" width="900">
</p>

This example shows a different authority condition: the change stays within scope and technical evidence is satisfied, but policy still requires human approval. Scope compliance and required approvals are separate parts of the decision.

See the [Change Passport overview](docs/change-passport.md) for how the record connects these elements.

## Shadow Mode

Shadow Mode is the observation-first concept for evaluating authority policies without making the results blocking:

- **WOULD ALLOW**
- **WOULD REQUIRE APPROVAL**
- **WOULD BLOCK**
- **NOT VERIFIED**

<p align="center">
  <img src="assets/shadow-mode.png" alt="Illustrative Shadow Mode result showing NOT VERIFIED because required evidence is incomplete" width="900">
</p>

Comparing these outcomes with human review helps teams identify false positives, missing evidence, and unclear approval boundaries before relying on enforcement. **NOT VERIFIED** keeps uncertainty visible instead of treating missing evidence as approval.

Read the [Shadow Mode overview](docs/shadow-mode.md) for the observation and calibration sequence.

## Authority is a distinct control

SENTARYN focuses on task-specific authority alongside existing engineering controls.

| Control | What it answers | What it does not prove |
| --- | --- | --- |
| **Correctness / tests** | Did the implementation behave as expected? | That the task authorized every change |
| **Code review** | Did a reviewer assess the proposed change? | That task authority and required evidence were explicitly checked |
| **Identity** | Who or what acted? | What that actor was authorized to change for this task |
| **Repository access** | Can the actor perform an operation? | That this task permits that operation |
| **Authority** | Was this task permitted to make this change? | That authorized code is automatically correct |

These controls reinforce one another. Tests evaluate behavior; authority evaluates permission for the specific task and change.

## What SENTARYN is not

- Not another coding agent.
- Not a replacement for tests.
- Not a replacement for code review.
- Not a general vulnerability scanner.
- Not simply repository permissions.
- Not a claim that authorized code is automatically correct.

SENTARYN focuses on a different control question:

**Was this exact software change authorized for this exact task, with the required evidence?**

## Agent-independent design

The authority model is independent from the agent that generated the change. Its inputs concern the task, authorized boundary, resulting revision, and evidence.

The same control question applies to changes generated with Codex, Claude Code, Cursor, GitHub Copilot, or internal coding agents. These are examples of generation environments, rather than claims of formal integrations.

## Repository guide

| Path | Purpose |
| --- | --- |
| [docs/architecture.md](docs/architecture.md) | Public evaluation flow and conceptual trust boundaries |
| [docs/authority-model.md](docs/authority-model.md) | Requested, authorized, actual, evidence, and decision |
| [docs/change-passport.md](docs/change-passport.md) | Connected evidence and decision context for one change |
| [docs/shadow-mode.md](docs/shadow-mode.md) | Observation, review comparison, and policy calibration |
| [examples/authority-scenario.md](examples/authority-scenario.md) | Worked authentication-timeout evaluation |
| [assets/README.md](assets/README.md) | Inventory and guidance for public product imagery |

## Explore SENTARYN

**Let AI build. Keep control.**

[Visit SENTARYN](https://sentaryn.com) · [Request early access](https://sentaryn.com/early-access)
