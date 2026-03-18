creating a new svelte project:
bunx sv create ./ --add tailwindcss


add ons like tailwind and lucia auth
https://svelte.dev/docs/kit/integrations#Add-ons

this is interesting, so you can build like a component library using sveltekit https://svelte.dev/docs/kit/packaging

this could be very useful when i have so many project and i dont want to build same components again and again

using this you can make your own library something like "omar-ui" and publish it to npm 

then in any project you use it by soemthing like:


```
import { Button } from "omar-ui"
```


this is very nice tbh
