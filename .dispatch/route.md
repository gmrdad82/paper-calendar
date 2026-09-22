# The route

Being handed `--merge` is the owner's word: never ask about commit, rebase,
merge or push.

1. In the card's worktree: stage what the runbook's "Files to stage" names
   and is not yet committed, plus the runbook. Never `git add .` or `-A`.
2. Commit signed: `<ID>: short imperative line`, no trailers. No signing:
   stop, say so in the runbook, land nothing.
3. `git fetch origin && git rebase origin/main`. A conflict that needs
   another card's work ported: abort, write `## Merge attempt <n>`, stop.
4. Build once: it compiles. Never a test, a suite, a gate or a rig.
5. `git push origin HEAD:main`.
6. Fast-forward the checkout's main; remove the worktree and the branch.
7. Append `## Landing` to the runbook; commit it as `<ID>: land`; push.

Alone: a flake in an untouched part, rerun once; a scanner hit on a fixture,
an allow marker; a build error this landing caused, one fix, then stop.
