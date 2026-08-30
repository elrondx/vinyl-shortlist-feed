# Brett VINYL shortlist feed

This repository publishes Brett's curated Facebook Marketplace VINYL shortlist
as two secret-keyed, read-only JSON snapshots for the separate Daily Vinyl
Watch.

## Security model

- No shortlist JSON is committed to this repository.
- No Facebook credentials, cookies or session data are used.
- The Shopping Agent origin URL is stored as an encrypted Actions secret.
- The primary and fallback filenames are independent 256-bit secrets.
- GitHub Pages is GET-only; incorrect paths return 404.
- The workflow validates the schema and rejects snapshots containing records
  marked rejected, sold, withdrawn or stale.

## Repository secrets

- `ORIGIN_URL`: scoped read-only Shopping Agent endpoint.
- `PRIMARY_PATH_KEY`: random 64-character hexadecimal primary path.
- `FALLBACK_PATH_KEY`: separate random 64-character hexadecimal fallback path.

The workflow runs hourly. If an origin fetch or validation fails, the
deployment fails and GitHub Pages keeps serving the previous last-good snapshot.
