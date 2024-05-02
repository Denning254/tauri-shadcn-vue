# A starter Tauri Shadcn Desktop App

### Prerequisite
Rust, Node,NPM, Vue CLI, Cargo must be installed on your computer before you can 

### Build a Starter Tauri Shadcn desktop app
#### Step 1: Create the desktop app scaffolding.
```bash
$ npm create tauri@latest

# Complete the form with your info
✔ Project name · Name-of-your-app** 
✔ Package name · name-of-your-app** 
✔ Choose which language to use for your frontend · TypeScript**  / JavaScript - (pnpm, yarn, npm, bun)
✔ Choose your package manager · npm** 
✔ Choose your UI template · Vue**  - (https://vuejs.org/)
✔ Choose your UI flavor · TypeScript** 
```
Make sure to choose Typescript for the frontend language and Vue for the UI.

```bash
#complete the tauri setup below:
$ cd Name-of-your-app
$ npm install

#Run this to see if your app complises
 npm run tauri dev
```
Add Tailwind to your app.
```bash
vue add tailwind

```
👀*Change the "postcss.config.js" js file extenion to cjs("postcss.config.cjs")* 👀

#### Step 2: Add and Configure Shadcn-vue 
Update the vite.config.ts file to allow for the path module to work


```ts
//Basic vite config
import path from "path"
import { defineConfig } from "vite"
import vue from "@vitejs/plugin-vue"

import tailwind from "tailwindcss"
import autoprefixer from "autoprefixer"

export default defineConfig({
  css: {
    postcss: {
      plugins: [tailwind(), autoprefixer()],
    },
  },
  plugins: [vue()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
})
```
Also update tsconfig.json so your app can resolve paths without error

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "module": "ESNext",
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "skipLibCheck": true,
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    },

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "preserve",

    /* Linting */
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true
  },
  "include": ["src/**/*.ts", "src/**/*.d.ts", "src/**/*.tsx", "src/**/*.vue"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```
install the path module
```bash
npm i -D @types/node

```
Delete default Vite styles
<br>Delete the default Vite stylesheet <mark>./src/style.css</mark>

Run the CLI
<br>Run the shadcn-vue init command to setup your project:
```bash
npx shadcn-vue@latest init
```
Configure components.json 
You will be asked a few questions to configure components.json:
```bash
#the defualts work for most usecases
Would you like to use TypeScript (recommended)? no / yes
Which framework are you using? Vite / Nuxt / Laravel
Which style would you like to use? › Default
Which color would you like to use as base color? › Slate
Where is your global CSS file? › › src/index.css
Do you want to use CSS variables for colors? › no / yes
Where is your tailwind.config.js located? › tailwind.config.js
Configure the import alias for components: › @/components
Configure the import alias for utils: › @/lib/utils
```
Add import to main.ts
```ts
import './assets/index.css'
```
### Example from [www.shadcn-vue.com](https://www.shadcn-vue.com/docs/installation/vite.html)

Adding a button example:
```bash
npx shadcn-vue@latest add button
```

Your vue componment example
```ts
<script setup lang="ts">
import { Button } from '@/components/ui/button'
</script>

<template>
  <div>
    <Button>Click me</Button>
  </div>
</template>
```