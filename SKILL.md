---
name: wakeupidiot
description: Reduce AI coding token usage by mapping the repository, retrieving only relevant context, and enforcing the smallest correct implementation. Use for coding, debugging, refactoring, architecture questions, and codebase exploration.
license: MIT
---

# WAKEUPIDIOT

Understand the system first. Then make the smallest correct change.

## Workflow

1. **Map before reading broadly.** If a repository graph, index, symbol map, or search database exists, query it first. Otherwise use targeted filename, symbol, import, and caller searches. Never load the whole repository when a narrow dependency path answers the question.
2. **Retrieve within a budget.** Start with the files, symbols, callers, tests, and configuration directly connected to the request. Expand only when evidence shows a missing dependency. Prefer exact source locations over summaries.
3. **Trace the real flow.** For changes and bugs, follow the relevant path end to end before editing. Find every caller of shared code. Fix the root cause at the narrowest shared point.
4. **Climb the minimum-work ladder:**
   - Does this need to exist?
   - Does the repository already solve it?
   - Does the standard library solve it?
   - Does the platform solve it natively?
   - Does an installed dependency solve it?
   - Can one clear line solve it?
   - Only then write the minimum new code.
5. **Keep the diff small.** Reuse before adding. Delete before abstracting. Avoid speculative configuration, wrappers, factories, interfaces with one implementation, and dependencies used for trivial work.
6. **Do not simplify away correctness.** Preserve validation at trust boundaries, security controls, accessibility, data-loss prevention, and explicit user requirements.
7. **Verify proportionally.** Run the smallest check that would fail if the change were wrong. Non-trivial branches, parsers, loops, money paths, and security paths require at least one runnable check.

## Context Rules

- Use graph or symbol traversal for architecture, relationships, and execution paths.
- Cap retrieved context and widen it only when the first result is insufficient.
- Treat generated summaries as navigation aids; verify specific claims against source locations.
- Never invent relationships. Mark uncertain relationships as uncertain.
- Do not rebuild an existing repository index unless it is stale or the user requests it.

## Output

Lead with the result. For implementation work, show the code or changed files first, then state what was deliberately skipped and when it would become necessary. Keep explanations shorter than the change unless the user asks for a report.

## Benchmark

The combined workflow reduced token burn by **up to 89.1%** in the benchmark configuration:

- Repository mapping narrowed 1,512 indexed nodes to 211 relevant nodes: **86.0% less context**.
- Minimum-change execution reduced tokens by a further **22%** on the remaining work across 12 feature tasks with four runs per task.
- Combined sequential reduction: `1 - (211 / 1512) * (1 - 0.22) = 89.1%`.

Results depend on repository size, task shape, index quality, and model behavior. Measure actual usage in the target environment.
