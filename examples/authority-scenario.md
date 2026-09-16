# Authority Scenario: Authentication Timeout

This scenario shows why successful tests and authorized scope are separate controls.

## Request

> Fix authentication timeout

The request identifies an intended outcome, but does not grant unrestricted authority across the repository.

## Authorized scope

```text
src/auth/**
tests/auth/**
```

The agent is authorized to change authentication source files and their tests.

## Actual changed files

```text
src/auth/session.py
tests/auth/test_session.py
.github/workflows/deploy.yml
```

Two files are inside the authorized boundary. The deployment workflow is not.

## Evidence and evaluation

| Signal | Result |
| --- | --- |
| Tests | **PASSED** |
| Authority | **EXCEEDED** |
| Decision | **WOULD BLOCK** |
| Reason | Unauthorized scope expansion |

## Why passing tests does not prove authority

Passing tests provide evidence that the tested behavior meets its assertions. They do not establish that every changed file was necessary, approved, or within delegated scope.

In this scenario, the change to `.github/workflows/deploy.yml` could affect how software is built or delivered. Even if that edit is technically sound and all tests pass, it was not included in the authority granted for the authentication-timeout task.

The result is therefore not “tests passed, so allow.” The authority evaluation records that actual scope exceeded authorized scope and reports **WOULD BLOCK** in Shadow Mode.

The change could proceed only through an appropriate next step defined by policy—for example, removing the unrelated modification or obtaining the required authorization and approval. Correctness evidence remains valuable, but it does not expand authority.

## Authority trace

```text
Requested:   Fix authentication timeout
Authorized:  src/auth/**, tests/auth/**
Actual:      Two authorized files + one unauthorized workflow file
Evidence:    Tests passed; changed-file scope observed
Decision:    WOULD BLOCK
Reason:      Unauthorized scope expansion
```

## Related documents

- [Authority model](../docs/authority-model.md)
- [Shadow Mode](../docs/shadow-mode.md)
- [Change Passport](../docs/change-passport.md)
- [Architecture](../docs/architecture.md)
- [Repository overview](../README.md)
