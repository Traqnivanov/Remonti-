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

## Read-only audit checkpoint 2 — source families, HTML, exact duplicates

### Source/master protection

The current tree contains **65 image families** where a JPG original exists together with one or more WebP/responsive variants. There are **65 JPG originals** in those families totaling **8,943,771 bytes**.

Under the safety policy these JPG originals are **source/master material and are PROTECTED by default**. Their size is not a reason to delete them.

This means a large part of the apparent repository "duplication" is intentional source + delivery-format storage, not cleanup garbage.

### HTML / sitemap audit

- HTML files in repository: **27**
- URLs in `sitemap.xml`: **24**
- Sitemap-mapped content pages: **24**
- HTML files outside sitemap:
  - `404.html` — expected infrastructure page; PROTECTED
  - `thanks.html` — conversion/thank-you page and referenced from active site flow; PROTECTED/ACTIVE
  - `bot.html` — standalone TeryBot assistant, canonical `https://ivanov-remonti.com/bot.html`, explicitly `noindex`; treat as dormant functional application and PROTECTED, not junk

### Exact-byte duplicate reference audit

The duplicate groups were checked against all repository text pages in two batches.

Confirmed examples:

- `ivanov-remonti-logo-stroitelni-uslugi-sofia.jpg` is referenced by active About pages.
- `довършителни ремонти София"` is referenced by active pages.
- `viber_изображение_2026-04-18_16-23-58-986.jpg` has the same bytes as those logo-related files but no direct internal reference found. It remains **POSSIBLE_DUPLICATE / KEEP** pending final source/external-link review.
- `shpaklovka-steni-apartament-sofia.jpg` is directly referenced by `montana/index.html`.
- `shpaklovka-vurhu-gipsokarton-sofia.jpg` has identical bytes but no direct internal reference found. It remains **POSSIBLE_DUPLICATE / KEEP** pending final review.
- The two exact 800px duplicates `dekorativna-pqsachna-mazilka-01-800.webp` and `dekorativna-pqsachna-mazilka-sofia-01-800.webp` are both used under different active paths; neither may be deleted.
- The exact 800px duplicates `gipsokarton-tavan-shpaklovka-lateks-cena-trud-sofia-800.webp` and `oferta-boyadisvane-lateks-kvadraten-metar-lom-800.webp` are both actively referenced; neither may be deleted.
- Their corresponding 480px `gipsokarton...` and `oferta...` variants are also actively referenced.
- Two 480px decorative-plaster duplicate paths currently have no direct internal exact-string reference. They remain **POSSIBLE_DUPLICATE / KEEP** until dynamic-path/source review is complete.
- No evidence of a generic runtime `-800` → `-480` filename-construction rule was found in repository code search, but absence of such a search result alone is not deletion proof.

### Safety conclusion

No deletion has been authorized. No cleanup mutation has been made.

The audit is reducing false-positive "junk" aggressively: active aliases, source JPGs, responsive variants, dormant functional pages, and unusual but referenced paths are being protected rather than removed.

## Candidate review batch A — evidence complete, NO deletion authorized

The following paths have passed the current read-only evidence checks strongly enough to be labeled **CANDIDATE**. This status does **not** authorize deletion.

### A1 — `viber_изображение_2026-04-18_16-23-58-986.jpg`
- Size: 127,871 bytes
- Exact blob SHA: `ba31d1bb443dbf88d35034f8052da694f56a006e`
- Exact-byte duplicates currently in repository:
  - `ivanov-remonti-logo-stroitelni-uslugi-sofia.jpg`
  - `довършителни ремонти София"`
- The semantic logo path is actively referenced by About pages; the unusual quoted path is also actively referenced.
- No current internal text reference to the Viber-named path was found.
- Git history shows the same content was renamed from the Viber filename to `ivanov-remonti-sofia-logo.jpg`, then to the semantic logo filename.
- Exact filename/direct-site public search returned no indexed result.
- Classification: **CANDIDATE**, pending Owner approval only.

### A2 — `shpaklovka-vurhu-gipsokarton-sofia.jpg`
- Size: 113,390 bytes
- Exact blob SHA: `5992d25def65beccc4ea82061a12f66527c44af0`
- Exact-byte duplicate: `shpaklovka-steni-apartament-sofia.jpg`
- `shpaklovka-steni-apartament-sofia.jpg` is referenced by `montana/index.html` and belongs to an active JPG/WebP family.
- No current internal text reference to `shpaklovka-vurhu-gipsokarton-sofia.jpg` was found.
- Exact filename/direct-site public search returned no indexed result.
- Classification: **CANDIDATE**, pending Owner approval only.

### A3 — `shpaklovka-boyadisvane-gipsokarton-sofia-01.jpg – Копие.jpg`
- Size: 125,444 bytes
- Exact blob SHA: `29cac141d7280984d6a5c7c4d07cbeaa52eb3aa7`
- Exact-byte duplicate: `shpaklovka-boyadisvane-gipsokarton-sofia-08.jpg`
- The `...-08` family has active 480/800 WebP variants used by site pages.
- The filename itself explicitly contains `Копие`.
- No current internal text reference to the copy path was found.
- Exact filename/direct-site public search returned no indexed result.
- Classification: **CANDIDATE**, pending Owner approval only.

### A4 — `samorazlivna-zamazka-pod-sofia-01.jpg`
- Size: 2 bytes
- Blob content is only CRLF; it is not valid image data.
- Exact duplicate of `tsyalosten-remont-sofia-01.jpg`.
- No current internal text reference was found.
- Exact filename/direct-site public search returned no indexed result.
- Classification: **CANDIDATE**, pending Owner approval only.

### A5 — `tsyalosten-remont-sofia-01.jpg`
- Size: 2 bytes
- Blob content is only CRLF; it is not valid image data.
- Exact duplicate of `samorazlivna-zamazka-pod-sofia-01.jpg`.
- No current internal text reference was found.
- Exact filename/direct-site public search returned no indexed result.
- Classification: **CANDIDATE**, pending Owner approval only.

### Candidate batch A safety status

- Candidate count: **5**
- Files deleted: **0**
- Owner deletion approval: **NOT YET GIVEN**
- Delete branch: **NOT CREATED**
- Delete PR: **NOT CREATED**
- Live change: **NONE**

Under the policy, these files must remain untouched until the Owner explicitly approves these exact paths as a deletion batch.
