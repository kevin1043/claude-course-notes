# CLAUDE.md

`CLAUDE.md` is guidance, not enforced config. Every line competes for attention. A longer file is followed less reliably. Keep it short.

## Hooks for hard rules

A rule that must never be broken, such as "never push to main", belongs in a pre-tool-use hook. The hook runs before the action and can block it. Leave softer conventions in `CLAUDE.md`.

## Four locations

Claude loads all of these at launch. They stack. Nothing is dropped.

| Location | What it is |
| --- | --- |
| Managed policy | Org file from the platform team. Always loaded. |
| User | Personal preferences on this machine, every project. |
| Project | Shared with the team, checked into the repo. |
| Local | Gitignored. Personal notes for this repo only. |

Use local for branch-only decisions that should not affect the team.

## Imports

Point at other files to split a long project file:

```
@.claude/conventions/code-style.md
@.claude/conventions/testing.md
@.claude/conventions/workflow.md
```

Imports are expanded inline at launch. They organize the file. They do not reduce context.

## Phrasing

- Specific and checkable. "Put new API routes in `src/api/handlers`, one per file." Avoid "follow best practices."
- Name the replacement. "Use named exports, not default exports."
- Spend emphasis (`IMPORTANT`, `YOU MUST`) on two or three rules. If everything shouts, nothing does.

## Revision

When Claude does the wrong thing, add or fix the rule. You can say "add that to the CLAUDE.md file." Delete any line you cannot justify.
