# electric

The Electric sync service for Pageloop, deployed on Render from this Dockerfile.

| Branch | Render service | Deploys |
|---|---|---|
| `main` | `electric-staging` | automatically on push |
| `prod` | `electric-prod` | manually, after `main` is merged into `prod` |

## Upgrading Electric

1. Bump the tag in `Dockerfile` on `main`. Staging redeploys.
2. Check staging (inbox, event detail, KB page live updates) against the pageloop-ui client version.
3. Merge `main` into `prod`, then deploy `electric-prod` (`render deploys create srv-da6sndafngtc73c9ek50`).

## Production settings (in Render, not in this repo)

- Plan: standard (2 GB, 1 CPU).
- Persistent disk: 5 GB at `/var/data`, with `ELECTRIC_STORAGE_DIR=/var/data/electric`, so shape
  logs survive restarts and clients don't all resync after a deploy.
- A restart takes ~35 s (disk-backed services cannot do zero-downtime deploys).
- `ELECTRIC_SECRET` and `DATABASE_URL` are set on the service.

## History

Replaces `dinakartumu/electric-staging` (public, which both services built from until 2026-10-08)
and `pageloop/electric-staging` (private, which Render's GitHub app could not read). Both are archived.
