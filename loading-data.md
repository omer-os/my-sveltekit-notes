
Data returned from layout load functions is available to child +layout.svelte components and the +page.svelte component as well as the layout that it 'belongs' to.



If multiple load functions return data with the same key, the last one 'wins' — the result of a layout load returning { a: 1, b: 2 } and a page load returning { b: 3, c: 4 } would be { a: 1, b: 3, c: 4 }.


The +page.svelte component, and each +layout.svelte component above it, has access to its own data plus all the data from its parents.

In some cases, we might need the opposite — a parent layout might need to access page data or data from a child layout. For example, the root layout might want to access a title property returned from a load function in +page.js or +page.server.js. This can be done with page.data:
<script lang="ts">
	import { page } from '$app/state';
</script>

<svelte:head>
	<title>{page.data.title}</title>
</svelte:head>




+page.js and +layout.js files export universal load functions that run both on the server and in the browser
+page.server.js and +layout.server.js files export server load functions that only run server-side
