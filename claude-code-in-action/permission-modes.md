# Permission modes

How much Claude Code may do before asking. Not Cursor Auto or Cost.

| Mode | Reads | Edits | Bash | Asks you | Use when |
| --- | --- | --- | --- | --- | --- |
| Manual | yes | ask | ask | always, except reads | learning |
| Accept edits | yes | yes | common yes | unusual commands | daily coding |
| Plan | yes | no | explore if classifier ok | before any real change | design first |
| Auto | yes | yes | yes if classifier ok | rarely | trusted repo, you are watching |
| Don't ask | workspace only | only if pre-approved | only pre-approved | never, deny instead | CI or a locked agent |
| Bypass | everything | everything | everything | never | isolated agent VM only |

## Manual

Reads go. Edits, bash, network, and installs ask every time.

## Accept edits

Reads, edits, and common local bash (`ls`, tests, `git status`, maybe `npm test`) run. Review the diff after. Odd commands still prompt.

## Plan

No edits. It reads and proposes a plan. Approved explore commands can run. Nothing is applied until you leave Plan.

## Auto

Default yes. A classifier can still block or ask on dangerous bash (`rm -rf`, `curl | sh`, secrets).

## Don't ask

Project reads and pre-approved tools only. Anything else is denied. No popup, so it cannot ask for more.

## Bypass permissions

No checks. Same as `--dangerously-skip-permissions`. Throwaway VM or container only, never a laptop with prod credentials.
