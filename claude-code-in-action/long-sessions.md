# Long sessions

Long tasks need two habits: scope the work before Claude starts, and steer it while it runs.

## Plan mode

Plan mode researches without editing source files. Claude reads the code and returns a plan. Read the plan and ask for missing pieces before execution. Changing the plan is faster than cleaning up a bad run.

## Compact

`/compact` summarizes the conversation, uses that summary as the new context, and drops the old messages. Add instructions so the summary keeps what still matters:

```
/compact Focus on the --version flag implementation
```

## Rewind

Double-tap Escape on an empty prompt. Every user prompt is a checkpoint.

- Restore code and conversation
- Restore conversation
- Restore code
- Summarize from here (compress a side conversation after the checkpoint)
- Summarize up to here (compress setup, keep the implementation)

## Goal

`/goal` sets a done condition. Claude keeps going until a fast evaluator confirms it. The evaluator only reads the transcript, so the condition must be visible in Claude's output.

```
/goal all tests in src/billing pass, and the type checker reports zero errors
```

Cancel with `/goal clear`.

## Loop

`/loop` runs a prompt on an interval, fixed or self-paced. Use it to poll something external, such as CI or a deploy. Escape stops a self-paced loop while it waits. A fixed loop runs until you cancel it, or for seven days.

## Worktrees

Parallel sessions on one checkout conflict. A worktree gives each session its own file tree. A clean worktree is removed when the session exits.

`.worktreeinclude` at the repo root lists git-ignored files to copy into each worktree, such as `.env` or local config.

## Habits

- Scope first, then steer.
- Tell compact what to keep.
- Rewind when Claude drifts.
- Use a goal when "done" is easier to describe than the steps.
- Put parallel work in worktrees.
