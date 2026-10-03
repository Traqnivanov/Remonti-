# IVANOV REMONTI — START HERE

This repository is a live website repository. Safety takes priority over cleanup speed.

## GLOBAL RULE #1 — NOTHING GOES LIVE WITHOUT OWNER APPROVAL

This rule applies to **ALL work in this repository**, not only cleanup.

**NOTHING may be merged to `main`, deployed, published, or otherwise made live without BOTH:**

1. the mandatory pre-merge checks being completed successfully; and
2. the Owner explicitly writing **`merge`** for that exact PR/change set.

Approval of an idea, task, implementation, screenshot, preview, or code change is **NOT** permission to merge or deploy.

Before every merge to `main`, the responsible chat/agent must verify at minimum:

- the exact PR/head SHA;
- the exact changed-file list;
- the exact diff against current `main`;
- that there are no unrelated or unexpected changes;
- technical QA relevant to the change;
- visual/functional QA when applicable;
- that the branch is based on or reconciled with current `main`;
- that the PR is still unmerged before the final Owner command.

If any check fails, is incomplete, or is ambiguous: **DO NOT MERGE.**

Without the exact Owner command **`merge`**: **NO MERGE, NO DEPLOY, NO LIVE CHANGE.**

## Mandatory first step for any cleanup work

Before auditing, moving, renaming, deleting, or "organizing" repository files, read **CLEANUP_SAFETY_RULES.md** in full.

The cleanup protocol is mandatory for every chat, tool, agent, and future handoff.

### Non-negotiable defaults

- **DO NOT delete anything by default.**
- **Unknown or uncertain = KEEP.**
- No direct cleanup changes on `main`.
- No delete, rename, move, history rewrite, force-push, or merge without the required Owner approval.
- Cleanup begins as **read-only audit only**.
- Every deletion must be proven safe file-by-file and approved by the Owner by exact path.
- Cleanup changes must use a separate safety branch and Draft PR.
- Merge happens only after final QA and explicit Owner command: **`merge`**.
- If two rules conflict, the stricter rule wins.

Current authoritative cleanup policy: **CLEANUP_SAFETY_RULES.md**  
Current cleanup state/log: **CLEANUP_AUDIT.md**
