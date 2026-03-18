```
my-project/
├ src/
│ ├ lib/
│ │ ├ server/
│ │ │ └ [your server-only lib files]
│ │ └ [your lib files]
│ ├ params/
│ │ └ [your param matchers]
│ ├ routes/
│ │ └ [your routes]
│ ├ app.html
│ ├ error.html
│ ├ hooks.client.js
│ ├ hooks.server.js
│ ├ service-worker.js
│ └ instrumentation.server.js
├ static/
│ └ [your static assets]
├ tests/
│ └ [your tests]
├ package.json
├ svelte.config.js
├ tsconfig.json
└ vite.config.js
```
```
```


src => main code
lib/server => i write server code here like db.ts and auth.ts, these files cant be reached in client side code, it doesnt allow me to use them there if i try ill get error saying these are server side code

src/params => i can validate route params here if i wanted, for example if i have this folder:
`/users/[userId]` and the id is int i can have something like this in params folder to validate the id and always make sure its number/integer and always there
```ts
// src/params/integer.ts
export const match = (param: string) => /^\d+$/.test(param)
```

then i rename the route folder to `/users/[userId=integer]` and now if someone goes to `/users/abc` they get 404 instead of hitting my load function with bad data


hooks.server.ts => runs on every server request before anything else. i can use it to intercept requests, add auth checks, modify responses, set cookies, etc. the main function is `handle` which gets the request event and a `resolve` function that continues to the actual route. also has `handleFetch` to modify fetch requests made in server load functions and `handleError` to catch unexpected errors

hooks.client.ts => NOT like hooks.server.ts. it doesnt intercept requests or run on every navigation. it ONLY has `handleError` which catches unhandled client-side errors (component crash, client load function throw, navigation fail). i can use it to send errors to a logging service like Sentry or return a custom error message that shows up in `$page.error`. if i dont need error tracking i can skip this file entirely
```ts

```ts
// hooks.client.ts
export const handleError = ({ error, event }) => {
  // send to Sentry, LogRocket, etc.
  console.error(error)
  return { message: "Something went wrong" }
}
```
```





