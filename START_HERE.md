# IVANOV REMONTI — START HERE

This repository is a live website repository. Safety takes priority over cleanup speed.

## GLOBAL RULE #1 — PRODUCTION CHANGES REQUIRE OWNER MERGE

This rule applies to all work that can affect the website, production behavior, public content, repository assets, deployment, or other important project behavior.

The following always require a safe branch/PR, relevant QA, and the Owner explicitly writing **`merge`** for that exact change set:

- HTML/CSS/JS or application code;
- page content or structure;
- images, video, media, favicons, logos or other assets;
- SEO, sitemap, canonical, metadata or structured data;
- links, routing, domains, redirects or deployment/build configuration;
- deletion, rename, move or replacement of repository files;
- performance, accessibility, security or privacy changes;
- any change that could alter what users, search engines, browsers, or production systems receive;
- any other change where impact is uncertain.

Approval of an idea, implementation, screenshot, preview, or task is not permission to merge a production-impacting change.

Before every production-impacting merge, verify the exact PR/head SHA, changed files, diff, relevant QA, current `main`, and absence of unrelated changes.

If any check fails or impact is uncertain: **DO NOT MERGE.**

### Documentation-only exception

A second Owner `merge` command is **not required** when all of the following are true:

1. the change is only internal repository documentation, rules, handoff notes, audit logs, or issue-log administration;
2. the underlying rule/decision was already explicitly discussed and approved by the Owner in chat;
3. no website page, runtime code, asset, SEO, config, build/deployment behavior, deletion, rename, or public output is changed;
4. the documentation change is checked to contain only the already-approved decision and no new product/technical decision.

Such documentation may be recorded and merged after verification without asking the Owner to approve the same rule a second time.

If there is any doubt whether a change is documentation-only or production-impacting, treat it as production-impacting and ask the Owner.

## GLOBAL RULE #2 — DISCOVERED PROBLEMS MUST BE REPORTED AND PERSISTED

This rule applies to **ALL work in this repository**.

If any chat, agent, tool, audit, test, or implementation discovers a meaningful problem of any kind, it must not be ignored, left only in chat memory, or silently fixed.

Problems include code, broken links, missing/wrong files, UI/mobile defects, SEO, media, performance, accessibility, duplicate/conflicting content, repository structure, deployment/build, security/privacy, or any other risk.

Mandatory behavior:

1. **REPORT THE PROBLEM TO THE OWNER IN CHAT** in clear, normal language.
2. For every confirmed or materially plausible problem that may require later work, **also record it in `ISSUE_LOG.md` automatically** with evidence, affected area, risk, and safe next step.
3. The Owner does **not** need to approve the act of logging a discovered problem. The log exists so important findings are not lost between chats.
4. **DO NOT fix it automatically** and do not silently expand the current task.
5. If the problem is critical and makes the current task unsafe, stop the affected work and report it immediately.
6. If it is non-blocking, report and log it, then continue only with the already-approved task unless the Owner changes the scope.
7. A logged issue is **not authorization to fix it**. Any production-impacting fix still requires its own safe scope, branch/PR, QA, and Owner `merge`.
8. Trivial, transient, or disproven observations do not need permanent log entries. If uncertain whether a finding is meaningful, prefer logging it as DISCOVERED rather than losing it.
9. Resolved issues remain in the log with the fixing PR/commit and verification result; they are not silently erased.

For repository work, check `ISSUE_LOG.md` before making changes so known problems are not forgotten or reintroduced.

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

## ACTIVE PRODUCT EXPLORATION — remote Lom clients

Read [`REMOTE_LOM_PRODUCT_CONTRACT.md`](REMOTE_LOM_PRODUCT_CONTRACT.md) when working on the experience for people from Lom who live elsewhere and return briefly. It contains the Owner-confirmed audience and order of presentation, the six review criteria, open hypotheses, decision log, and the exact NEXT. This is a **working contract**, not approval for a new page, site change, sitemap edit, or prototype implementation.

**Current checkpoint (10.10.2026):** Owner's recognition test: a remote Lom client sees a concrete solution in action before a choice, request, or data entry and reaches their own conclusion, „Да, това точно търсех“. This phrase is an internal product test, not public copy or permission for pressure. The first standalone prototype asks questions first and is not approved. The mechanism and separate-page decision remain OPEN.

**Next:** Compare two or three candidate mechanisms for showing a useful result before input. Apply the criteria, including the non-advertising voice gate, and natural-uniqueness test from the working contract, discuss one point at a time with the Owner, then replace its current checkpoint when a decision is made. Do not restart the GSC audit or assume the v0 prototype is the chosen direction.
