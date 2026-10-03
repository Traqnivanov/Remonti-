# IVANOV REMONTI — REPOSITORY CLEANUP SAFETY RULES

**Status: MANDATORY / OWNER SAFETY POLICY**  
**Repository: `Traqnivanov/Remonti-`**

## 1. Core principle

The cleanup objective is secondary to site integrity.

> It is acceptable to keep 100 unnecessary files. It is NOT acceptable to delete 1 file that is still needed.

Therefore:

- Default decision = **KEEP**.
- Any uncertainty = **KEEP / REVIEW**, never delete.
- "Looks old", "looks duplicated", "ugly filename", "not seen on one page", or "there is a WebP version" are **never sufficient reasons to delete**.
- No cleanup action may depend on visual guesswork alone.

## 2. Absolute prohibitions

During repository cleanup, the following are prohibited unless the Owner gives separate, explicit approval for that exact action:

- direct delete/change on `main`;
- mass deletion;
- rename or move mixed together with deletion;
- deleting files only because their names look obsolete;
- deleting originals only because optimized files exist;
- deleting a file because a simple text search returned zero results;
- deleting branches/tags as part of content cleanup;
- rewriting Git history;
- `git filter-repo`, BFG, force-push, orphan-history rebuilds, destructive rebase, or similar history surgery;
- deleting production files to reduce repository size without proving they are unused;
- automatic merge or automatic approval.

## 3. Cleanup phases — must happen in this order

### Phase A — READ-ONLY INVENTORY

Create a complete inventory of the current `main` tree.

No files are changed.

For each file collect, where applicable:

- exact path;
- filename and extension;
- size;
- blob SHA;
- category: HTML / CSS / JS / image / SEO / config / document / other;
- possible variants or duplicates;
- known references;
- notes about uncertainty.

### Phase B — DEPENDENCY AUDIT

A file cannot become a deletion candidate until references are checked across the whole current repository.

The audit must check at minimum:

- HTML `src`, `href`, `srcset`, `poster`, preload and link tags;
- inline CSS and stylesheet `url(...)`;
- JavaScript strings, arrays, objects, template literals and dynamically built paths;
- lightboxes, hidden galleries, modals and service-card data;
- JSON-LD / Schema.org;
- Open Graph and Twitter metadata;
- canonical/SEO-related image references;
- favicon and touch-icon references;
- sitemap, robots, 404, CNAME and other site infrastructure;
- Bulgarian, English and German pages;
- Sofia, Lom and Montana sections;
- root-level and nested relative paths;
- absolute URLs using both `ivanov-remonti.com` and `traqnivanov.github.io/Remonti-`;
- URL-encoded filenames, spaces, Unicode names and case differences;
- responsive image families such as original / 480 / 800 variants;
- code that constructs filenames or URLs dynamically.

**A zero-result simple search is NOT proof of safety.**

### Phase C — CLASSIFICATION

Every audited file must receive exactly one status:

- **ACTIVE** — confirmed used. Never delete.
- **PROTECTED** — infrastructure, SEO, brand, source, or otherwise sensitive. Keep unless separately proven and approved.
- **UNKNOWN** — purpose or dependency is not fully proven. Keep.
- **POSSIBLE_DUPLICATE** — may duplicate another asset, but not safe to delete yet.
- **CANDIDATE** — no dependency found after full audit, but still not approved for deletion.
- **OWNER_APPROVED_DELETE** — exact path explicitly approved by Owner after evidence review.

Only **OWNER_APPROVED_DELETE** may be removed.

## 4. Extra protection for images and media

Before an image/media file can become `CANDIDATE`:

1. Open/inspect the asset when technically possible.
2. Identify what it visually contains.
3. Check whether it is a source/original for a WebP, 480px, 800px, thumbnail, OG image, service card, gallery item, or future regeneration source.
4. Check exact filename and all known variants.
5. Check all city/language pages and service pages.
6. If the file could plausibly be a source master or externally linked asset, classify as **PROTECTED** or **UNKNOWN**, not delete.

A JPG and a WebP showing the same photo are not automatically duplicates for deletion purposes.

## 5. Protected-by-default items

The following are **PROTECTED by default** until a separate exact audit proves otherwise:

- `CNAME`;
- `robots.txt`;
- sitemap files;
- `404.html`;
- favicons and touch icons;
- logos and brand assets;
- analytics/tracker/consent-related code or assets;
- Open Graph / social preview assets;
- files referenced from JSON-LD or other structured data;
- language versions;
- service pages;
- hidden/lightbox/gallery assets;
- files with unclear or unusual names;
- originals that may be source material for optimized assets;
- any file referenced by any active page or runtime code.

## 6. Owner approval gate — before deletion

Before deleting even one file, present the Owner with the exact candidate list.

For every proposed file show:

- exact path;
- size;
- what it appears to be;
- why it is considered unused;
- all checks performed;
- related/variant files;
- risk or uncertainty;
- recommendation: KEEP or candidate for deletion.

The Owner must explicitly approve the exact deletion batch.

General phrases such as "clean it", "remove junk", or "delete unused files" do **not** authorize an unshown batch.

## 7. Backup checkpoint before the first delete

Before the first deletion batch of a cleanup campaign:

- record the exact `main` SHA in `CLEANUP_AUDIT.md`;
- create a pre-cleanup safety branch or tag pointing to that SHA;
- do not rewrite that history;
- keep the checkpoint until cleanup is completed and live QA is accepted.

This safety pointer does not duplicate repository file contents; it preserves an easy rollback checkpoint.

## 8. Deletion batch limits

Deletion work must be deliberately small.

- Maximum: **5 files per deletion PR**.
- High-risk files: **1 at a time**.
- One cleanup purpose per PR.
- No unrelated design/content/code changes in a deletion PR.
- No rename/move bundled with deletion.
- If more than 5 files are candidates, create additional batches only after the previous batch is verified.

## 9. Branch and PR rules

Every cleanup mutation must:

1. start from the current verified `main`;
2. use a new dedicated safety branch;
3. use a Draft PR;
4. never modify production directly;
5. show an exact compare against `main`;
6. contain only the Owner-approved paths/actions.

If the branch is behind `main`, the cleanup stops until reconciled.

## 10. Pre-merge QA — mandatory

Before asking for merge:

- verify the PR head SHA;
- verify the PR changed-file list equals the approved list exactly;
- verify there are no unexpected additions/renames/deletions;
- repeat repository reference checks for deleted candidates;
- verify no remaining HTML/CSS/JS/JSON-LD reference points to a deleted local file;
- check critical site pages and galleries;
- check service-card assets and lightboxes;
- check videos and lazy-loading behavior where relevant;
- check Sofia, Lom, Montana, EN and DE surfaces affected by the batch;
- confirm PR is still Draft / not merged until Owner approval.

If any check is ambiguous or fails: **DO NOT MERGE**.

## 11. Two explicit approvals

Cleanup deletion requires two separate Owner gates:

**Gate 1 — deletion approval:** Owner approves the exact paths to remove.  
**Gate 2 — merge approval:** after branch QA and visual/functional verification, Owner explicitly writes **`merge`**.

Passing Gate 1 does not authorize merge.

## 12. Post-merge live QA

After each merged cleanup batch:

- wait for the live site to update;
- verify the affected live pages;
- verify main pages and service pages relevant to those assets;
- verify galleries/lightboxes where relevant;
- verify no broken images/assets;
- record the merged commit and result in `CLEANUP_AUDIT.md`.

If a regression appears:

1. stop all further cleanup;
2. revert/restore immediately from Git;
3. verify live recovery;
4. investigate before any new cleanup batch.

## 13. History rewrite policy

Normal cleanup must **never rewrite Git history**.

Repository size alone is not justification for destructive history surgery.

Any future history rewrite requires a completely separate Owner decision, separate backup plan, separate risk analysis, and explicit approval naming the exact operation.

## 14. Continuity rule for future chats

Every future chat working on repository cleanup must first read:

1. `START_HERE.md`
2. `CLEANUP_SAFETY_RULES.md`
3. `CLEANUP_AUDIT.md`

Then it must report:

- current `main` SHA;
- current cleanup checkpoint;
- whether any files are approved for deletion;
- current active cleanup branch/PR, if any;
- exact next safe step.

It must **not restart the cleanup from scratch**, reinterpret these rules loosely, or silently expand scope.

## 15. Final veto rule

If there is any conflict between saving space and preserving a potentially useful file:

**PRESERVE THE FILE.**

If evidence is incomplete:

**KEEP.**

If there is doubt:

**STOP AND ASK THE OWNER.**
