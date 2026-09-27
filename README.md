# clypsy-edge
Stable public hostname for the Clypsy Telegram Mini App. Vercel rewrites every path server-side to the current
Cloudflare quick tunnel. `vercel.json` is rewritten and pushed automatically by `scripts/supervise-clypsy.sh`
(banvanxd/clypsy) whenever the tunnel URL changes.
