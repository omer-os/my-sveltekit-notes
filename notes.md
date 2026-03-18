we have hooks.client.js as well as hooks.server.js

$lib/server is a special folder that SvelteKit guarantees will never be importable from client-side code. If you try to import something from $lib/server in a component or +page.ts, SvelteKit throws an error at build time.
You put stuff there that should never reach the browser — database clients, API keys, secret tokens, server-only utilities, etc.


SvelteKit also has a `src/params` folder for **param matchers** — functions that validate params before the route matches:
// src/params/integer.ts
export const match = (param: string) => /^\d+$/.test(param)
```

Then use it in your route folder name:
```
src/routes/products/[id=integer]/
