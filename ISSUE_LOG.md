# IVANOV REMONTI — REPOSITORY ISSUE LOG

**Status: MANDATORY CONTINUITY LOG**  
**Repository: `Traqnivanov/Remonti-`**

This file records meaningful problems discovered during any repository work so they are not forgotten between chats, silently repaired, mixed into unrelated PRs, or rediscovered from scratch.

## Rules

- Discover a meaningful problem → report it to the Owner in chat.
- Confirmed or materially plausible problems that may require later work are also recorded here automatically.
- The Owner does not need to approve the act of logging a discovered problem.
- A log entry is **not permission to fix**.
- Do not silently expand the current task to repair a logged issue.
- Production-impacting fixes require their own safe scope, branch/PR, QA, and Owner `merge`.
- Critical problems may stop affected work immediately and must be reported.
- Trivial, transient, or disproven observations do not need permanent entries.
- If uncertainty remains and the finding could matter later, prefer a `DISCOVERED` entry instead of losing it.
- Resolved issues remain in the log with the fixing PR/commit and verification result.

## Status values

- **DISCOVERED** — plausible finding; more verification may be needed.
- **CONFIRMED** — verified with evidence.
- **PLANNED** — Owner approved a future fix direction.
- **IN_PROGRESS** — isolated safe branch/PR exists.
- **BLOCKED** — cannot proceed safely yet.
- **RESOLVED** — fixed, merged, and verified.
- **KEEP / NO ACTION** — reviewed and intentionally left unchanged.

---

## ISSUE-001 — Favicon / touch-icon filename mismatch

**Status:** CONFIRMED  
**Category:** Repository integrity / browser icons  
**Discovered during:** cleanup read-only audit  
**Source main SHA:** `212835307e60cbd205d516c8bc5d331189dcbf23`

### Evidence

Active HTML pages reference these root paths:

- `/favicon-32.png`
- `/favicon-192.png`
- `/apple-touch-icon.png`

Those exact paths do not exist in the current repository tree.

The repository contains:

- `favicon-32(1).png` — 1,428 bytes
- `favicon-192(1).png` — 25,974 bytes
- `apple-touch-icon(1).png` — 23,008 bytes

All three `(1)` files were added together in commit:

`7af263ee70103f53c34a2a2098eea20a31328110` — 2026-08-04.

### Risk

Browsers/pages may request icon paths that are absent from the repository.

### Safe proposed fix

Do not rename/delete the existing `(1)` files first.

In a separate safe branch:

1. create exact copies at the expected filenames without `(1)`;
2. keep the existing aliases during initial repair;
3. verify affected pages/icon requests;
4. only after successful QA consider old aliases for a separate cleanup review.

### Authorization / implementation

- Fix approved by Owner: **NO**
- Branch: **NONE**
- PR: **NONE**
- Merge authorization: **NONE**
- Live change: **NONE**

---

## New issue template

### ISSUE-XXX — Short title

**Status:** DISCOVERED  
**Category:**  
**Discovered during:**  
**Source main SHA:**  

**Affected paths/pages:**  

**Evidence / reproduction:**  

**Risk / impact:**  

**Safe proposed next step:**  

**Current-task blocker:** YES / NO

**Authorization / implementation:**
- Owner fix approval:
- Branch:
- PR:
- QA:
- Owner merge approval:
- Merge commit:
- Live verification:
