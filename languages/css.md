# CSS

[← Retour à l'accueil](/README.md)

## Features waiting room

### `@scope`

- [Limit the reach of your selectors with the CSS @scope at-rule](https://developer.chrome.com/articles/at-scope)
- [@scope in css](https://fullystacked.net/posts/scope-in-css/)
- [Can I use](https://caniuse.com/css-cascade-scope)

### Nesting CSS

- [CSS nesting examples](https://ishadeed.com/article/css-nesting/)
- [CSS nesting - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_nesting)
- [Can I use](https://caniuse.com/?search=nesting)

### `@container`

- [@container - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/@container)
- [Can I use](https://caniuse.com/?search=%40container)
- [Getting started with CSS container queries - MDN](https://developer.mozilla.org/en-US/blog/getting-started-with-css-container-queries/?utm_source=CSS-Weekly&utm_medium=newsletter&utm_campaign=issue-569-november-30-2023)
- [CSS container queries - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_container_queries#container_query_length_units)

### `margin-trim`

- [margin-trm - MDN](https://developer.mozilla.org/fr/docs/Web/CSS/margin-trim)

### `text-wrap: balance`

- [text-wrap - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/text-wrap)

## Features à utiliser

### Sélecteurs `:where()` et `is()`

- [where - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/:where)
- [is - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/:is)

Ces sélecteurs fournissent la même fonctionnalité, à l'exception que `:where()` et son contenu ne compte pas le poids du sélecteur.


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

### Media query range syntax

- [Can I use](https://caniuse.com/?search=css-media-range-syntax)
- [The New CSS Media Query Range Syntax - CSS Tricks](https://css-tricks.com/the-new-css-media-query-range-syntax/)

Permet d'écrire les media queries avec des opérateurs logiques, ce qui simplifie leur écriture.

Exemple 1 :

```CSS
@media (min-width: 600px) { … }

// devient :
@media (width >= 600px ) { … }
```

Exemple 2 :

```CSS
@media (min-width: 400px) and (max-width: 1000px) { … }

// devient :
@media (400px <= width <= 1000px) { … }
```

### `clamp()`

- [Clamp - MDN](https://developer.mozilla.org/fr/docs/Web/CSS/clamp)

La fonction CSS clamp() permet de fixer une limite hausse et basse à une valeur (le plus souvent fluide).

Exemple :

```CSS
width: clamp(10px, 4em, 80px);
/* avec 1em = 16px, on a 4em = 16px * 4 = 64px */
width: clamp(10px, 64px, 80px);
/* clamp(MIN, VAL, MAX) est résolue comme max(MIN, min(VAL, MAX))) */
width: max(10px, min(64px, 80px))
width: max(10px, 64px);
width: 64px;
```

### `color-mix`

- [color-mix - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/color-mix)

## Ressources

- [Locally private custom propreties](https://fullystacked.net/posts/scope-in-css/)
- [Surprising Facts About New CSS Selectors](https://cloudfour.com/thinks/surprising-facts-about-new-css-selectors/)
- [Layout Breakouts with CSS Grid](https://ryanmulligan.dev/blog/layout-breakouts/)
