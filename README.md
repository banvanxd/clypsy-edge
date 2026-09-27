# clypsy-edge

Public hostname for the Clypsy Telegram Mini App: https://clypsy-app.vercel.app (Vercel project `clypsy-app`).

- `dist/` is the production build of `apps/miniapp`. Vercel's CDN serves it directly, with SPA fallback to
  `index.html`. Hashed `/assets/*` are cached for a year (immutable). `index.html` is `no-cache`.
- Only `/api/*` (with the `/api` prefix stripped), `/media/*` and `/health` are rewritten to the current
  Cloudflare quick tunnel, which points straight at the API on :3001.
- `dist/version.json` shows which commit is live. `dist/edge-origin.json` shows which tunnel host this deployment
  proxies to; the supervisor polls it and only stops an old tunnel once the new host is live here.

Do not edit this repo by hand. It is generated from banvanxd/clypsy (`deploy/clypsy-edge/`):
- `scripts/deploy-miniapp-edge.sh` builds the Mini App, copies `dist/` here, renders `vercel.json` and pushes.
- `scripts/supervise-clypsy.sh` re-renders `vercel.json` (+ `dist/edge-origin.json`) and pushes when the tunnel host
  changes. The new tunnel is started first and the old one keeps serving until Vercel has redeployed.
Every push to `main` makes Vercel redeploy automatically.
