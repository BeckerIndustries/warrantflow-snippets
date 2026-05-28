# WarrantFlow Snippets

This repository hosts the public clause/template catalog that the WarrantFlow
desktop app downloads and caches. Officers browse these clauses under
**Warrant Templates** in the app and copy them into a warrant.

## The catalog

`catalog.json` is the single file the app reads. Schema:

```json
{
  "version": 1,                 // bump when you change the catalog
  "updated": "2026-05-27",      // yyyy-MM-dd
  "snippets": [
    {
      "id": "unique-stable-id",       // never reuse; lowercase-with-hyphens
      "category": "item",             // see categories below
      "title": "Human-readable title",
      "body": "The clause text. Use [BRACKETS] for fill-in blanks.",
      "tags": ["search", "keywords"]  // used by the in-app search box
    }
  ]
}
```

### Categories (must be exactly one of these)

| value | meaning |
|---|---|
| `place` | Places to be searched (residence, vehicle, account) |
| `item` | Items / property / records to be seized |
| `expertise` | Affiant-expertise boilerplate paragraphs |
| `probable_cause_fragment` | Reusable probable-cause language |
| `other` | Anything else |

## How to add or edit a clause

1. Edit `catalog.json`.
2. Keep `id` values stable and unique. Add new IDs for new clauses; don't
   recycle an old ID for different content.
3. Bump the top-level `version` and update `updated`.
4. Validate the JSON (any JSON linter, or `python -m json.tool catalog.json`).
5. Commit and push. The app picks up changes the next time a user clicks
   **Refresh** in Warrant Templates.

## Notes

- The catalog is **public and unauthenticated** — don't put anything
  sensitive or agency-confidential here. These are generic, reusable clauses.
- `[BRACKETED]` placeholders are deliberately left for the officer to fill in
  after inserting the clause into a warrant.
