# mailpit-app

Standalone Alpine service that downloads and runs [axllent/mailpit](https://github.com/axllent/mailpit) v1.31.1 — SMTP sink + web UI. No user source to iterate on.

## Zerops service facts

- HTTP ports: `8025` (web UI, `httpSupport: true`); `1025` (SMTP, plain TCP)
- Siblings: —
- Runtime base: `alpine@3.21`

## Zerops

No dev iteration loop — the app is an upstream binary. Changes in this repo only affect `download-mailpit.sh`. Each change requires a full build+deploy through the **Zerops development workflow via `zcp` MCP tools**.

## Notes

- Mailpit version pinned via `MAILPIT_VERSION` in `download-mailpit.sh` (default `v1.31.1`).
- Import snippet lives in `README.md`; no standalone project import YAML in this repo.
