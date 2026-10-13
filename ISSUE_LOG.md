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

## ISSUE-005 — Remote Lom first-screen draft still reads as a generic process

**Status:** CONFIRMED  
**Category:** Product concept / proof of useful mechanism  
**Discovered during:** 2026-10-11 scenario review of `REMOTE_LOM_FIRST_SCREEN_V1.md`  

**Affected paths/pages:** Draft documentation in PR #24 only. No production page changed.

**Evidence / reproduction:** The revised first screen shows an illustrative decision about wall preparation after inspection, but still only as a text scheme. It does not show the actual usable output sent to an absent owner. A visitor without access reaches that path only after the main example. The existing Lom page already explains inspection, detailed offer, and photo/video reporting. Independent six-criteria assessment in `REMOTE_LOM_FIRST_SCREEN_V1.md` finds natural uniqueness not met and other criteria partial.

**Follow-up 12.10.2026:** The Owner-selected single-screen prototype in Draft PR #25 improves recognition and the order of information, but the first card still contains a photo placeholder and generic „Подготвена основа“. The later „Нужно решение“ state describes an unspecified discovered area. The six-criteria review in `REMOTE_LOM_FIRST_SCREEN_AUDIT.md` therefore keeps „Какво вижда“ and natural uniqueness as NOT PASSED for public use. This is the same unresolved proof gap, not a new independent issue.\n\n**Risk / impact:** Calling the draft a finished instrument could lead to a new page that is essentially a reformatted FAQ and misses the Owner's recognition criterion.

**Safe proposed next step:** Confirm the actual follow-up message or artifact after an inspection, then show a clearly marked example with established facts, unresolved items, and the owner's real decision from afar. Test both access scenarios with target users and compare it against the current Lom page and a short phone explanation. Do not implement or publish the present version.

**Current-task blocker:** YES for implementation; NO for concept refinement.

**Authorization / implementation:** Not approved; no production changes.

---

## ISSUE-006 — Remote-update cadence and photo estimate claims need verification

**Status:** DISCOVERED  
**Category:** Public content / remote-work operational consistency  
**Discovered during:** 2026-10-12 global remote renovation research  

**Affected paths/pages:** `lom/index.html`, `en/lom/index.html`, potentially `de/lom/index.html` and any proposed remote-Lom experience. No production page has been changed.

**Evidence / reproduction:** The live Bulgarian Lom page says photo/video reports are sent at each stage of work. The English Lom page promises daily photos and videos, and its footer invites photos on WhatsApp with an estimated price within 24 hours. The English page also describes live video inspection or a detailed photo report, and a video-call handover; the BG page describes inspecting the completed work together. Sources: https://ivanov-remonti.com/lom/ and https://ivanov-remonti.com/en/lom/ (reviewed 2026-10-12). ISSUE-004 already records the payment/handover difference; this new issue focuses on update cadence and estimate-before-inspection.

**Risk / impact:** A visitor may interpret a fixed daily-update service or a reliable quote from photos as guaranteed, while the Bulgarian process and the new concept rely on an on-site inspection and stage-based reporting. Trust would weaken if the actual operating model differs from public promises. Do not call the EN statements false without asking Owner how they are delivered in practice.

**Safe proposed next step:** Owner confirms (a) whether progress is reported daily or at defined stages, (b) what can be estimated from photos within 24 hours and how it is distinguished from a binding offer, and (c) whether remote video inspection and handover are actually available under agreed conditions. Then audit the exact public sentences and agree any separate content fix. The proposed new experience must not repeat unverified cadence, price or handover terms.

**Current-task blocker:** YES for final public wording on reporting/remote handover/price; NO for research and a conditional prototype.

**Authorization / implementation:** No fix approved; no production changes.

---

## ISSUE-007 — Hero counters expose zero before animation

**Status:** DISCOVERED  
**Category:** First impression / content reliability  
**Discovered during:** 2026-10-12 first-screen audit

**Affected paths/pages:** `lom/index.html` hero (check other language/city pages separately if a fix is scoped).

**Evidence / reproduction:** In `main` `lom/index.html` lines 649–650, the visible HTML starts at `0 Доволни клиенти` and `0 Години опит`, with `data-target=250` and `data-target=23`. A later IntersectionObserver at approximately lines 1291–1296 starts the count animation only when `.hero-stats` intersects. The public text extraction currently shows the zeros. No live mobile screenshot or no-JS rendering was obtained in this audit.

**Risk / impact:** A visitor or renderer may see misleading zero experience/customer counts before JavaScript runs, if it fails, or before the lower hero area intersects. This is a first-impression trust risk, not evidence that Google ranks the page lower.

**Safe proposed next step:** Reproduce on a real phone at slow load and with scripts off; verify the factual targets with Owner. In a separate scoped fix, render the true verified value as initial HTML and use animation only as optional presentation. Do not silently roll this into the remote diary launch.

**Current-task blocker:** NO for concept audit; YES if the final first-screen design retains those counters without verification.

**Authorization / implementation:** Not approved; no production changes.

---

## ISSUE-008 — Трите отговора може да слизат под първия мобилен екран

**Status:** DISCOVERED  
**Category:** Prototype / mobile first impression  
**Discovered during:** 2026-10-13 review of Draft PR #25

**Affected paths/pages:** `prototypes/lom-first-screen-review.html` only. No production page changed.

**Evidence / reproduction:** Commit `573cfb11dc62c1646f80a45084b98a106aacb57e` moves the three answers before the image, confirmed by the loaded DOM and interactive browser. At widths below 760 px the layout becomes a single column, with the review banner, navigation, eyebrow, multi-line H1 and subline all preceding the example card. Thus on a short phone screen the third answer may remain below the initial viewport. The available browser showed the desktop layout but did not provide a permitted 360/390/412 px visual viewport; this is a risk, not a reproduced visual defect.

**Follow-up 13.10.2026:** Owner sent three phone screenshots of the older prototype: without scrolling the headline and start of the sample card are visible, while the photo precedes the three answers; later screenshots show the answers below. The current prototype already puts answers before the photo. Commit `5705afb47bf165df0ccdf6029ee3ebd97f6b025f` also shortens duplicate card labels and spacing. The new compact version still needs its own phone screenshot; do not transfer the old screenshot result to the new version.\n\n**Follow-up 13.10.2026, 23:55 Sofia:** Owner provided a phone screenshot of the pinned compact version (commit `5705afb47bf165df0ccdf6029ee3ebd97f6b025f`). In this actual mobile viewport, the headline, explanation, all three answers in the intended order, photo and disclosure caption appear without scrolling. This resolves the first-screen fold concern for the observed device. It does not test other viewport sizes, the exception interaction, comprehension by an unprompted visitor, or operational truth of the illustrative example.

**Risk / impact:** The observed phone layout supports the five-second visual order; cross-device and product comprehension remain unverified. Do not treat this screenshot as full mobile or public-release approval.

**Safe proposed next step:** Continue the prototype's next structural layer and check the exception interaction and two client scenarios. Review other viewport sizes when a permitted device is available. Keep this within Draft PR #25; no live page edits.

**Current-task blocker:** YES for final mobile approval or production proposal; NO for continued prototype work.

**Authorization / implementation:** Observed-device first-screen visual order PASS; wider mobile/product QA pending; no production change.

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
