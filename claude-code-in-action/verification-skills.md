# Verification skills

If you have typed the same multi-step instruction twice, make it a skill. Build a verification skill first, so checking does not depend on you remembering to ask.

## What it does

When a change matches the skill description, the skill runs on its own:

1. Run the test suite.
2. Read the diff.
3. Check that no test was weakened to force a pass.
4. Report pass or fail with the evidence.

Done means the gates ran and the results were stated. A green suite alone is not enough.

The same shape fits a release checklist, a migration recipe, or a pre-PR check.

## Skill folder

A skill is a folder with `SKILL.md`: a name, a description that triggers it, and the procedure. Only descriptions load until the skill is needed.

- `reference.md` holds detail. Link it from `SKILL.md`. Claude reads it only when it needs that depth.
- Scripts, such as `check.sh`, are executed. Their source is not loaded into context.

Keep `SKILL.md` short. Put depth and tools in side files.

Check the skill into `.claude/skills` so the team shares it.

## Where a rule belongs

| Kind of rule | Where |
| --- | --- |
| Always-on conventions (names, file locations) | `CLAUDE.md` |
| A repeated procedure for one kind of task | Skill |
| A rule Claude must not be able to skip | Hook |

`CLAUDE.md` and skills are instructions. A hook is code that runs.
