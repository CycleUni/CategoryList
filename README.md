# CategoryList

JSON fixture for CycleUni's admin Category (college) bulk-import feature.

- **Target API**: `POST /api/v1/admin/categories/bulk/` (`adminapi.views.AdminCategoryBulkImportView`, staff-only)
- **Request body**: `{"action": "preview" | "apply", "items": [...]}` — send `categories.json`'s `items` array as-is
- **Matching key**: `slug` (unique per region on the `Category` model) — re-importing is idempotent; unchanged rows are skipped, differing rows are reported as `modified`
- **Field shapes**: canonical `title`/`description` are in English, matching the seeded defaults in `UniBooks-BE/core/default_categories.py`; `translations.zh-TW` and `translations.zh-HK` hold the Taiwan and Hong Kong wording

Contents: the 8 default colleges from `core/default_categories.py` (worded identically, so importing into a region seeded with them reports them as `unchanged`) plus 4 additional colleges (agriculture, arts & design, education, dentistry). Tested end-to-end against the live endpoint in `UniBooks-BE/tests/test_bulk_import_fixtures.py`, including the `new`/`modified`/`unchanged` diff paths.
