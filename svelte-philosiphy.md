this is from sveltekit documentation on https://svelte.dev/docs/kit/web-standards

```
Throughout this documentation, you'll see references to the standard Web APIs that SvelteKit builds on top of. Rather than reinventing the wheel, we use the platform, which means your existing web development skills are applicable to SvelteKit. Conversely, time spent learning SvelteKit will help you be a better web developer elsewhere.

These APIs are available in all modern browsers and in many non-browser environments like Cloudflare Workers, Deno, and Vercel Functions. During development, and in adapters for Node-based environments (including AWS Lambda), they're made available via polyfills where necessary (for now, that is — Node is rapidly adding support for more web standards).
```


fetch => sveltekit gives me a special version of fetch inside load functions, server hooks, and API routes. if i call fetch('/api/products') inside a server load function it doesnt make an actual HTTP request to itself — it calls the endpoint code directly (no network round trip). it also automatically carries the user's cookies/auth so i dont lose the session. and i can use relative URLs instead of full http://localhost:5173/... . outside of these places (random server utility files etc) i lose this magic and need full URLs + manually pass cookie/auth headers



headers: 
The Headers interface allows you to read incoming request.headers and set outgoing response.headers. For example, you can get the request.headers as shown below, and use the json convenience function to send modified response.headers:
src/routes/what-is-my-user-agent/+server
```ts
import { json } from '@sveltejs/kit';
import type { RequestHandler } from './$types';

export const GET: RequestHandler = ({ request }) => {
	// log all headers
	console.log(...request.headers);

	// create a JSON Response using a header we received
	return json({
		// retrieve a specific header
		userAgent: request.headers.get('user-agent')
	}, {
		// set a header on the response
		headers: { 'x-custom-header': 'potato' }
	});
};
```
```
```




If an error occurs during load, SvelteKit will render a default error page. You can customise this error page on a per-route basis by adding an +error.svelte file:
<script lang="ts">
	import { page } from '$app/state';
</script>

<h1>{page.status}: {page.error.message}</h1>









