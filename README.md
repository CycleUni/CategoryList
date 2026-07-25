# CategoryList

JSON fixture for CycleUni's admin Category (college) bulk-import feature.

- **Target API**: `POST /api/v1/admin/categories/bulk/` (`adminapi.views.AdminCategoryBulkImportView`, staff-only)
- **Request body**: `{"action": "preview" | "apply", "items": [...]}` — send `categories.json`'s `items` array as-is
- **Matching key**: `slug` (unique on the `Category` model) — re-importing is idempotent; unchanged rows are skipped, differing rows are reported as `modified`
- **Field shapes**: canonical `title`/`description` are in Chinese (matching this project's actual seeded data in `core/migrations/0002_seed_categories.py`, not the model docstring's English-canonical description), `translations.en` holds the English variant

Contents: the 8 colleges already seeded by `core/migrations/0002_seed_categories.py` (worded identically, so importing against a fresh database reports them as `unchanged`) plus 4 additional colleges (agriculture, arts & design, education, dentistry). Tested end-to-end against the live endpoint in `CycleUni-BE/tests/test_bulk_import_fixtures.py`, including the `new`/`modified`/`unchanged` diff paths.
