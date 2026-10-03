# IVANOV REMONTI — CLEANUP AUDIT LOG

**Policy:** `CLEANUP_SAFETY_RULES.md`

## Current status

- Cleanup mode: **READ-ONLY AUDIT ONLY**
- Files approved for deletion: **NONE**
- Deletion batches merged: **NONE**
- History rewrite: **PROHIBITED**
- Direct `main` cleanup changes: **PROHIBITED**
- Owner approval required before any deletion: **YES**
- Owner approval required again before merge: **YES**
- Global live/main safety gate: **MANDATORY FOR ALL REPO WORK**
- Exact Owner command `merge` required for the exact current PR/change set: **YES**
- Pre-merge head/file/diff/QA re-check required: **YES**
- Auto-merge: **PROHIBITED**

## Baseline

Baseline `main` SHA before cleanup protocol work:

`813a3bd0cc446fbd88ba844d87e816700a2cc04a`

This is a reference checkpoint only. Before the first actual deletion batch, the then-current `main` SHA must be recorded again and a pre-cleanup safety branch/tag must be created as required by the policy.

## Audit classifications

Allowed statuses:

- ACTIVE
- PROTECTED
- UNKNOWN
- POSSIBLE_DUPLICATE
- CANDIDATE
- OWNER_APPROVED_DELETE

No file may be deleted unless its final status is **OWNER_APPROVED_DELETE**.

## Cleanup batches

No cleanup deletion batch has been approved or executed yet.

Future batches must record:

- batch number;
- source `main` SHA;
- safety branch;
- Draft PR;
- exact approved paths;
- evidence summary;
- QA result;
- Owner deletion approval;
- Owner merge approval;
- merge commit;
- live QA result;
- rollback/revert information if needed.

## Read-only audit checkpoint — 2026-10-03

Source `main` SHA audited:

`813a3bd0cc446fbd88ba844d87e816700a2cc04a`

### Inventory

- Total files: **249**
- Total current-tree bytes: **23,054,631**
- HTML: **27**
- WebP: **115**
- JPG: **99**
- PNG: **4**
- TXT: **1**
- XML: **1**
- Other/no-extension: **2**

### Current classification

- **ACTIVE:** 123
- **PROTECTED:** 32
- **POSSIBLE_DUPLICATE:** 65
- **UNKNOWN:** 29
- **CANDIDATE:** 0
- **OWNER_APPROVED_DELETE:** 0

No file is authorized for deletion.

### Important findings

1. Exact byte-duplicate analysis found **10 duplicate blob groups** totaling about **917 KB** of theoretical duplicate bytes. This does **not** mean those files are safe to delete; several duplicate paths are independently referenced by active pages.
2. The unusual root path `довършителни ремонти София"` is referenced by active HTML and shares exact bytes with other image files. It is **not** junk and must not be deleted casually.
3. `IMG_20230322_094845.jpg`, `IMG_20230322_094845-480.webp`, and `IMG_20230322_094845-800.webp` form an intentional source/responsive family. The JPG was deleted/re-added in July and the WebP variants were added together in August. Treat as **PROTECTED/KEEP** until a separate exact decision.
4. `portret.jpg` was added during the same work window as the About/`za-men` page changes. Treat as **PROTECTED/KEEP** despite no current direct text reference.
5. Two `.jpg` paths — `samorazlivna-zamazka-pod-sofia-01.jpg` and `tsyalosten-remont-sofia-01.jpg` — currently contain only CRLF (2 bytes) and are not valid image data. Because they represent previously intended named assets and save essentially no space, they remain **UNKNOWN/KEEP** for now rather than being deleted.
6. Several Viber-named files are survivors from a large April upload/rename sequence. Some are exact duplicates of later semantic filenames; others are unique. They remain **UNKNOWN** or **POSSIBLE_DUPLICATE** until source/visual equivalence is proven.
7. Clear exact-byte relationships include:
   - `viber_изображение_2026-04-18_16-23-58-986.jpg` = `ivanov-remonti-logo-stroitelni-uslugi-sofia.jpg` = `довършителни ремонти София"`
   - `shpaklovka-vurhu-gipsokarton-sofia.jpg` = `shpaklovka-steni-apartament-sofia.jpg`
   - `shpaklovka-boyadisvane-gipsokarton-sofia-01.jpg – Копие.jpg` = `shpaklovka-boyadisvane-gipsokarton-sofia-08.jpg`
   - `casa-própria-1024x712-01.jpg` = `viber_изображение_2026-04-18_16-29-13-789.jpg`
8. Even where exact bytes are duplicated, **no delete is approved**. Internal references, external-link risk, source-master value, and rollback value must still be evaluated.

### Next safe step

Continue read-only analysis of the remaining **UNKNOWN** and **POSSIBLE_DUPLICATE** groups. Prioritize proving whether unreferenced duplicates have an actively referenced identical copy and whether unique old assets are source masters.

No delete branch, deletion PR, or merge is authorized.
