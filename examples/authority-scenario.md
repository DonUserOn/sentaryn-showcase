# Authority Scenario: Authentication Timeout

This illustrative public product scenario shows why successful tests and task authority are separate controls.

## Request

> Fix authentication timeout

The request identifies an intended outcome. It does not grant unrestricted authority across the repository.

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

Two files are inside the authorized boundary. The deployment workflow is outside it.

## Evidence and evaluation

| Signal | Result |
| --- | --- |
| Evidence | Tests **PASSED** |
| Authority | **EXCEEDED** |
| Decision | **WOULD BLOCK** |
| Reason | Unauthorized scope expansion |

## Why passing tests does not prove authority

Passing tests provide evidence that tested behavior meets its assertions. They do not establish that every changed file was approved or within delegated scope.

The edit to `.github/workflows/deploy.yml` can affect software delivery. Even if it is technically sound and all tests pass, it was not included in the authority granted for this task.

**The code may work. The change can still exceed the authority granted by the task.**

The actual changed paths establish scope expansion. The model therefore reports **WOULD BLOCK** in Shadow Mode. That observation outcome does not itself block a merge.

## Appropriate next steps

Remove the out-of-scope workflow edit, or obtain explicit authorization through the applicable policy and approval process. Re-evaluate the resulting revision and its evidence; approval or test results from another change are not a substitute.

## Authority trace

```text
Requested:   Fix authentication timeout
Authorized:  src/auth/**, tests/auth/**
Actual:      src/auth/session.py
             tests/auth/test_session.py
             .github/workflows/deploy.yml
Evidence:    Tests PASSED; changed-file scope observed
Authority:   EXCEEDED
Decision:    WOULD BLOCK
Reason:      Unauthorized scope expansion
```

The [authority decision illustration](../README.md#authority-decision) additionally makes missing authorization evidence visible. The [Change Passport illustration](../README.md#change-passport) demonstrates a separate case: in-scope changes with a remaining human approval requirement.

## Related documents

- [Authority model](../docs/authority-model.md)
- [Shadow Mode](../docs/shadow-mode.md)
- [Change Passport](../docs/change-passport.md)
- [Architecture](../docs/architecture.md)
- [Repository overview](../README.md)
