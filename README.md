
# Antigravity-no-bullshit

Practical engineering rules for making Antigravity behave less like a code generator and more like a developer maintaining a real codebase.

## What this is

This is a collection of `AGENTS.md` rules and reusable skills for the [Antigravity](https://antigravity.google) AI coding agent.

Instead of treating every task as a greenfield project, these rules push the agent to:

- Understand the existing codebase before changing it.
- Make the smallest reasonable change that solves the problem.
- Preserve working behavior and existing conventions.
- Stay within the requested scope.
- Write code, UI, and documentation that fits the actual project rather than generic generated patterns.

It is not a tool, framework, library, or runtime package. It is a set of guardrails.

## What it tries to prevent

These are common failure patterns when an agent works without enough context or discipline:

- Rewriting working code for no reason.
- Creating abstractions before they are needed.
- Duplicating existing utilities, components, or helpers.
- Scope creep and "while I'm here" cleanup.
- Generic AI-looking UI (excessive gradients, glassmorphism, dashboard-card everything).
- Excessive comments, JSDoc, and documentation that restate the obvious.
- Adding unnecessary dependencies.
- Defensive programming everywhere.
- Changing unrelated files during a focused task.
- Refactoring while implementing an unrelated feature.
- Guessing APIs, data shapes, or project architecture.
- Continuing to "improve" the project after the requested task is already complete.

## Skills

| Skill | Purpose |
|---|---|
| `anti-ai-code` | Avoid unnecessary abstraction, ceremony, boilerplate, and generated-looking implementation patterns. |
| `human-ui` | Keep UI contextual, proportional, and consistent with the existing product. |
| `codebase-first` | Inspect and understand the repository before inventing new architecture. |
| `task-discipline` | Keep implementation within the requested scope. |
| `no-ai-writing` | Keep docs, comments, messages, and copy specific and natural. |
| `surgical-edit` | Make precise local changes while preserving unrelated code. |

`AGENTS.md` sits at `.antigravity/AGENTS.md` and provides the global engineering baseline. Skills live under `.antigravity/skills/` and add deeper, specialized guidance.

## Philosophy

- Understand before changing.
- Use what already exists.
- Change only what needs changing.
- Don't solve hypothetical problems.
- Don't refactor for entertainment.
- Preserve working behavior.
- Verify the actual result.
- Stop when the task is done.

The goal isn't to make AI code "look human". The goal is to make the agent exercise better engineering judgment.

## Structure

```
.antigravity/
├── AGENTS.md
└── skills/
    ├── anti-ai-code/
    │   └── SKILL.md
    ├── human-ui/
    │   └── SKILL.md
    ├── codebase-first/
    │   └── SKILL.md
    ├── task-discipline/
    │   └── SKILL.md
    ├── no-ai-writing/
    │   └── SKILL.md
    └── surgical-edit/
        └── SKILL.md
```

## Usage

1. Copy the `.antigravity/` directory into your project root.
2. Keep `AGENTS.md` at `.antigravity/AGENTS.md`.
3. Place skills under `.antigravity/skills/<skill-name>/SKILL.md`.
4. Antigravity will pick up these project-level instructions when working in the repository.

That's it. No build step, no dependencies, no configuration file.

## Adding new skills

New skills are welcome when they:

- Solve a recurring engineering problem.
- Are specific enough to be actionable.
- Complement existing rules instead of duplicating them.
- Avoid turning every personal preference into another giant rulebook.
- Contain practical guidance and constraints, not generic advice.

If a skill can be summarized as "write good code", it probably belongs in `AGENTS.md` or nowhere at all.

## License

Released under the [MIT License](LICENSE).

## Disclaimer

These are engineering guidelines, not universal laws. Project-specific instructions and explicit user requirements take precedence.