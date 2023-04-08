# Astro

## Installation

### Installer Astro

[Guide d'installation](https://docs.astro.build/fr/install/auto/#1-utiliser-lassistant-dinstallation)

```shell
pnpm create astro@latest
```

### Framework JS

Au besoin, ajouter un framework JS (vue, react, etc...) avec la commande [astro add](https://docs.astro.build/fr/guides/integrations-guide/#configuration-dint%C3%A9gration-automatique).

### Ajouter les utilitaires

#### Fichier editorconfig

Dropper le fichier dans le répertoire

#### PostCSS 

PostCSS est pris en compte de base via vite ([doc astro](https://docs.astro.build/fr/guides/styling/#postcss) [doc vite](https://vitejs.dev/guide/features.html#postcss)).

* Installer [post css autoprefixer](https://github.com/postcss/autoprefixer)

```shell
pnpm i -D autoprefixer@latest
```

```js
// postcss.config.mjs
import autoprefixer from 'autoprefixer'

export default {
  plugins: [
    autoprefixer
  ]
}
```

> [tester autoprefixer](https://github.com/postcss/autoprefixer#debug)

#### eslint & prettier

[Documentation astro eslint & prettier](https://docs.astro.build/en/editor-setup/#other-tools)

* Installer [config eslint alsa](https://github.com/alsacreations/eslint) 🥝
* Installer [eslint-plugin-astro](https://github.com/ota-meshi/eslint-plugin-astro)
* Installer prettier et [prettier-plugin-astro](https://github.com/withastro/prettier-plugin-astro)

> Lien externe: [faire fonctionner eslint & prettier avec astro](https://patheticgeek.dev/blog/astro-prettier-eslint-vscode).


