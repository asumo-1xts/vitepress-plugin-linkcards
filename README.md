<h1 align="center">
vitepress-plugin-linkcards
</h1>

<div align="center">

**A VitePress plugin to generate pretty linkcards with OGP.**

You can see: [A blog generated with this plugin](https://blog.asumo.dev/posts/10-vitepress-linkcards.html)

[![NPM Version](https://img.shields.io/npm/v/vitepress-plugin-linkcards?style=flat&logo=npm&logoColor=white&label=npmjs&color=%23CB3837)](https://www.npmjs.com/package/vitepress-plugin-linkcards)
[![VitePress](https://img.shields.io/badge/For_VitePress-v1_|_v2-%235C73E7?logo=vitepress&logoColor=white)](https://vuejs.github.io/vitepress/v1]/)
[![MIT](https://img.shields.io/badge/License-MIT-green)](/LICENSE)

[![Yarn](https://img.shields.io/badge/Built_with_Yarn-v4.9.2-%232C8EBB?logo=yarn&logoColor=white)](https://yarnpkg.com/)
[![Oxc](https://img.shields.io/badge/Oxc-%2300F7F1?logo=oxc&logoColor=white&label=Lint%20and%20Format%20with&labelColor=gray)](https://oxc.rs/)

<img src="https://github.com/asumo-1xts/vitepress-plugin-linkcards/blob/main/.github/screen.webp?raw=true" width=90% alt="How it shows" />

</div>

<br>

<div align="center">

This plugin was forked from [markdown-it-link-to-card](https://github.com/luckrya/markdown-it-link-to-card).

</div>

## Getting started

### Install

```shell
npm i -D vitepress-plugin-linkcards    # npm
yarn add -D vitepress-plugin-linkcards # yarn
pnpm add -D vitepress-plugin-linkcards # pnpm
```

### Usage

#### `docs/.vitepress/config.ts`

```ts
import { defineConfig } from 'vitepress'
import { linkToCardPlugin } from 'vitepress-plugin-linkcards'
import type { LinkToCardPluginOptions } from 'vitepress-plugin-linkcards'

export default defineConfig({
  // ...
  markdown: {
    config: (md) => {
      md.use<LinkToCardPluginOptions>(linkToCardPlugin, {
        // target: "_self" // if needed
      })
    }
  }
  // ...
})
```

#### `*.md`

Generates a linkcard when `@:` appended.

```md
[example](@:https://example.com)
```

## Supported options

### Target

As shown in [Usage](#usage), you can specify the target window in which to open a link.

- `_blank` **(default)**
- `_self`
- `_top`
- `_parent`

### Color theme

You can customize:

| Property                      | **default**           |
| :---------------------------- | --------------------- |
| Border color                  | `var(--vp-c-bg)`      |
| Background color              | `var(--vp-c-bg-soft)` |
| Border color when hovered     | none                  |
| Background color when hovered | none                  |

#### `docs/.vitepress/theme/custom.css`

```css
/* For example: like "Features" in VitePress */

.vitepress-plugin-linkcards-container {
  border-color: #00000000 !important;
  background-color: var(--vp-c-bg-soft) !important;
}

.vitepress-plugin-linkcards-container:hover {
  border-color: var(--vp-c-brand-1) !important;
  background-color: var(--vp-c-bg-soft) !important;
}
```

#### `docs/.vitepress/theme/index.ts`

```ts
import DefaultTheme from 'vitepress/theme-without-fonts'
import type { Theme as ThemeConfig } from 'vitepress'
import './custom.css'

const Theme: ThemeConfig = {
  extends: DefaultTheme
}

export default {
  ...Theme
}
```

## Other specifications

### `.linkcards_cache.json`

It is generated automatically in `docs/` and cache all the parsed metadata.

You can move it to root dir if needed.

### Special handlings for `github.com` and `zenn.dev`

This plugin has special handling for `github.com` and `zenn.dev` to display their metadata correctly.
