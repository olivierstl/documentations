# Formatter et vérifier le code

[← Retour à l'accueil](/README.md)

## eslint

- [Documentation officielle](https://eslint.org/docs/latest/use/getting-started)
- [Config eslint alsa](https://github.com/alsacreations/eslint)

Installer eslint avec la commande `pnpm add --save-dev eslint`.

Initialiser eslint avec la commande `npx eslint --init` et répondre aux questions sur le projet.

Afficher la config eslint générée : `npx eslint --print-config eslintrc.cjs`.

## prettier

[Documentation officielle](https://prettier.io/docs/en/)

Installer prettier pour eslint : `pnpm add prettier eslint-config-prettier eslint-plugin-prettier`.

## husky

Husky permet d'executer des hook lors des commits et donc de vérifier les fichiers avant de les commiter.

Installer husky `pnpm add --save-dev husky` à la racine du projet.

Initialiser husky avec la commande `npx install husky` à la racine du projet.

Ajouter la ligne suivante dans la section `scripts` du fichier `package.json` : `"prepare": "install husky"`. Cette commande s'executera avant `(p)npm install`.

### Linter les fichiers avant commit

Installer la dépendance pour linter le code `pnpm add --save-dev lint-staged` à la racine du projet.

Ajouter un hook `pre-commit` à husky avec la commande `npx husky add .husky/pre-commit "npx lint-staged"` en lui demandant d'éxecuter une commande pour linter.

On ajoute ensuite cette commande au fichier `package.json` :

```json
  "scripts": { … },
  "lint-staged": {
    "**/*": "prettier --write --ignore unknown"
  },
```

Pour résoudre les conflits avec eslint, installer la dépendance [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier) puis ajouter `prettier` en `pnpm add --save-dev eslint-config-prettier`.

### Linter les messages de commit 🤯

On utilise [conventionnal commit](https://www.conventionalcommits.org/en/v1.0.0/) comme base pour réstreindre la nomenclature de nos commits. Pour l'installation, suivre les [indications du repo](https://github.com/conventional-changelog/commitlint/#what-is-commitlint). Ne pas oublier de varier les commandes d'installation pour `pnpm`.

Après ça, Husky devrait aboyer dans la CLI si les messages de commits ne suivent pas la nomenclature. 🐕

## Ressources

- [Installer prettier & husky avec eslint (en) - YT](https://www.youtube.com/watch?v=tmTajqVgkwI)
- [VsCode + ESLint + Prettier - YT](https://www.youtube.com/watch?v=XDlj3fWzho4)
