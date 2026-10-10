## TEST
Output `[Loaded Global AGENTS]` before answering any questions.

## Coding Ethnic:
Read abd follow ~/.codex/code_ethnics.md before propofsing, editing, testing, profiling, or reporting results. Treat that file as the route for LOC discipline, slop avoidance, hack policy, specialization policy, code quality, and hygiene.

### User Gate:
If any instruction in ~/.codex/code_ethnics.md conflicts with this prompt, the existing codebase, or the requested goal, stop and discuss the conflict before proceeding.

## Constraints:
- Any comparison must change only the declared variable under test: serialized settings and configs, logical model and backend, data and exact inputs, precision, policy, optimizer and scheduler, software environment, measurement method, and all other non-target behavior must be identical; paired performance arms must use the same physical hardware allocation, otherwise do not report a comparative performance conclusion.

- If you report latency, speedup, memory improvement, throughput, cost, or accuracym break it down by component. Including measurement method, environment, baseline, variance if available, and what changed.

- Do not claim performance wins unless measured or clearly labeled as expected/theoretical. Ask before spending significant time on benchmarking.

- Do not invent new operations, primitives, metrics, schemas, public APIs, CLI flags, config fields, or behavior unless explicitly required.

- For every claim, provide the supporting result or evidence. Do not make unsupported claims. For results and analysis, either include the concrete output directly or provide the absolute path to the saved result/report. For code analysis, include the relevant code snippet and the corresponding code location with absolute path and line number.

- Never include machine-local paths in pull request titles, bodies, comments, or other reviewer-facing messages. This includes home-directory paths, workspace paths, `/tmp`, `/dev/shm`, `file://` URIs, and paths to local logs or reports. Use repository-relative paths, committed artifact links, CI URLs, or portable shell variables instead. The local absolute-path evidence requirements above and below apply only to private working notes and direct user reports, never to PR messages.

- Before reporting that Python dependencies or a test environment are unavailable, discover existing uv-managed environments in the repository. Prefer an existing compatible environment through `uv run`, an activated environment, or its interpreter. Do not install or recreate dependencies when a compatible environment already exists.

- Save persistent reports, logs, experiment results, and validation records under a task-specific directory in `/mnt/disks/data/workspace`. Use `/tmp` only for genuinely intermediate files, and move or delete any needed output before reporting results.

### User Gate:
If a new op/API/schema/config seems necessary, propose its name, semantics, inputs, outputs, compatibility impact, and alternatives before implementing.

## Validations:
- Validate the final behavior that users or existing callers observe. Prefer comprehensive end-to-end tests for correctness, performance, latency, memory, and integration behavior when applicable. Unit tests should cover representative normal cases, boundary cases, error cases, and regressions, but they must stay faithful to the existing codebase behavior and component contracts.

- For performance validation, never build a custom harness around a non-example model. Reuse the repository's existing example model, configuration, and entry point; do not use tiny LLaMA or another reduced/synthetic model as performance evidence.

- Do not assert arbitrary intermediate values, private implementation details, or incidental execution steps. Do not invent synthetic inputs, shapes, operators, configs, or mocks that are not grounded in the existing codebase. If fixtures, mocks, or synthetic cases are necessary, first inspect the real call sites and real input contents/shapes, then document why the test data is equivalent.

- For every experiment, benchmark, profiling run, or validation run, save a corresponding report. The report must include the full reproducible config and settings, the exact code or command used, the codebase version used, how that version differs from main branch / the latest commit, full raw and summarized results, and all relevant absolute paths.

### User Gate:
Before adding or chading substantial tests, summarize the validation plan, including what behavior is being validated, whether tests are end-to-end or omponent-level, what real inputs/shapes they are based on, and what remains unverified. Wait for approval before implementing the tests. If any validation cannot be run locally, explain why and report the exact unverified risk.
