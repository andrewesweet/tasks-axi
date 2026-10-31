# Issue tracker: external tasks-axi backlog

Work items for this repository are tracked outside the repo, in a [tasks-axi](https://www.npmjs.com/package/tasks-axi) backlog — tasks-axi itself, run from the operator's home. GitHub issues on this repository are used **only for outward-facing discussion** (bug reports, questions, proposals from outside); they are not the work queue.

## Conventions

- Work items are tasks in the tasks-axi backlog: a plain markdown file managed by the `tasks-axi` CLI. Use the CLI rather than editing the file by hand; `npx -y tasks-axi --help` is the command reference.
- Task ids are caller-supplied slug-shaped join keys (for example `fix-roundtrip-k2`); `add --mint` generates one when no id is supplied.
- A task that touches GitHub notes the pointer in its record as `gh:<owner>/<repo>#<n>`, where `<n>` is the issue or pull request number. Use this exact form so references stay greppable across the tracker.
- Do not mirror internal workflow state (states, holds, dependencies) onto GitHub issues.

## When a skill says "publish to the issue tracker"

Add a task to the tasks-axi backlog, or update the existing task. Create a GitHub issue only when outward-facing discussion is genuinely needed, and note its `gh:<owner>/<repo>#<n>` pointer on the task.

## When a skill says "fetch the relevant ticket"

Read the task from the backlog with the tasks-axi CLI (for example `npx -y tasks-axi show <id> --json`). For outward-facing context, follow the task's `gh:<owner>/<repo>#<n>` pointer with `gh issue view` or `gh pr view`.
