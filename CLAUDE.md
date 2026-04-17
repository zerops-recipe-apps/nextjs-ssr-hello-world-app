# nextjs-ssr-hello-world-app

Next.js 15 SSR starter: standalone output, PostgreSQL, migration guarded by `zsc execOnce` — baseline Next.js SSR recipe on Zerops.

## Zerops service facts

- HTTP port: `3000`
- Siblings: `db` (PostgreSQL) — env: `DB_HOST`, `DB_PORT`, `DB_USER`, `DB_PASS`, `DB_NAME`
- Runtime base: `nodejs@22`

## Zerops dev

`setup: dev` idles on `zsc noop --silent`; the agent starts the dev server.

- Dev command: `npm run dev`
- In-container rebuild without deploy: `npm run build`

**All platform operations (start/stop/status/logs of the dev server, deploy, env / scaling / storage / domains) go through the Zerops development workflow via `zcp` MCP tools. Don't shell out to `zcli`.**

## Notes

- `output: 'standalone'` + `@vercel/nft` dep tracing — no `node_modules` at prod runtime.
- `migrate.cjs` is esbuild-bundled (`migrate.js` + `pg`) so it runs before the server without NODE_PATH gymnastics.
- Do NOT cache `.next/cache` — Zerops cache restore causes EACCES on subsequent builds.
