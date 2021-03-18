---
title: Migrating from Sapper
---

SvelteKit is the successor to Sapper and shares many elements of its design.

If you have an existing Sapper app that you plan to migrate to SvelteKit, however, there are a number of changes you will need to make.

Whilst not a comprehensive list, most applications will benefit from the following:

- Add a [`svelte.config.cjs` ](https://github.com/sveltejs/kit/blob/master/packages/create-svelte/template/svelte.config.cjs) with the adapter of your choice
- Update your `template.html` to [`app.html`](https://github.com/sveltejs/kit/blob/master/packages/create-svelte/template/src/app.html)
  - It should have a `<div id="svelte">` (or `id` matching `target` in `svelte.config.cjs`)
- The error and layout pages should prefixed by `$` instead of `_`
- Replace imports from `@sapper/app` with imports from `$app/navigation` and `$app/stores` and update APIs accordingly
- If you have source code in `src/node_modules`, move it to `src/lib` and update the import path to `$lib`
- Move any custom `client.js` code to `$layout.svelte` and put it in an `if (browser)` check (`import { browser } from "$app/env";`).
- `preload` has been renamed to `load`. It has a new method signature and return values
- `sapper:prefetch` and `sapper:noscroll` have been renamed to `sveltekit:prefetch` and `sveltekit:noscroll`

The remainder of this section contains more detail on each of these steps.

You may find it helpful to view the [examples](https://github.com/sveltejs/kit/tree/master/examples) while migrating.

Please see [sveltejs/integrations](https://github.com/sveltejs/integrations#sveltekit) for examples of setting up popular tools like PostCSS, Tailwind CSS, mdsvex, Firebase, GraphQL, and Bulma.