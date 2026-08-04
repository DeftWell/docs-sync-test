# docs-sync-test

The standing test fixture for the Lemma Docs GitHub sync (lemma-docs issue #28
and its later phases). Deliberately public so the sync can be tested without a
token; nothing in here is real documentation.

The synced content lives under `docs/` — this README sits outside it, and the
sync skips README files anyway.

## Test recipes

- **First sync:** connect `DeftWell/docs-sync-test`, branch `main`, folder
  `docs`, then Dry run (expect one create row per file) and Sync now.
- **Incremental update:** edit `docs/sync-test/change-me.md` here, commit to
  main, Sync now. Exactly one row should sync; the rest stay untouched.
- **Delete / prune:** delete `change-me.md`, Sync now — its doc drops to
  draft. Restore the file and it republishes.
- **Rename:** rename a file in place (same folder), Sync now — the doc must
  keep its ID and URL.
- **Conflict:** in warn mode, edit a synced doc in wp-admin, Sync now — it is
  kept and reported. Sync with Force — the repo wins.
- **Reset:** on the site, detach or trash the synced docs and delete the
  "Sync Test" collection; the next sync recreates everything.

When a new sync phase lands (webhooks, images, previews), add its fixture
files under `docs/` and a recipe line here.
