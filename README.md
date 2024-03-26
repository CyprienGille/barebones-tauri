# Steps to produce a barebones tauri+sveltekit+tailwind app

## From https://tauri.app/v1/guides/getting-started/setup/sveltekit/

### Frontend scaffolding
```bash
npm create svelte@latest
```
- (Folder name)
- Skeleton Project
- TypeScript
- ESLint + Prettier

### SSG Mode
```bash
npm install --save-dev @sveltejs/adapter-static
```
- Change the first line of svelte.config.js to :
```js
import adapter from '@sveltejs/adapter-static' // This was changed from adapter-auto
```
- Create the file `src/routes/+layout.ts` and fill it with:
```ts
export const prerender = true
export const ssr = false
```

```bash
npm install
npm install @tauri-apps/api
```

### Backend scaffolding
```bash
cargo tauri init
```
- App name
- Window name
- Assets : `../build`
- Dev URL : `http://localhost:5173`
- Dev command : `npm run dev`
- Build command : `npm run build`

**Check that everything works so far with `cargo tauri dev`**

## From https://tailwindcss.com/docs/guides/sveltekit
**Follow steps 2-6 (step 3 might not be needed).**
```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```
- In `svelte.config.js` :
```js
import { vitePreprocess } from '@sveltejs/vite-plugin-svelte';
/** @type {import('@sveltejs/kit').Config} */
const config = {
  kit: {
    adapter: adapter()
  },
  preprocess: vitePreprocess()
};
export default config;
```
- In `tailwind.config.js` :
```js
/** @type {import('tailwindcss').Config} */
export default {
  content: ['./src/**/*.{html,js,svelte,ts}'],
  theme: {
    extend: {}
  },
  plugins: []
};
```
- In `src/app.css` (new) :
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```
- In `src/routes/+layout.svelte` (new) :
```svelte
<script>
  import "../app.css";
</script>

<slot />
```

## From https://github.com/tailwindlabs/prettier-plugin-tailwindcss
```bash
npm install -D prettier prettier-plugin-tailwindcss
```
- In `prettier.config.js` :
```js
module.exports = {
  plugins: ['prettier-plugin-tailwindcss'],
}
```
