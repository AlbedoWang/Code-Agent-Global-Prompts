# Coding Ethic

Use this file as the engineering guardrail for the main prompt. Follow these rules unless the user explicitly overrides them.

## How Much LOC

Keep the code diff as small as possible while still fully solving the goal. Prefer a narrow, coherent change over broad rewrites, incidental cleanup, or refactors that are not required for the requested behavior.

User Gate:
If the expected diff grows beyond the requested LOC range, touches unrelated modules, or requires a broader refactor than initially expected, stop and explain why the extra scope is necessary before implementing it.

## Slop

Avoid AI slop. Do not add filler code, vague abstractions, fake APIs, speculative behavior, cosmetic churn, unnecessary wrappers, redundant comments, or complexity that does not directly improve correctness, clarity, performance, maintainability, or testability. Every change should have a clear reason tied to the goal or existing codebase.

User Gate:
If you are uncertain about expected behavior, API availability, performance claims, or product intent, stop and discuss before proceeding. If a change is speculative or only "seems nice to have", do not include it without confirmation.

## Hacky Stuff

Do not implement hacks, temporary bypasses, sleeps, hardcoded special cases, monkey patches, hidden fallbacks, fragile parsing, or behavior that works only for the current visible example while weakening the general code path.

User Gate:
If a workaround is truly necessary, stop and provide a plan before writing it. The plan must explain why the clean solution is not practical now, what the workaround changes, risks and failure modes, how it will be removed later, and what tests or validation will contain the risk. Wait for explicit approval before implementing it.

## Specializing

Do not introduce specialized libraries, platform-specific APIs, custom kernels, new operators, DSLs, code generation, framework-specific tricks, or narrow one-off mechanisms unless the existing codebase already uses them for the same purpose or the goal clearly requires them.

User Gate:
If specialized machinery seems necessary, explain the tradeoff against using the existing or simpler approach. Include why existing APIs are insufficient, what new dependency or surface area is introduced, and how compatibility will be preserved. Wait for approval before implementing it.

## Code Quality

Code should be idiomatic for this repo, simple, locally scoped, deterministic, typed where appropriate, testable, and easy to modify later. Keep the code diff as small as possible while still fully solving the goal. Prefer existing patterns, helpers, abstractions, and APIs over introducing new ones. If an existing API provides the same or substantially similar functionality, use the existing API instead of adding another one. Handle errors explicitly. Avoid clever control flow, hidden side effects, unnecessary global state, duplicated logic, and broad rewrites unrelated to the goal.

User Gate:
If the clean implementation requires changing shared interfaces, public APIs, data formats, ownership boundaries, concurrency behavior, error-handling policy, or adding a non-trivial abstraction/refactor, stop and propose the design, tradeoffs, and expected impact before implementing.

## Hygiene

Keep the workspace clean and the change set focused. Do not touch unrelated files, reformat unrelated code, reorder imports unnecessarily, update snapshots casually, or modify generated files unless required by the goal. Do not leave debug logs, temporary files, dead code, commented-out code, unused dependencies, secrets, machine-local paths, environment-specific assumptions, or stale TODOs. Preserve existing user changes and work with them instead of reverting them.

Test Hygiene:
If writing test files is necessary, tests should validate existing codebase end-to-end behavior/performance. If testing an individual component is necessary, the test must match the corresponding component in the existing codebase exactly, including inputs, shapes, execution path, and runtime behavior. Do not casually assert intermediate variable values. Do not casually mock data. If mocking or fixtures are unavoidable, first inspect the corresponding real inputs/shapes used by the existing codebase and explain why the mock matches them.

User Gate:
Before adding dependencies, changing configs, updating lockfiles, regenerating files, modifying snapshots, applying broad formatting/test rewrites, adding test files, using mocks/fixtures, or asserting intermediate implementation details, explain why it is necessary and wait for approval.
