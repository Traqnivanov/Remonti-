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

**Evidence / reproduction:** Current EN and DE HTML list bg, en, de, and x-default; current BG Lom HTML lists only bg and x-default. The sitemap provides language alternates for EN and DE URL entries but not BG Lom. Commit `9532438e33a22e7e4ad2a81e4fa47c961936fa58` deliberately removed the EN/DE alternates from BG Lom on 2026-08-07. The Owner states Google Search Console warned that the earlier setup was not okay. The exact warning and its target URLs have not yet been reviewed here. Sitemap EN/DE URLs omit the slash used by HTML canonical; the slashless EN URL is listed as discovered but not indexed in Search Console, while the slash versions have search impressions and clicks. Public URL checks observed redirects from slashless EN and DE URLs to their slash versions. The historical Google warning itself remains unverified.

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

## ISSUE-003 — Montana has no verified incoming HTML navigation link

**Status:** CONFIRMED  
**Category:** SEO / internal navigation  
**Discovered during:** 2026-10-10 Search Console links export and repository review

**Affected paths/pages:** `index.html`, `lom/index.html`, `montana/index.html`

**Evidence / reproduction:** Search Console reports 55 internal links across its listed target pages, but `/montana/` is absent from its complete internal target export. Source inspection finds no `montana` reference in the Sofia root or Lom landing HTML; the Montana page points to itself. This does not prove there are no incoming links anywhere in the repository, but the checked primary entry points do not link to it.

**Risk / impact:** Visitors and crawlers may have difficulty navigating to the Montana page; the page is nevertheless indexed and has impressions and clicks.

**Safe proposed next step:** Audit all navigational entry points, then propose one useful, visible contextual link to Montana where it matches the actual service area. Review mobile navigation and avoid misleading cross-city claims.

**Current-task blocker:** NO

**Authorization / implementation:** No production fix authorized; no code changed.

---

## ISSUE-004 — Conflicting business identity in Montana structured data

**Status:** CONFIRMED  
**Category:** SEO / structured data  
**Discovered during:** 2026-10-10 repository review

**Affected paths/pages:** `montana/index.html`

**Evidence / reproduction:** The first JSON-LD business entity uses `@id: https://ivanov-remonti.com/lom/#business` while its `url` is the Montana page. A second JSON-LD `HomeAndConstructionBusiness` entity on the same page uses `@id: https://ivanov-remonti.com/montana#ivanov-remonti`. The two entities also list different telephone numbers. The first entity uses a Lom address, which may be intentional; the identity and telephone mismatch need an Owner check before correction.

**Risk / impact:** Search systems may receive inconsistent identity/contact signals from the Montana page. No Search Console structured-data error has been established for this issue.

**Safe proposed next step:** Verify which phone and business address are intended for Montana, review the two JSON-LD blocks and Google-visible output, then prepare a separate scoped fix only if required.

**Current-task blocker:** NO

**Authorization / implementation:** No production fix authorized; no code changed.

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
