# Hooks

A line in `CLAUDE.md` is a request. A hook is code that runs at a fixed point, so Claude cannot skip it.

Claude Code fires about 30 hook events. These are the ones to use.

| Hook | When | What you use it for |
| --- | --- | --- |
| PreToolUse | Before a tool call | Stop or rewrite the call. The enforcement hook. |
| PostToolUse | After a successful tool call | Format or lint. Too late to stop the call. |
| Stop | Claude wants to end the turn | Refuse if a condition is unmet. |
| SubagentStop | A sub-agent finishes | Same as Stop, for that sub-agent. |
| PreCompact | Before compaction | Record what must survive, or block the compact. |
| PostCompact | After compaction | Does not put output back into the conversation. |
| InstructionsLoaded | A `CLAUDE.md` or rule file loads | Audit what entered context. |
| SessionStart | Session starts, and after compact | Prime the environment. Re-inject context after compact. |

## Re-inject after compact

`PostCompact` does not feed its output back into the conversation. Use `SessionStart` with the `compact` matcher. That output is inserted into the conversation. Use the `startup` source on `SessionStart` when you only want a fresh start.

## PreToolUse decision

Print JSON and exit 0. `permissionDecision` is `allow`, `deny`, or `ask`. `defer` is only for non-interactive `-p` runs.

`updatedInput` replaces the whole tool input. Echo every field you are not changing. Use it to redact a secret and still let the command run.

```json
{
  "hookSpecificOutput": {
    "hookEventName": "PreToolUse",
    "permissionDecision": "deny",
    "permissionDecisionReason": "...",
    "updatedInput": {
      "command": "..."
    }
  }
}
```

A Bash matcher can watch one tool, and an `if` can narrow it to one command. Example: a command contains `sk_live_`, the hook swaps it for a placeholder, then the command runs without the secret.

## Exit codes

| Code | Effect |
| --- | --- |
| 0 | Success. JSON on stdout is parsed. Plain text is ignored on most events. On SessionStart, UserPromptSubmit, and UserPromptExpansion, plain text is added to context. |
| 2 | Blocking error. Stderr is fed back to Claude. This is the code that stops a call. It can also block Stop. |
| 1, or anything else | Non-blocking. Stderr is logged. Claude continues. Exit 1 does not block. |

`PostToolUse` can return text, but the tool already ran. `Notification` and `SessionStart` ignore blocking. `SessionStart` shows stderr only to you.

## What to set up

Guard tools with PreToolUse. Gate the end of a turn with Stop. Preserve state across a compact with SessionStart and the compact matcher.
