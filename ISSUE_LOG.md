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

## ISSUE-005 — Latest published diary card used work date

**Status:** RESOLVED IN DRAFT, NOT MERGED  
**Category:** Prototype / client chronology  
**Discovered during:** 2026-10-21 role test of Draft PR #26  
**Source main SHA:** Not applicable; prototype branch head before fix `91748b8505728fc98ee3c778e721fa0fa6deb2a8`

**Affected paths/pages:** `prototypes/property-diary-lab.html` in Draft PR #26.

**Evidence / reproduction:** The client card "Последно публикувано" selected `entries[0]`, while `entries` was sorted by `workDate`. Publishing an older work day after a newer work day made the card show the wrong record.

**Risk / impact:** A client checking the diary could miss the newest publication.

**Safe proposed next step:** The card now selects by `publishedAt`; the history remains by `workDate`. Recheck this case in a browser with IndexedDB and on a phone before any real service.

**Current-task blocker:** NO for Draft review; YES for claiming full end-to-end QA.

**Authorization / implementation:**
- Owner fix approval: "ok raboti" in current chat
- Branch: `prototype/property-diary-lab-v1`
- PR: #26 (Draft)
- QA: syntax, reversed work/publication date comparator, and interactive backdated publication test passed; history remains by work date
- Owner merge approval: NO
- Merge commit: none
- Live verification: not applicable

---

## ISSUE-006 — False IndexedDB diagnosis during first-open test

**Status:** DISPROVEN; corrected on 2026-10-21  
**Category:** QA interpretation  
**Discovered during:** 2026-10-21 direct preview test  
**Source main SHA:** Not applicable; Draft PR #26

**Affected paths/pages:** `prototypes/property-diary-lab.html` preview on raw.githack.

**Evidence / reproduction:** The page originally displayed a storage error. A restricted read-only browser evaluation reported `typeof indexedDB === "undefined"`, but this was not evidence of the page's own storage capability. After fixing the clean-start render error, the test object, published entries, and test image persisted through reload and across the next commit URL on the same origin.

**Risk / impact:** The initial diagnosis incorrectly attributed a prototype code defect to the browser environment. The claim must not be repeated in handoff or user-facing QA.

**Safe proposed next step:** Treat the storage error as a prior symptom of ISSUE-007. Confirm fallback separately only in a controlled browser that truly disables storage.

**Current-task blocker:** NO

**Authorization / implementation:**
- Owner fix approval: "ok raboti" for current prototype task
- Branch: `prototype/property-diary-lab-v1`
- PR: #26 (Draft)
- QA: test records and photo survived reload
- Owner merge approval: NO
- Merge commit: none
- Live verification: not applicable

---

## ISSUE-007 — Clean first-open render error misreported as storage failure

**Status:** RESOLVED IN DRAFT, NOT MERGED  
**Category:** Prototype / initial state and error handling  
**Discovered during:** 2026-10-21 test following Owner screenshot  
**Source main SHA:** Not applicable; Draft PR #26 head before fix `cda52d3d7963abcb8524f934ca950749c27a0f1a`

**Affected paths/pages:** `prototypes/property-diary-lab.html` in Draft PR #26.

**Evidence / reproduction:** When `state.recent=null` and there is no selected project, optional equality of two undefined IDs evaluated true in `showFields()`, then the code read `state.recent.roomId` and threw. The same risk existed in `showScopes()`. The broad initialization `catch` showed "browser cannot save" and disabled controls, making the actual defect look like a storage failure.

**Risk / impact:** A new tester cannot create the first project and may believe their browser is incompatible.

**Safe proposed next step:** Both recent-selection expressions require a real project, room, and recent state. The storage `try/catch` now covers only database open/read. The fallback, if needed, explicitly labels entries as temporary; normal storage explicitly labels browser-only storage. Do not use real client data.

**Current-task blocker:** NO for Draft review; YES for real service until authentication and server persistence exist.

**Authorization / implementation:**
- Owner fix approval: "ok raboti" for prototype and screenshot steering
- Branch: `prototype/property-diary-lab-v1`
- PR: #26 (Draft)
- QA: clean start, project/room/work, hidden draft, publish, photo, reload persistence, backdated publication card passed in browser
- Owner merge approval: NO
- Merge commit: none
- Live verification: not applicable

---

## ISSUE-008 — Published work may lack a named activity

**Status:** RESOLVED IN DRAFT, NOT MERGED  
**Category:** Property diary / scope versus performed action  
**Discovered during:** 2026-10-21 Owner screenshot review  
**Source main SHA:** Not applicable; Draft PR #26 head `93eb16e262b16f6e174d531f358317080f79657d`

**Affected paths/pages:** `prototypes/property-diary-lab.html` and diary working model in Draft PR #26.

**Evidence / reproduction:** Owner created a test project and a bedroom, published a progress entry with date, action and image, while the room showed "Няма добавена работа". The current publish check requires a selected agreed work only when the room already has at least one. The published entry is therefore titled generically "Извършена работа" and has no named work/phase. Screenshot provided in chat; the existing flow matches source behavior.

**Risk / impact:** The client can see that something happened but not the work or phase it belongs to. A bare action could also be mistaken for confirmation that a newly found or additional activity was already agreed.

**Safe proposed next step:** Review a model that keeps the agreed scope distinct from an actual performed activity. For a progress publication, require a clear activity name even if no agreed scope exists; allow an optional link to the agreed scope. A change of scope stays a separate in-person/phone discussion, not an online approval. Test this against a short first record and a newly discovered activity before changing the Draft UI. Owner approved a richer assignment hierarchy in chat: source of the current scope (contract and appendix, accepted offer, or agreed assignment), room, point, subpoint, and linked diary record. The Draft implementation requires a selected point for published progress; issue records remain separate and do not imply online consent.

**Current-task blocker:** YES for WORK acceptance of this record structure; NO for continued prototype discussion.

**Authorization / implementation:**
- Owner fix approval: `ok raboti` for the reviewed assignment-by-room prototype
- Branch: `prototype/property-diary-lab-v1`
- PR: #26 (Draft)
- QA: browser check of two-room sample, client room filter, dated supplement, new subpoint attached to supplement, draft linked to that subpoint; JavaScript syntax. Separate phone visual QA and real client authentication remain open.
- Owner merge approval: NO
- Merge commit: none
- Live verification: not applicable

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
