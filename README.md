# starter--vue-ts-unocss

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and
disable Vetur)

+ [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## Type Support for `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for
type checking. In editors, we
need [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin)
to make the TypeScript language service aware of `.vue` types.

If the standalone TypeScript plugin doesn't feel fast enough to you, Volar has also implemented
a [Take Over Mode](https://github.com/johnsoncodehk/volar/discussions/471#discussioncomment-1361669) that is more
performant. You can enable it by the following steps:

1. Disable the built-in TypeScript Extension

1) Run `Extensions: Show Built-in Extensions` from VSCode's command palette
2) Find `TypeScript and JavaScript Language Features`, right click and select `Disable (Workspace)`

2. Reload the VSCode window by running `Developer: Reload Window` from the command palette.

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

```sh
pnpm i
```

### Compile and Hot-Reload for Development

```sh
pnpm dev
```

### Type-Check, Compile and Minify for Production

```sh
pnpm build
```

### Run Unit Tests with [Vitest](https://vitest.dev/)

```sh
pnpm test:unit
```

### Run End-to-End Tests with [Cypress](https://www.cypress.io/)

```sh
pnpm build
pnpm test:e2e # or `pnpm test:e2e:ci` for headless testing
```

### Lint with [ESLint](https://eslint.org/)

```sh
pnpm lint
```

## Starter Setup

### Vite([vuejs](https://github.com/vuejs)/**[create-vue](https://github.com/vuejs/create-vue)**)

Terminal:

```sh
pnpm create vue@3
```

`package.json`:

```json
{
  "dependencies": {
    "pinia": "^2.0.21",
    "vue": "^3.2.38",
    "vue-router": "^4.1.5"
  },
  "devDependencies": {
    "@rushstack/eslint-patch": "^1.1.4",
    "@types/jsdom": "^20.0.0",
    "@types/node": "^16.11.56",
    "@vitejs/plugin-vue": "^3.0.3",
    "@vue/eslint-config-prettier": "^7.0.0",
    "@vue/eslint-config-typescript": "^11.0.0",
    "@vue/test-utils": "^2.0.2",
    "@vue/tsconfig": "^0.1.3",
    "cypress": "^10.7.0",
    "eslint": "^8.22.0",
    "eslint-plugin-cypress": "^2.12.1",
    "eslint-plugin-vue": "^9.3.0",
    "jsdom": "^20.0.0",
    "npm-run-all": "^4.1.5",
    "prettier": "^2.7.1",
    "start-server-and-test": "^1.14.0",
    "typescript": "~4.7.4",
    "vite": "^3.0.9",
    "vitest": "^0.23.0",
    "vue-tsc": "^0.40.7"
  }
}
```

#### [antfu](https://github.com/antfu)/**[unplugin-auto-import](https://github.com/antfu/unplugin-auto-import)**&**[unplugin-vue-components](https://github.com/antfu/unplugin-vue-components)**

Terminal:

```sh
pnpm add -D unplugin-auto-import unplugin-vue-components
```

`vite.config.ts`:

```typescript
import AutoImport from "unplugin-auto-import/vite";
import Components from "unplugin-vue-components/vite";

export default defineConfig({
  plugins: [
    AutoImport({
      dirs: ["src/apis", "src/composables", "src/stores", "src/utils"],
      imports: ["vue", "vue-router", "pinia", { axios: [["default", "axios"]] }],
      dts: true,
      eslintrc: { enabled: true },
    }),
    Components({
      dts: true,
    }),
  ],
});
```

【问题】ESLint error of `no-undef`(`'module' is not defined`)

【解决】`.eslintrc.cjs`:

```javascript
module.exports = {
  env: {
    node: true,
  },
};
```

【问题】ESLint error of `no-undef`(`'ref' is not defined`)

【解决】`.eslintrc.cjs`:

```javascript
module.exports = {
  extends: [
    ".eslintrc-auto-import.json"
  ],
};
```

【问题】`Unknown html tag HelloWorld`、`TS2304: Cannot find name 'ref'.`

【解决】`tsconfig.app.json`:

```json
{
  "include": [
    "auto-imports.d.ts",
    "components.d.ts"
  ]
}
```

#### [unocss](https://github.com/unocss)/**[unocss](https://github.com/unocss/unocss)**

Terminal:

```sh
pnpm add -D unocss @unocss/preset-uno @unocss/preset-attributify @unocss/preset-icons
```

`main.ts`:

```typescript
import "uno.css";
```

`vite.config.ts`:

```typescript
import Unocss from "unocss/vite";
import { presetAttributify, presetIcons, presetUno } from "unocss";

export default defineConfig({
  plugins: [
    Unocss({
      presets: [presetUno(), presetAttributify(), presetIcons()],
    }),
  ],
});
```

##### [Icones](https://icones.js.org/)

Terminal:

```sh
pnpm add -D @iconify-json/logos @iconify-json/carbon
```

`vite.config.ts`:

```typescript
export default defineConfig({
  plugins: [
    Unocss({
      presets: [
        presetIcons({
          collections: {
            logos: () => import("@iconify-json/logos").then((i) => i.icons),
            carbon: () => import("@iconify-json/carbon").then((i) => i.icons),
          },
        }),
      ],
    }),
  ],
});
```

#### [vueuse](https://github.com/vueuse)/**[vueuse](https://github.com/vueuse/vueuse)**

Terminal:

```sh
pnpm add @vueuse/core
```

##### [@vueuse/integrations](https://vueuse.org/integrations/readme.html#vueuse-integrations)

Terminal:

```sh
# useAxios
pnpm add axios
# useCookies
pnpm add universal-cookie
# useJwt
pnpm add jwt-decode
# useNProgress
pnpm add nprogress
# useFocusTrap
pnpm add focus-trap
# useAsyncValidator
pnpm add async-validator
# useIDBKeyval
pnpm add idb-keyval
```

#### [leoforfree](https://github.com/leoforfree)/**[cz-customizable](https://github.com/leoforfree/cz-customizable)**

Terminal:

```sh
pnpm add -D cz-customizable
```

`package.json`:

```json
{
  "config": {
    "commitizen": {
      "path": "node_modules/cz-customizable"
    }
  }
}
```

`.cz-config.js`:

```javascript
module.exports = {
  types: [
    { value: "feat", name: "feat:     A new feature" },
    { value: "fix", name: "fix:      A bug fix" },
    { value: "docs", name: "docs:     Documentation only changes" },
    { value: "style", name: "style:    Changes that dont affect the meaning of the code" },
    { value: "refactor", name: "refactor: A code change that neither fixes a bug nor adds a feature" },
    { value: "perf", name: "perf:     A code change that improves performance" },
    { value: "test", name: "test:     Adding missing tests" },
    { value: "chore", name: "chore:    Changes to the build process or auxiliary tools" },
    { value: "revert", name: "revert:   Revert to a commit" },
    { value: "wip", name: "wip:      Work in progress" },
  ],

  scopes: [
    { name: "project" },
    { name: "assets" },
    { name: "components" },
    { name: "composables" },
    { name: "router" },
    { name: "stores" },
    { name: "types" },
    { name: "views" },
  ],

  // override the messages, defaults are as follows
  messages: {
    type: "Select the type of change that you're committing:",
    scope: "\nDenote the SCOPE of this change (optional):",
    // used if allowCustomScopes is true
    customScope: "Denote the SCOPE of this change:",
    subject: "Write a SHORT, IMPERATIVE tense description of the change:\n",
    body: 'Provide a LONGER description of the change (optional). Use "|" to break new line:\n',
    breaking: "List any BREAKING CHANGES (optional):\n",
    footer: "List any ISSUES CLOSED by this change (optional). E.g.: #31, #34:\n",
    confirmCommit: "Are you sure you want to proceed with the commit above?",
  },

  allowCustomScopes: true,
  allowBreakingChanges: ["feat", "fix"],
  skipQuestions: ["body", "footer"],

  subjectLimit: 100,
  footerPrefix: "ISSUES CLOSED:",
};
```

##### [commitizen](https://github.com/commitizen)/**[cz-cli](https://github.com/commitizen/cz-cli)**

Terminal:

```sh
pnpm add -D commitizen
npm pkg set scripts.commit="cz"
```

#### [conventional-changelog](https://github.com/conventional-changelog)/**[commitlint](https://github.com/conventional-changelog/commitlint)**

Terminal:

```sh
pnpm add -D @commitlint/config-conventional @commitlint/cli
```

`.commitlintrc.js`:

```javascript
module.exports = {
  extends: ["@commitlint/config-conventional"],
  rules: {
    "type-enum": [2, "always", ["feat", "fix", "docs", "style", "refactor", "perf", "test", "chore", "revert", "wip"]],
    "subject-case": [0],
  },
};
```

##### [typicode](https://github.com/typicode)/**[husky](https://github.com/typicode/husky)**

```sh
pnpm add -D husky
pnpm pkg set scripts.prepare="husky install"
git init
pnpm prepare
npx husky add .husky/commit-msg  "pnpm exec commitlint --edit"
npx husky add .husky/pre-commit  "pnpm lint && pnpm type-check"
```

### Git

Terminal:

```sh
git add -A
git branch -M main
git remote add origin git@github.com:cicadasinging/starter--vite-ts-unocss.git
pnpm commit
```
