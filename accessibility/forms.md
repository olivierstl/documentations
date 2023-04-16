
# Formulaires

## Liens utiles

* [w3c design system - Forms](https://design-system.w3.org/styles/forms.html#top-tips)
* [Modèles de conception WAI](https://www.w3.org/WAI/ARIA/apg/patterns/)

## Sommaire

<!-- no toc -->
* [Label](#label)
  * [Label masqué](#label-masqué)
  * [Pas de label](#pas-de-label)
* [Placeholder](#placeholder)
* [Informations sur les champs](#informations-sur-les-champs)
* [Champs requis et optionnels](#champs-requis-et-optionnels)
  * [Champs facultatifs par défaut et champs obligatoires signalés](#champs-facultatifs-par-défaut-et-champs-obligatoires-signalés)
  * [Champs obligatoires par défaut et champs facultatifs signalés](#champs-obligatoires-par-défaut-et-champs-facultatifs-signalés)
  * [Exemples de bonnes et mauvaises pratiques](#exemples-de-bonnes-et-mauvaises-pratiques)
  * [Cas particuliers : input cochables](#cas-particuliers--input-cochables)
* [Champs et éléments disabled](#champs-et-éléments-disabled)
* [Faciliter la saisie](#faciliter-la-saisie)
  * [Type](#type)
  * [Format attendu](#format-attendu)
  * [Autocomplete](#autocomplete)
  * [Fieldset](#fieldset)
    * [Informations complémentaires aux groupes de champs](#informations-complémentaires-aux-groupes-de-champs)
* [Types de données particulières](#types-de-données-particulières)
  * [Données numériques](#données-numériques)
  * [Mot de passe et email](#mot-de-passe-et-email)
  * [Numéro de téléphone](#numéro-de-téléphone)
  * [Heure et date](#heure-et-date)
    * [Heure](#heure)
    * [Date](#date)
* [Checkbox, switch et radio](#checkbox-switch-et-radio)
  * [Caractère requis](#caractère-requis)
    * [Input seul](#input-seul)
    * [Groupe d'inputs](#groupe-dinputs)
  * [Informations sur les inputs cochables](#informations-sur-les-inputs-cochables)
    * [Sur le groupe de choix](#sur-le-groupe-de-choix)
    * [Sur un input cochable en particulier](#sur-un-input-cochable-en-particulier)
* [Select](#select)
* [Champs conditionnels](#champs-conditionnels)
  * [Retours d'expérience de Gov.uk](#retours-dexpérience-de-govuk)
* [Erreurs et validation](#erreurs-et-validation)
  * [Rendu des messages d'erreurs](#rendu-des-messages-derreurs)
  * [Types d'erreurs et informations nécessaires](#types-derreurs-et-informations-nécessaires)
    * [Absence de saisie dans un champ obligatoire](#absence-de-saisie-dans-un-champ-obligatoire)
    * [Type de données ou format](#type-de-données-ou-format)
  * [Validation en cours de saisie](#validation-en-cours-de-saisie)
  * [Validation de formulaire et résumé des erreurs](#validation-de-formulaire-et-résumé-des-erreurs)
  * [Résumé des erreurs proposé par le W3C](#résumé-des-erreurs-proposé-par-le-w3c)

## Label

Une étiquette de champ est un texte qui permet d'expliquer quelle donnée est attendue. Tous les champs doivent disposer d'un élément `<label>` associé aussi appelé étiquette. Ce dernier est associé au champ grâce aux attributs `for=""` et `id=""`. L'élément `<label>` n'entoure pas l'élément `<input>`, il est placé avant ce dernier&nbsp;:

```html
<label for="demo-input">Étiquette</label> <input id="demo-input" type="text" />
```

Dans le cas d'inputs cochables (checkbox, switch, radios), l'élément `<label>` se place après l'élément `<input>`&nbsp;:

```html
<input id="demo-checkbox" type="checkbox" />
<label for="demo-checkbox">Étiquette</label>
```

### Label masqué

Certains champs sont maquettés sans étiquette visible. Si c'est le cas, conserver un élément `<label>` masqué visuellement via la classe `sr-only`. Une alternative textuelle visible reste obligatoire: compléter l'attribut `title` du champ ou ajouter un tooltip. Dans le cas d'utilisation de tooltip, ce dernier ne devra pas être associé au champ ni vocalisé pour éviter de faire doublon avec l'élément `<label>` caché.

```html
<label for="demo-input" class="sr-only">Étiquette</label>
<input id="demo-input" type="text" title="Étiquette" />
```

### Pas de label

Certains champs n'ont volontairement pas de label car un autre élément de l'interface donne déjà l'information. Il faut alors associer le champ à cet élément en ajoutant l'id de ce dernier dans l'attribut `aria-labelledby` de l'élément `<input>`.

```html
<h2 for="demo-title">Titre</h2>
...
<input id="demo-input" type="text" aria-labelledby="demo-title" />
```

## Placeholder

L'utilisation d'un attribut `placeholder` à des fins informatives uniquement est toujours contrindiqué&nbsp;:

* Il souffre de gros soucis de contraste par défaut (possible de fixer via CSS)
* Son contenu est masqué dès la première saisie
* Le contenu du `placeholder` peut laisser penser à l'internaute que le champ est déjà renseigné

Il reste possible d'utiliser un `placeholder` aux conditions suivantes&nbsp;:

* Le champ a une étiquette explicite visible
* L'attribut `placeholder` n'est pas le seul vecteur d'informations d'aide à la saisie (format/type de données attendues)

## Informations sur les champs

Il est possible d'apporter de l'information supplémentaire concernant un champ dans un [passage de texte associé](https://accessibilite.numerique.gouv.fr/methode/glossaire/#passage-de-texte-lie-par-aria-labelledby-ou-aria-describedby). Ces informations se placent la plupart du temps dans un élément html après l'input. Les exemples les plus courant sont&nbsp;:

* Mention obligatoire
* Aide à la saisie
* Message d'erreur
* Message de succès
* Compteur de limite de caractères

L'information fournie doit être la plus concise possible. Si de telles informations sont présentes&nbsp;:

* Le passage de texte possède un attribut `id` unique
* Le champ possède l'attribut `aria-describedby` et ce dernier contient les `id` de chaque passage de texte associé. Pour cumuler plusieurs `id` au sein de l'attribut, il suffit de les séparer par des espaces.

```html
<div class="form-group ">
    <label for="demo" class="form-label"> Label </label>
    <input
        id="demo"
        class="form-control"
        type="text"
        name="demo"
        aria-describedby="help-demo"
    />
    <p id="help-demo" class="help-block">Passage de texte</p>
</div>
```

Par convention de code, il est recommandé d'inclure une notion sémantique dans le nommage des ids de passage de texte, exemple : `help-...` pour une aide, `error-...` et `success-...` pour un message d'erreur ou de succès ou encore `required-...` pour un message requis.

## Champs requis et optionnels

La complétion d'un formulaire dépend de sa lisibilité&nbsp;: L'internaute doit être en mesure de comprendre facilement quels champs sont obligatoires pour valider un formulaire. Si un champ est requis, l'élement de formulaire doit posséder l'attribut `required` (ajouter l'attribut `novalidate` sur l'élément `<form>` pour éviter la validation native).

```html
<form novalidate>
    ...
    <label for="demo-input">Étiquette</label>
    <input id="demo-input" type=text" ... required> ...
</form>
```

Le caractère requis ou facultatif des champs doit être indiqué visuellement. Les consignes d'indications varient selon le contexte&nbsp;:

### Champs facultatifs par défaut et champs obligatoires signalés

Sans mention contraire, les champs d'un formulaire sont implicitement considérés comme facultatifs. Il convient alors de préciser leur caractère obligatoire, pour ça, plusieurs options&nbsp;:

* L'écrire en toute lettre dans l'élément `<label>` : `(obligatoire)`
* Utiliser un symbole comme l'astérisque `*`. Dans ce cas, il est nécessaire de décrire le sens du symbole : `<p>Les champs marqués d'une étoile (*) sont obligatoires</p>`. Cette information doit apparaitre avant le premier champ du formulaire concerné hors de l'élément `<form>`&nbsp;: Certaines technologies d'assistance possèdent un mode de lecteur spécial formulaire. Ce mode peut ignorer les textes non associés à un champ quelconque. Il n'est pas nécessaire de la lier à chaque champ via l'attribut `aria-describedby`.

```html
<p>Les champs marqués d'une étoile (*) sont obligatoires</p>
<form>
    ...
    <label for="demo-input">Étiquette *</label>
    <input id="demo-input" type=text" ... required> ...
</form>
```

### Champs obligatoires par défaut et champs facultatifs signalés

Il est également possible de rendre tous les champs obligatoires par défaut et de signaler les champs facultatifs (Voir [critère 11.10](https://www.numerique.gouv.fr/publications/rgaa-accessibilite/methode-rgaa/criteres/#crit-11-10) - Cas particuliers et Notes techniques (fin de bloc)).

Dans ce cas, il est nécessaire de décrire le fonctionnement du formulaire : `<p>Tous les champs sont obligatoires sauf ceux marqués de la mention "facultatif"</p>`. Cette information doit apparaitre avant le premier champ du formulaire concerné. Il n'est pas nécessaire de la lier à chaque champ via l'attribut `aria-describedby`.

```html
<p>
    Tous les champs sont obligatoires sauf ceux marqués de la mention
    "facultatif"
</p>
<form>
    ...
    <label for="demo-input">Étiquette</label>
    <input id="demo-input" type=text" ... required> ...
</form>
```

Il convient alors de préciser le caractère facultatif des champs en l'écrivant en toute lettre dans l'élément `<label>` : `(facultatif)`

### Exemples de bonnes et mauvaises pratiques

La [documentation access42](https://disic.github.io/guide-integrateur/demo/6-formulaires/aides-controles-saisie.html) donne plusieurs exemples de bonnes et mauvaises pratiques ici.

### Cas particuliers : input cochables

Si le champ est un input cochable (radio, checkbox, switch), le caractère obligatoire ou facultatif est exprimé différement&nbsp;: [voir documentation dédiée](#caractère-requis).

## Champs et éléments disabled

Un élément de formulaire désactivé doit posséder l'attribut `disabled`.

Un bouton ou un élément de formulaire submit doit posséder l'attribut `aria-disabled="true"` et non l'attribut `disabled`. Ce dernier est à éviter dans ce cas car l'élément auquel il est appliqué disparait du flux d'éléments navigables au clavier. Ainsi, dans un formulaire, un bouton submit ayant l'attribut `disabled` ne sera pas atteignable au clavier et pourra donner l'impression d'un bug. [Article dédié au sujet sur css-tricks](https://css-tricks.com/making-disabled-buttons-more-inclusive/).

Pour donner un style à un élément ainsi désactivé, utiliser un sélecteur qui cible l'attribut `aria-disabled`.

## Faciliter la saisie

### Type

Renseigner l'attribut `type` permet d'apporter de l'information sur la valeur attendue dans le champ voir de complètement changer le comportement ou le style de l'input. Liste des [valeurs existantes](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input#les_diff%C3%A9rents_types_de_champs_input) pour l'attribut `type`.

```html
<label for="demo-input">Étiquette</label> <input id="demo-input" type=password"
name="password">
```

Bien qu'il existe beaucoup de valeurs pour l'attribut type, toutes ne sont pas recommandées en terme d'accessibilité&nbsp;:[voir documentation types de données particulières](#types-de-données-particulières).

### Format attendu

Si un format particulier est attendu, ce dernier **doit** être indiqué pour permettre une bonne complétion du champ. Il peut être présent dans le label ou dans un passage de texte associé. Pour une date on pourrait avoir&nbsp;:

```html
<label for="input-anniversaire">Date de naissance</label>
<input
    id="input-anniversaire"
    type="text"
    name="birthdate"
    aria-describedby="help-input-anniversaire"
/>
<p id="help-input-anniversaire">Format: 31/12/1991</p>
```

Dans certains cas, il est aussi possible d'avoir recours à un groupe d'inputs, pour préciser une unité par exemple (heures, euros, etc...). Comme pour l'aide, il faut le lier l'élément au champ grâce à `aria-describedby`.

### Autocomplete

L'attribut `autocomplete` permet au navigateur de suggérer des valeurs d'autocomplétions pour les champs de formulaire. Elles sont constituées des valeurs saisies précédemment par l'internaute, des valeurs enregistrées par le navigateur (type mot de passe, mail, etc...) ou encore par les gestionnaires de mots de passes.

Si la complétion d'un champ requiert des données de l'internaute pour être complété et qu'une valeur correspondante existe pour l'attribut `autocomplete`, ce dernier devient obligatoire pour faciliter la saisie (Voir [critère 11.13.1](https://www.numerique.gouv.fr/publications/rgaa-accessibilite/methode-rgaa/criteres/#test-11-13-1)). Liste des [valeurs d'autocomplete](https://developer.mozilla.org/fr/docs/Web/HTML/Attributes/autocomplete#valeurs).

### Fieldset

Les [champs de même nature](https://accessibilite.numerique.gouv.fr/methode/glossaire/#champs-de-meme-nature) sont regroupés dans un élément `<fieldset>` ([critère 11.5](https://accessibilite.numerique.gouv.fr/methode/criteres-et-tests/#11.5)). Exemple: identité, coordonnées, informations de paiement, etc... L'élément `<legend>` est obligatoire et donne une information textuelle sur le regroupement ([critère 11.6](https://accessibilite.numerique.gouv.fr/methode/criteres-et-tests/#11.6)).

```html
<fieldset>
    <legend>Titre du regroupement d'inputs</legend>
    ...
    <label for="demo-input">Étiquette</label>
    <input id="demo-input" type=text" ...> ...
</fieldset>
```

Si plusieurs champs apparaissent avec la même étiquette, les séparer dans des éléments `<fieldset>` différents est obligatoire. Par exemple, des fieldsets "adresse de facturation" et “adresse de livraison" vont tous les deux contenir des champs nom, prénom, adresse, rue, ville, etc... Malgré leurs labels similaires, leur finalité est différente.

```html
<fieldset>
    <legend>Adresse de facturation</legend>
    ...
    <label for="facturation-ville">Ville</label>
    <input id="facturation-ville" type=texte" ...> ...
</fieldset>
...
<fieldset>
    <legend>Adresse de livraison</legend>
    ...
    <label for="livraison-ville">Ville</label>
    <input id="livraison-ville" type=texte" ...> ...
</fieldset>
```

Une meilleure structuration du formulaire permettra une meilleure compréhension de ce dernier. Pour les inputs cochables, un élément `<fieldset>` est obligatoire à partir du moment ou il y a plus d'un choix (voir [documentation Checkbox, switch et radio](#checkbox-switch-et-radio)).

#### Informations complémentaires aux groupes de champs

Tout comme [pour les champs](#informations-sur-les-champs), il est possible d'apporter des informations complémentaires à un élément `<fieldset>`. Dans ce cas et pour des raisons de restitution (cf [article sur tenon](https://blog.tenon.io/accessible-validation-of-checkbox-and-radiobutton-groups/)), le texte doit figurer dans l'élément `<legend>`.

```html
<fieldset>
    <legend>
        Titre du groupe
        <span>Passage de texte</span>
    </legend>
    ...
</fieldset>
```

Il arrive que pour des besoins de styles, on souhaite avoir le passage de texte à la fin de l'élément `<fieldset>` après les inputs cochables. La solution est alors de masquer visuellement le passage de texte contenu dans l'élément `<legend>` via la classe `sr-only` et d'ajouter un bloc de texte contenant le même passage de texte et possédant l'attribut `aria-hidden="true"` à la fin de l'élément `<fieldset>`.

```html
<fieldset>
    <legend>
        Titre du groupe
        <span class="sr-only">Passage de texte</span>
    </legend>
    ...
    <p aria-hidden="true">Passage de texte</p>
</fieldset>
```

Soit le texte informatif doit être situé en `sr-only` dans la balise `<legend>` et doit apparaitre visuellement en `aria-hidden="true"` dans le fieldset (2eme option dixit Nicolas dixit Shirley)

## Types de données particulières

### Données numériques

Pour des questions d'accessibilité le type `number` n'est pas utilisé (voir [gitlab](https://git-scm.pole-emploi.intra/studio-pole-emploi/pole-webdesign/wikis/Guides/HTML/saisie-chiffres) et [article gov.uk](https://technology.blog.gov.uk/2020/02/24/why-the-gov-uk-design-system-team-changed-the-input-type-for-numbers/)). Il faut préférer `type="text"` avec les attributs suivants `inputmode="numeric" pattern="[0-9]*"`.

_Exemple&nbsp;: déclinaison de composant input email_

```html
<label for="input-demo">Nombre d'années d'experience</label>
<input id="input-demo" type="text" ... inputmode="numeric" pattern="[0-9]*" />
```

Pour éviter la validation HTML5 native, ajouter l'attribut `novalidate` sur l'élément `<form>`.

### Mot de passe et email

Pour le champ de type `password` ou `email`, ajouter les attributs suivants&nbsp;:

* `autocapitalize="none"`&nbsp;: Évite la transformation automatique de certaines lettres en majuscules pour les clavier virtuels ou les moyens de saisie orale ([doc autocapitalize MDN](https://developer.mozilla.org/fr/docs/Web/HTML/Global_attributes/autocapitalize))
* `autocorrect="off"`&nbsp;: Évite la correction automatique de Safari ([doc autocorrect MDN](https://developer.mozilla.org/fr/docs/Web/HTML/Element/input#autocorrect))
* `spellcheck="false"`&nbsp;: [doc spellcheck MDN](https://developer.mozilla.org/fr/docs/Web/HTML/Global_attributes/spellcheck))

Ces attributs évitent que le navigateur ne modifie le contenu de l'input lorsqu'il considère qu'il y a des fautes ou erreurs. S'il s'agit d'un email et que ce champ concerne les informations de l'internaute, renseigner l'attribut `autocomplete` avec la valeur `email`.

_Exemple&nbsp;: déclinaison de composant input mot de passe_

```html
<label for="input-pw">Mot de passe</label>
<input
    id="input-pw"
    type="password"
    ...
    autocapitalize="none"
    autocorrect="off"
    spellcheck="false"
/>
```

_Exemple&nbsp;: déclinaison de composant input email_

```html
<label for="input-pw">Email</label>
<input
    id="input-pw"
    type="email"
    ...
    autocapitalize="none"
    autocorrect="off"
    spellcheck="false"
/>
```

### Numéro de téléphone

Utiliser le type `tel` et ajouter l'attribut `inputmode="tel"`. Si ce champ concerne les informations de l'internaute, compléter avec l'attribut `autocomplete`, sa valeur dépendra du format de téléphone souhaité (avec ou sans indicateur de pays par exemple). [Exemple sans indicateur]({{ '/components/detail/input-alt--tel' | path }}) et [exemple avec indicateur]({{ '/components/detail/input-alt--tel-inter' | path }}).

```html
<label for="telephone-fr">Téléphone</label>
<input
    id="telephone-fr"
    type="tel"
    ...
    autocomplete="tel-national"
    inputmode="tel"
/>
```

### Heure et date

Ne pas utiliser les inputs natifs de type `date` ou `time` en raison d'incohérences dans la manière donc les technologies d'assistances interprètent ces champs ([support type date](https://a11ysupport.io/tech/html/input(type-date)_element) - [support type time](https://a11ysupport.io/tech/html/input(type-time)_element))

Pour faire simple, utiliser le `type="text"` avec un passage de texte pour laisser connaitre le format attendu. En fonction des cas présentés, certains attributs sont ajoutés pour aider la saisie.

Si le besoin d'un composant de sélection de dates est indispensable, il existe des solutions de scripts accessibles, voici un [article du site digita11y qui offre une liste exhaustive](https://www.digitala11y.com/accessible-datepickers-roundup/).

#### Heure

##### Champ heure unique

Utiliser le type `text` et ajouter un passage de texte associé indiquant le format attendu: "_Format 24h: hh:mm_" ou "_Exemple: 23:30_".

```html
<label for="input-heure">Horaire de départ</label>
<input id="input-heure" type="text" ... aria-describedby="help-input-heure" />
<p id="help-input-heure">Exemple: 23:30</p>
```

Il est possible (non obligatoire) de limiter la longueur de la valeur acceptée dans le champ avec l'attribut `maxlength`.

##### Champs heures multiples

Utiliser deux champs dédiés, un pour les heures et un pour les minutes. Ces champs possèdent les attributs suivants&nbsp;: `pattern="[0-9]*" inputmode="numeric"`. L'élément `<form>` possède l'attribut `novalidate` pour éviter la validation HTML native.

Les deux champs sont regroupés dans un élément `<fieldset>`, le contenu l'élément `<legend>` est explicite et donne une indication du format attendu, exemple: "_Format 24h_".

```html
<fieldset>
    <legend>Horaire de départ (format 24h)</legend>
    <label for="input-heure">Heures</label>
    <input
        id="input-heure"
        type="text"
        ...
        pattern="[0-9]*"
        inputmode="numeric"
    />
    <label for="input-minutes">Minutes</label>
    <input
        id="input-minutes"
        type="text"
        ...
        pattern="[0-9]*"
        inputmode="numeric"
    />
</fieldset>
```

#### Date

##### Champ date unique

Utiliser le type `text` et ajouter un passage de texte associé indiquant le format attendu: "_Format jour mois année_" ou "_Exemple: 22/03/1993_".

```html
<label for="input-heure">Date de départ</label>
<input id="input-heure" type="text" ... aria-describedby="help-input-heure" />
<p id="help-input-heure">Exemple: 22/03/1993</p>
```

Il est possible (non obligatoire) de limiter la longueur de la valeur acceptée dans le champ avec l'attribut `maxlength`.

##### Champs dates multiples

Utiliser trois champs dédiés, un pour le jour, un pour le mois et un pour les minutes. Ces champs possèdent les attributs suivants&nbsp;: `pattern="[0-9]*" inputmode="numeric"`. L'élément `<form>` possède l'attribut `novalidate` pour éviter la validation HTML native.

Les trois champs sont regroupés dans un élément `<fieldset>`, le contenu l'élément `<legend>` est explicite et donne une indication du format attendu, exemple: "_Format jour mois année_".

```html
<fieldset>
    <legend>Horaire de départ (Format jour mois année)</legend>
    <label for="input-day">Jour</label>
    <input
        id="input-day"
        type="text"
        ...
        pattern="[0-9]*"
        inputmode="numeric"
    />
    <label for="input-mois">Mois</label>
    <input
        id="input-mois"
        type="text"
        ...
        pattern="[0-9]*"
        inputmode="numeric"
    />
    <label for="input-annee">Année</label>
    <input
        id="input-annee"
        type="text"
        ...
        pattern="[0-9]*"
        inputmode="numeric"
    />
</fieldset>
```

## Checkbox, switch et radio

Les inputs de types `checkbox` ou `radio` permettent de proposer un choix unique ou un groupe à choix multiple. Il n'est pas nécessaire de regrouper plusieurs inputs cochables au sein d'éléments de listes html `<ul>` ou `<ol>`. Un groupe d'inputs cochables est toujours contenu dans un `<fieldset>` (voir [documentation Fieldset]({{ '/docs/generalites/formulaires#fieldset' | path }})).

> Considerant qu'un radio ne peut être décoché, si la question n'est pas obligatoire pour la validation du formulaire, ajouter une option "_Non_" ou "_Ne pas répondre_" à la liste des choix.

### Caractère requis

Le caractère requis est exprimé de manière différente en fonction de la présence d'un input cochable seul (checkbox ou switch, un radio ne peut par principe pas être seul), ou d'un groupe d'input cochables réunis au sein d'un `<fieldset>`.

#### Input seul

L'input cochable possède l'attribut `required`.

Si le caractère obligatoire de l'input cochable ne suit pas la logique globale du formulaire, une mention visuelle est présente dans le `<label>`&nbsp;:

##### Champs facultatifs par défaut

Sans indication, les champs d'un formulaire sont faculatifs par défaut. Dans ce contexte, un input cochable seul et obligatoire possède la mention "(obligatoire)" ou un indicateur visuel qui signale son caractère requis dans son `<label>`. Dans le même contexte, un input seul facultatif n'a pas besoin de mention supplémentaire.

```html
<p>Les champs marqués d'une étoile (*) sont obligatoires</p>
<form novalidate>
    <input id="input-demo" type="checkbox" ... required />
    <label for="input-demo"
        >J'ai lu et j'accepte les conditions générales *</label
    >
</form>
```

##### Champs obligatoires par défaut

Dans un formulaire où les champs sont obligatoires par défaut, un input cochable seul et obligatoire n'a pas besoin de mention supplémentaire. Dans le même contexte, un input seul facultatif possède la mention "(facultatif)" dans son élément `<label>`.

```html
<p>
    Tous les champs sont obligatoires sauf ceux marqués de la mention
    "facultatif"
</p>
<form novalidate>
    <input id="input-demo" type="checkbox" ... required />
    <label for="input-demo"
        >J'ai lu et j'accepte les conditions générales</label
    >
</form>
```

#### Groupe d'inputs

Les inputs cochables au sein d'un élément `<fieldset>` ne possèdent pas l'attribut `required` pour des raisons d'ambiguïté (est-ce qu'un choix est requis ou cet input en particulier ?).

Si le caractère obligatoire du groupe d'inputs cochables ne suit pas la logique globale du formulaire, une mention visuelle est présente dans l'élément `<legend>` du `<fieldset>`&nbsp;:

##### Group de champs facultatifs par défaut

Sans indication, les champs d'un formulaire sont faculatifs par défaut. Dans ce contexte, un groupe d'inputs obligatoires possède la mention "(obligatoire)" ou un indicateur visuel qui signale son caractère requis dans son `<legend>`. Dans le même contexte, un groupe d'inputs facultatif n'a pas besoin de mention supplémentaire.

```html
<p>Les champs marqués d'une étoile (*) sont obligatoires</p>
<form novalidate>
    <fieldset>
        <legend>Groupe d'inputs *</legend>
        ...
    </fieldset>
</form>
```

##### Groupe de champs obligatoires par défaut

Dans un formulaire où les champs sont obligatoires par défaut, un groupe d'inputs obligatoires n'a pas besoin de mention supplémentaire. Dans le même contexte, un groupe d'inputs facultatif a la mention "(facultatif)" dans la balise `<legend>`. Dans le même contexte, un groupe d'inputs facultatif possède la mention "(facultatif)" dans son élément `<legend>`.

```html
<p>
    Tous les champs sont obligatoires sauf ceux marqués de la mention
    "facultatif"
</p>
<form novalidate>
    <fieldset>
        <legend>Groupe d'inputs</legend>
        ...
    </fieldset>
</form>
```

### Informations sur les inputs cochables

#### Sur le groupe de choix

Voir documentation [informations complémentaires aux groupes de champs]({{ '/doc/formulaires#informations-complémentaires-aux-groupes-de-champs' | path }})

[Exemple dans le composant radio]({{ '/components/detail/radio--help-fieldset' | path }})

#### Sur un input cochable en particulier

Voir documentation [informations sur les champs]({{ '/docs/generalites/formulaires#informations-sur-les-champs' | path }})

[Exemple dans le composant radio]({{ '/components/detail/radio--help-input' | path }})

## Select

L'input `<select>` est un champ de formulaire qui fournit une liste d'`<option>`s parmi lesquelles l'internaute pourra choisir. Il est toujours obligatoirement constitué d'un champ et d'un label associé. De manière facultative il peut être accompagné d'un passage de texte d'aide, d'un message d'erreur ou de succès.

Il est possible de regrouper les options via l'élément `<optgroup>`. Cette dernière doit posséder l'attribut `label` complété de manière explicite. L'utilisation des groupes d'options est préconisée tant que deux groupes ou plus se distinguent. Les groupes sont en général déterminés en amont côté conception.

```html
<label for="select-demo">Choisissez une catégorie</label>
<select id="select-demo">
    <optgroup label="Films internationaux">
        <option>Action/aventure</option>
        ...
    </optgroup>
    <optgroup label="Films français">
        <option>Action/aventure</option>
        ...
    </optgroup>
</select>
```

Ce champ devrait être utilisé en dernier recours car il est compliqué à utiliser&nbsp;: La liste de choix est masquée et, si elle est longue, demandera de scroller. L'utilisation d'une liste de `radio` est une bonne alternative. Si le nombre de choix est trop important, affiner avec des questions préliminaires devrait permettre de les réduire. Le site [gov.uk](https://design-system.service.gov.uk/components/select/#research-on-this-component) fournit un lien vers une conférence donnant des retours sur ce élément de formulaire (en anglais): [Alice Bartlett: Burn your select tags](https://www.youtube.com/watch?v=CUkMCQR4TpY)

## Champs conditionnels

Certains choix requierent parfois des précisions. Il est possible d'ajouter un ou des champs conditionnels à un formulaire (_exemple: cocher un checkbox fait apparaitre un champ texte_).

D'après un [article sur le sujet](https://accessibility.blog.gov.uk/2021/09/21/an-update-on-the-accessibility-of-conditionally-revealed-questions/) sur le site gov.uk, il est possible d'[utiliser l'attribut `aria-expanded`](https://github.com/alphagov/govuk-frontend/issues/979#issuecomment-528932826) pour apporter de l'information sur l'état affiché ou masqué d'un élément associé. Cet attribut est mal supporté pour les rôles radio et checkbox mais ne dégrade pas pour autant le parcours de l'internaute. Gov.uk en conclut qu'il peut être utilisé car bénéfique pour une partie des internautes.

```html
<!-- Cocher la case "Email" déploie un champ caché -->
<input
    id="contact"
    type="checkbox"
    ...
    aria-controls="conditional-field"
    aria-expanded="true"
/>
<label for="contact">Email</label>
<!-- Champ caché par défaut et révélé si la case est cochée -->
<div id="conditional-field">
    <label for="input-pw">Email</label>
    <input id="input-pw" type="email" ...">
</div>
```

### Retours d'expérience de Gov.uk

Voici les recommandations de conception du site Gov.uk

* Masquer / afficher un seul champ à la fois (label et aides inclus).
* Masquer / afficher uniquement des champs (label et aides inclus).
* Garder l'interface simple
* Ne pas cacher / masquer quelque chose qui n'est pas un champ.

Voici les recommandations d'implémentations du site Gov.uk

* Attribut `aria-controls`&nbsp;: avec id du bloc déployé
* Attribut `aria-expanded`&nbsp;: sur l'élément de formulaire cochable. Non valide **mais** ne dégrade pas l'expérience
* Attribut `aria-live`&nbsp;: **exclu d'office** car bruyant et ne donne pas l'état initial du composant : lit juste le texte
* Optionnel&nbsp;: Passage de texte en aide ou texte dans le label "révèle du contenu"

<!--
Champs qui se valident automatiquement: Erreurs / succès dans une balise aria-live polite

Validation de form :

-   Donner de l'info dans le titre de la page
-   Error summary : https://design-system.service.gov.uk/components/error-summary/

-->

## Erreurs et validation

Pour éviter la validation HTML5 native, ajouter l'attribut `novalidate` sur l'élément `<form>`.

### Rendu des messages d'erreurs

Un champ en erreur possède l'attribut `aria-invalid="true"`. Le message d'erreur est situé dans l'élément `<label>` ou le passage de texte associé à l'`<input>`.

```html
<label for="input-demo">Étiquette</label>
<input
    id="input-demo"
    type="text"
    ...
    required
    aria-invalid="true"
    aria-describedby="error-input-demo"
/>
<p id="error-input-demo">Message d'erreur</p>
```

Dans le cas d'un regroupement d'inputs cochables au sein d'un élément `<fieldset>`, l'attribut `aria-invalid="true"` n'est pas utilisé car ambigu. Concernant l'implementation des messages d'erreur, se référer aux recommandations détaillées dans la partie ([informations complémentaires des groupes de champs]({{ '/docs/generalites/formulaires#informations-complémentaires' | path }})).

```html
<fieldset>
    <legend>Étiquette du groupe <span>Message d'erreur.</span></legend>
    <input type="radio" id="demo-radio1" ... value="yes" />
    <label for="demo-radio1">Oui</label>
    <input type="radio" id="demo-radio2" ... value="no" />
    <label for="demo-radio2">Non</label>
</fieldset>
```

### Types d'erreurs et informations nécessaires

#### Absence de saisie dans un champ obligatoire

L'erreur permet d'identifier nommément le champ et son caractère obligatoire

```html
<label for="input-demo">Prénom</label>
<input
    id="input-demo"
    type="text"
    ...
    required
    aria-invalid="true"
    aria-describedby="error-input-demo"
/>
<p id="error-input-demo">Entrez un prénom</p>
```

#### Type de données ou format

L'erreur permet d'identifier le champ concerné, fournit une indication du type de données ou du format attendu ainsi qu'un exemple de valeur attendue

```html
<label for="input-pw">Email</label>
<input
    id="input-pw"
    type="email"
    ...
    required
    aria-invalid="true"
    aria-describedby="error-input-demo"
/>
<p id="error-input-demo">
    Email non valide. Exemple de format valide&nbsp;: michel.grange@gmail.com
</p>
```

### Validation en cours de saisie

Il arrive que le front-end gère une partie de la validation des données au cours de la complétion d'un formulaire. Si c'est le cas l'élément HTML qui va accueillir le message d’erreur existe au préalable dans le DOM et possède les attributs `role=“status”` et `aria-live=“assertive”`.

```html
<label for="input-demo">Étiquette</label>
<input
    id="input-demo"
    type="text"
    ...
    required
    aria-invalid="true"
    aria-describedby="error-input-demo"
/>
<!-- Sans erreur, la balise existe dans le DOM, est masquée (sr-only, display: none;) -->
<p id="error-input-demo" role="“status”" aria-live="“assertive”"></p>
```

Le message d’erreur apparait lorsque le focus quitte le champ ou groupe de champs&nbsp;:

```html
<label for="input-demo">Étiquette</label>
<input
    id="input-demo"
    type="text"
    ...
    required
    aria-invalid="true"
    aria-describedby="error-input-demo"
/>
<!-- Le message d'erreur est injecté, l'élément est affiché visuellement -->
<p id="error-input-demo" role="“status”" aria-live="“assertive”">
    Message d'erreur
</p>
```

### Validation de formulaire et résumé des erreurs

Si la validation d'un formulaire entraine des erreurs, les modifications suivantes sont attendues dans la page&nbsp;:

La balise `<title>` de la page commence par le texte `“Erreur“`

Un bloc en début de page annonce le nombre d'erreurs du formulaire. Ce bloc devrait être le premier élément contenu dans la balise `<main>` de la page. Il peut apparaitre après le fil d’Ariane ou le lien de retour à la page précédante si ces derniers se trouvent dans la balise `<main>`.

Il possède l'attribut `role="alert"` et l'attribut `tabindex="-1"` Au chargement de la page, le focus est placé sur ce bloc via JavaScript. Le bloc contient le nombre d'erreurs présentes dans le formulaire et un élément `<a>` contenant une ancre vers le premier champ en erreur&nbsp;:

```html
<div class="alert alert-danger" tabindex="-1" role="alert">
    <strong>X erreurs ont été detectées.</strong> Merci de consulter les champs
    avec une indication en erreur.
    <a href="#input-demo">Aller au premier champ en erreur</a>.
</div>
...
<!-- Formulaire plus loin dans la page -->
<form novalidate>
    ...
    <label for="input-demo">Étiquette</label>
    <input
        id="input-demo"
        type="text"
        ...
        required
        aria-invalid="true"
        aria-describedby="error-input-demo"
    />
    <p id="error-input-demo">Message d'erreur</p>
    ...
</form>
```

Si le premier champ en erreur dans la page est contenu dans un élément `<fieldset>`, l'ancre pointe sur le premier champ en erreur dans le regroupement.

```html
<div class="alert alert-danger" tabindex="-1" role="alert">
    <strong>X erreurs ont été detectées.</strong> Merci de consulter les champs avec une indication en erreur.
    <a href="#input-demo">Aller au premier champ en erreur</a>.
</div>
...
<!-- Formulaire plus loin dans la page -->
<form novalidate>
    ...
    <fieldset>
        <legend>Étiquette du groupe</legend>
        <label for="input-demo">Étiquette</label>
        <input id="input-demo" type="text" ... required aria-invalid="true" aria-describedby="error-input-demo">
        <p id="error-input-demo">Message d'erreur</p>
    ...
</form>
```

Si le premier champ en erreur dans la page est contenu dans un élément `<fieldset>` et est une liste d'éléments cochables, l'ancre pointe sur le premier choix disponible.

```html
<div class="alert alert-danger" tabindex="-1" role="alert">
    <strong>X erreurs ont été detectées.</strong> Merci de consulter les champs
    avec une indication en erreur.
    <a href="#demo-radio1">Aller au premier champ en erreur</a>.
</div>
...
<!-- Formulaire plus loin dans la page -->
<form novalidate>
    ...
    <fieldset>
        <legend>Étiquette du groupe <span>Message d'erreur.</span></legend>
        <input type="radio" id="demo-radio1" ... value="yes" />
        <label for="demo-radio1">Oui</label>
        <input type="radio" id="demo-radio2" ... value="no" />
        <label for="demo-radio2">Non</label>
    </fieldset>
    ...
</form>
```

Ces consignes ne font pas l'objet de critères dédiés dans le RGAA, mais elles permettent cependant de grandement améliorer la navigation dans les pages qui contiennent des erreurs de formulaires.

### Résumé des erreurs proposé par le W3C

Dans son design system, le w3c met en avant un [résumé des erreurs](https://design-system.w3.org/styles/forms.html#error-messages)</a> bien plus fourni&nbsp;:

* Le bloc est un des premiers éléments contenu dans la balise `<main>` de la page. Il peut apparaitre après le fil d’Ariane ou le lien de retour à la page précédante si ces derniers se trouvent dans la balise `<main>`. Il est conseillé de le placer avant le `<h1>` de la page si ce dernier se trouve dans l'élément `<main>`.

* Ce bloc possède l’attribut `tabindex=“-1”` et reçoit le focus au chargement de la page.

* Le bloc contient un titre de niveau `<h2>` dont le contenu est "Une erreur est survenue". Ce titre sert de nom accessible au bloc de résumé des erreurs&nbsp;: Le bloc possède l’attribut `aria-labelledby` avec pour contenu, l’`id` de l'élément `<h2>`titre.

* Le bloc contient une liste des erreurs présente dans le formulaire. Chaque erreur listée est un élément de lien `<a>` dont l'attribut `href` est une ancre qui permet d'atteindre le champ concerné.

* L'intitulé visible de chaque erreur de la liste correspond au texte visible du message d’erreur du champ vers lequel il pointe.

```html
<div role="alert" tabindex="-1" aria-labelledby="error-summary-title">
    <h2 id="error-summary-title">Une erreur est survenue</h2>
    <ul>
        <!-- L'intitulé visible reprend le message d'erreur  -->
        <li><a href="#input-firstname">Entrez un prénom</a></li>
        ...
    </ul>
</div>
...
<!-- Formulaire plus loin dans la page -->
<form novalidate>
    ...
    <label for="input-firstname">Prénom</label>
    <input
        id="input-firstname"
        type="text"
        ...
        required
        aria-invalid="true"
        aria-describedby="error-input-firstname"
    />
    <p id="error-input-firstname">Entrez un prénom</p>
    ...
</form>
```

Pour plus de détails et d'exemples, consulter la [documentation du design system w3c](https://design-system.w3.org/styles/forms.html#error-messages)</a>.
