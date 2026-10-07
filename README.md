# WAKEUPIDIOT

WAKEUPIDIOT is a single-file AI coding skill that cuts wasted context and unnecessary code. It makes an AI map the repository, retrieve only the relevant path, understand the real flow, and then ship the smallest correct change.

## What it does

Most coding agents waste tokens in two places:

1. Reading far more of the repository than the task requires.
2. Writing abstractions, dependencies, and scaffolding the product did not ask for.

WAKEUPIDIOT attacks both. It narrows repository context before implementation, traces callers and dependencies, reuses what already exists, and stops at the first simple solution that fully works.

## Install

The complete installable skill is [`SKILL.md`](./SKILL.md). Copy that one file into your AI tool's instruction or skill location.

### Codex

```bash
mkdir -p ~/.codex/skills/wakeupidiot
curl -L https://raw.githubusercontent.com/Pedroshakoor/wakeupidiot/main/SKILL.md \
  -o ~/.codex/skills/wakeupidiot/SKILL.md
```

Restart Codex, then invoke `$wakeupidiot` or ask it to minimize token usage while working on a codebase.

### Claude Code

```bash
curl -L https://raw.githubusercontent.com/Pedroshakoor/wakeupidiot/main/SKILL.md \
  -o CLAUDE.md
```

### Cursor, Windsurf, Cline, Roo Code, and other AI tools

Copy the contents of [`SKILL.md`](./SKILL.md) into the tool's project rules, system instructions, or reusable skill directory. The file has no runtime dependency and works with any AI that accepts Markdown instructions.

## How it works

```text
User request
    ↓
Map or search the repository
    ↓
Retrieve only connected files, symbols, callers, and tests
    ↓
Trace the real execution path
    ↓
Reuse → standard library → native platform → installed dependency
    ↓
Write the smallest correct diff
    ↓
Run the smallest meaningful verification
```

The workflow remains tool-neutral. If a repository graph exists, the AI uses it. If not, it falls back to targeted search and dependency tracing.

## Benchmark

The benchmark configuration reduced token burn by **up to 89.1%**.

| Stage | Result |
|---|---:|
| Repository context | 1,512 nodes narrowed to 211 |
| Context reduction | 86.0% |
| Remaining-work token reduction | 22% |
| Combined sequential reduction | **89.1%** |

Formula:

```text
1 - (211 / 1512) × (1 - 0.22) = 0.891
```

The implementation benchmark covered 12 feature tasks with four runs per task. Actual savings vary with repository size, task shape, index quality, and model behavior.

## Principles

- Understand before editing.
- Retrieve evidence, not the entire repository.
- Fix root causes at shared points.
- Reuse before writing.
- Delete before abstracting.
- Preserve correctness, security, validation, and accessibility.
- Verify the behavior with the smallest meaningful check.

## License

MIT
