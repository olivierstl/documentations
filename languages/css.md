# CSS

[← Retour à l'accueil](/README.md)

## Features waiting room

### Sélecteur `:has()`

- [Documentation MDN](https://developer.mozilla.org/fr/docs/Web/CSS/:has).
- [Can I use](https://caniuse.com/?search=has)

Exemples:

```css
a:has(> img) { … }
```

Ce sélecteur permet de cibler uniquement les éléments `<a>` qui contiennent un fils direct `<img>`.

```css
h1:has(+ p) { … }
```

Le sélecteur qui suit correspond aux éléments `<h1>` qui précèdent directement un élément `<p>`.

### `@scope`

- [Limit the reach of your selectors with the CSS @scope at-rule](https://developer.chrome.com/articles/at-scope)
- [@scope in css](https://fullystacked.net/posts/scope-in-css/)
- [Can I use](https://caniuse.com/css-cascade-scope)

### Nesting CSS

- [CSS nesting examples](https://ishadeed.com/article/css-nesting/)
- [CSS nesting - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_nesting)
- [Can I use](https://caniuse.com/?search=nesting)

### `@container`

- [@containe - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/@container)
- [Can I use](https://caniuse.com/?search=%40container)

## Ressources

- [Locally private custom propreties](https://fullystacked.net/posts/scope-in-css/)
- [Surprising Facts About New CSS Selectors](https://cloudfour.com/thinks/surprising-facts-about-new-css-selectors/)
- [Layout Breakouts with CSS Grid](https://ryanmulligan.dev/blog/layout-breakouts/)
