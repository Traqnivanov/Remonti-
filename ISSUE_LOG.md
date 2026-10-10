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

**Status:** RESOLVED  
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

- Fix approved by Owner: **YES**
- Branch: `fix/favicon-paths`
- PR: **#12**
- QA: **PASS**
- Owner merge approval: **YES**
- Merge commit: `1c512ea2ee64960bd78d5f07afcc60e7047a4435`
- GitHub Pages deploy run: **#625 — SUCCESS**
- Live verification: **PASS — the three icon URLs no longer return 404 after deployment**

---

## ISSUE-002 — Verify historical hreflang change against Search Console warning

**Status:** DISCOVERED  
**Category:** SEO / international targeting  
**Discovered during:** 2026-10-10 public search, source review, and Owner correction  
**Source main SHA:** `26c5c5a1149b08c8b98197d6982b399cf460f86e`

**Affected paths/pages:** `lom/index.html`, `en/lom/index.html`, `de/lom/index.html`, `sitemap.xml`

**Evidence / reproduction:** Current EN and DE HTML list bg, en, de, and x-default; current BG Lom HTML lists only bg and x-default. The sitemap provides language alternates for EN and DE URL entries but not BG Lom. Commit `9532438e33a22e7e4ad2a81e4fa47c961936fa58` deliberately removed the EN/DE alternates from BG Lom on 2026-08-07. The Owner states Google Search Console warned that the earlier setup was not okay. The exact warning and its target URLs have not yet been reviewed here. Sitemap EN/DE URLs omit the slash used by HTML canonical; live redirect behavior is unverified.

**Risk / impact:** The current mapping is asymmetric, but its actual impact and the reason for the historical Google warning are unknown. Do not call this an indexing or ranking defect without reviewing the warning and URL Inspection.

**Safe proposed next step:** Obtain the exact Search Console warning or screenshot and its affected URLs, then inspect those URLs in Search Console, including Google-selected canonical and index status. Compare the earlier and current configurations and determine whether any change is warranted. Do not restore the removed tags based only on this log.

**Current-task blocker:** NO

**Authorization / implementation:**
- Owner fix approval: NO
- Branch:
- PR:
- QA:
- Owner merge approval:
- Merge commit:
- Live verification:

---

## ISSUE-003 — Remote Lom contract lacks an outcome and exit test

**Status:** CONFIRMED  
**Category:** Product criteria / decision continuity  
**Discovered during:** 2026-10-10 Owner-requested audit of `REMOTE_LOM_PRODUCT_CONTRACT.md`  
**Source main SHA:** `07188e450a30effef877b78e34f32a1f837f8ba9`

**Affected paths/pages:** `REMOTE_LOM_PRODUCT_CONTRACT.md`, `START_HERE.md` handoff only. No production page is changed.

**Evidence / reproduction:** Section 3 lists six quality gates for proposals but does not define observable end success or how to decide that a direction is good enough to stop comparing. Section 7 calls for 2–3 mechanisms without a tie-break or exit rule. The current wording also prejudges a `план/артефакт`, an `единствено действие`, and a three-second threshold before the mechanism is chosen. It does not explicitly test whether a visitor without dates/access can use the experience, whether the existing Lom page would serve better than a new page, or whether the displayed workflow can be delivered in actual operations.

**Risk / impact:** A visually convincing concept could pass subjective criteria without helping a remote client make a real next decision. Repeated comparison of new mechanisms without an exit test can become a loop. A new page or tool might be built unnecessarily.

**Safe proposed next step:** Agree with Owner on a short outcome contract: the exact human decision enabled; truthful proof tied to the real workflow; two representative scenario tests plus failure/unknown states; explicit reason for a separate page versus the existing Lom page; and a bounded proceed/revise/stop decision. Keep proposed thresholds and wording OPEN until Owner decides. Do not treat this log as authorization to change the product contract or site.

**Current-task blocker:** YES for choosing/implementing the mechanism; NO for discussion and analysis.

**Authorization / implementation:**
- Owner fix approval: OPEN
- Branch:
- PR:
- QA:
- Owner merge approval:
- Merge commit:
- Live verification:

---

## ISSUE-004 — Payment and handover statements differ across Lom language pages

**Status:** DISCOVERED  
**Category:** Public content / cross-language operational consistency  
**Discovered during:** 2026-10-10 remote Lom mechanism research  
**Source main SHA:** `692c88acee13ee866c91fd11ffda251031ab61b1`

**Affected paths/pages:** `lom/index.html`, `en/lom/index.html`, `de/lom/index.html`

**Evidence / reproduction:** Public BG Lom FAQ says payment is when the client is satisfied, not before or midway; the BG process describes inspecting the completed property together. EN Lom says materials are paid upfront and labour in agreed stages or at stage completion, and says handover may happen by video call. DE FAQ likewise describes materials upfront and staged labour, with video-call handover. These may reflect different client arrangements, but that distinction is not explicit in the public wording. Public pages: https://ivanov-remonti.com/lom/ ; https://ivanov-remonti.com/en/lom/ ; https://ivanov-remonti.com/de/lom/ .

**Risk / impact:** A remote client may form a payment or presence expectation that differs from the actual agreement. A new remote-Lom experience must not repeat one version as a universal rule.

**Safe proposed next step:** Ask Owner which payment and handover arrangements are actually offered in each case, then audit the precise sentences and agree any separate content fix. Do not change the site or use unverified terms in the proposed mechanism.

**Current-task blocker:** NO for concept comparison; YES for final public wording that mentions payment or remote handover.

**Authorization / implementation:**
- Owner fix approval: OPEN
- Branch:
- PR:
- QA:
- Owner merge approval:
- Merge commit:
- Live verification:

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
