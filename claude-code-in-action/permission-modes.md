# Permission modes

Permission modes set how much Claude Code may do on your machine before asking. They are not Cursor Auto or Cost.

## Manual

Reads go through. Edits, bash, network, and installs ask every time. You allow or deny each action. Slowest, safest while you learn.

## Accept edits

Reads, file edits, and common local bash (`ls`, tests, `git status`, maybe `npm test`) run without asking. You review the diff after. Odd or risky commands still prompt. Default for writing code you will review.

## Plan

No edits. Claude reads and proposes a plan. Explore commands a classifier approves can run. It does not apply the change until you leave Plan. Use this before a big refactor.

## Auto

Default yes to almost everything. A second classifier looks at each action, especially bash, and can still block or ask if it looks dangerous (`rm -rf`, `curl | sh`, secrets). Faster. You trust the classifier, not a click each time.

## Don't ask

Reads in your project dirs and pre-approved tools only. Anything that would have prompted is denied, with no popup. It cannot widen permissions by asking you.

## Bypass permissions

No checks. Same as `--dangerously-skip-permissions`. Full shell. Only in a throwaway VM or container, never on a laptop with prod credentials.

## What runs

| Mode | Reads | Edits | Bash | Asks you |
| --- | --- | --- | --- | --- |
| Manual | yes | ask | ask | always, except reads |
| Accept edits | yes | yes | common yes | unusual commands |
| Plan | yes | no | explore if classifier ok | before any real change |
| Auto | yes | yes | yes if classifier ok | rarely |
| Don't ask | workspace only | only if pre-approved | only pre-approved | never, deny instead |
| Bypass | everything | everything | everything | never |

Pick by blast radius. Learning: Manual. Daily coding: Accept edits. Design first: Plan. Trusted repo while you watch: Auto. CI or a locked agent: Don't ask. Isolated agent VM: Bypass.
