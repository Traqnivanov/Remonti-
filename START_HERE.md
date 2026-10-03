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

## GLOBAL RULE #2 — EVERY DISCOVERED PROBLEM MUST BE REPORTED AND TRACKED

This rule applies to **ALL work in this repository**.

If any chat, agent, tool, audit, test, or implementation discovers a problem of any kind, it must not be ignored or silently fixed.

Problems include, but are not limited to:

- code bugs or risky logic;
- broken links, missing files, wrong paths or bad filenames;
- HTML/CSS/JS issues;
- UI/mobile/visual defects;
- SEO, sitemap, canonical, metadata or structured-data issues;
- image/video/media problems;
- performance or loading problems;
- accessibility issues;
- duplicated/conflicting content;
- obsolete or suspicious repository structure;
- deployment/build problems;
- security/privacy risks;
- anything that may cause future breakage or confusion.

Mandatory behavior:

1. **REPORT IT TO THE OWNER** clearly, even when it is outside the current task.
2. **DO NOT silently expand the current scope** to fix it.
3. If the problem is not part of the current approved task, record it in **`ISSUE_LOG.md`** with evidence and a safe next step.
4. If it is critical or makes the current work unsafe, **STOP the affected work and inform the Owner immediately**.
5. If it is non-blocking, log it and continue only with the already approved task.
6. A discovered issue does **not** authorize a fix, merge, deployment, deletion, rename, or refactor.
7. Every fix still requires its own safe scope, branch/PR, QA, and explicit Owner **`merge`**.
8. Resolved issues stay in the log with the fixing PR/commit; they are not silently erased.

For every repository task, check **`ISSUE_LOG.md`** before making changes so known problems are not forgotten or reintroduced.

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

Current repository issue/backlog log: **ISSUE_LOG.md**  
Current authoritative cleanup policy: **CLEANUP_SAFETY_RULES.md**  
Current cleanup state/log: **CLEANUP_AUDIT.md**
