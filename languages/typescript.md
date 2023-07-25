# Premiers pas en TypeScript

[← Retour à l'accueil](/README.md)

Infos issues de la [formation TypeScript](https://grafikart.fr/formations/typescript) du bro Grafikart. 💜

## Installation

Lancer la commande `npm install typescript -D`.

## Compiler

- `npx tsc nom-du-fichier`: compile le fichier `.ts` en fichier `.js` dans le répertoire courant
- `npx tsc nom-du-fichier --outDir nom-du-repertoire`: compile le fichier `.ts` en fichier `.js` dans le répertoire visé
- `npx tsc ... --watch`: flag qui permet à la commande d'observer les modifications de notre code

Ces commandes servent s'il n'y au aucun fichier de configuration `tsconfig.json` présent à la racine du projet. Si un fichier de configuration de TS est présent:

- `npx tsc (--watch)`: va lancer typescript selon la configuration précisée

## tsconfig.json

- `compilerOptions`: objet des paramètres de compilation
  - `outDir`: correspond à l'option `--outDir`. Répertoire de sortie
  - `target`: version de JS vers laquelle le fichier est compilé
  - `noEmitOnError`: ne compile pas le code en cas d'erreur,
  - `strict`: plus haut niveau d'exigeance de TS ([doc](https://www.typescriptlang.org/tsconfig#strict))
- `files`: tableau des objets à compiler

## Typer correctement

### Les types de base

```typescript
const s:string = 'Hello world'
const n:number = 42
const b:boolean = false
const d: null = null
const arr: string[] = ['hello', 'world']
const user: { firstname: string, lastname?: string } = { firstname: 'John', lastname: 'Doe (optionnel)' }
```

### Les objets

```typescript
// Objet moins précis: pattern de clés et valeurs string
const user: { [key: string]: string } = { firstname: 'John', lastname: 'Doe (optionnel)' }
// Type objets spécifiques utilisables par défaut (MouseEvent, HTMLInputElement, ...)
const date: Date = new Date()
```

### Les fonctions

```typescript
// Typage de la fonction et du paramètre
const cb: Function = (e: MouseEvent) => { ... }
function printId(id: number) { ... }

// Typage du retour
// `void` ~ne retourne rien~ le retour n'est pas utilisé
const cb: Function = (e: MouseEvent): void => { ... }
// autre écriture
const cb: (e: MouseEvent) => void = (e) => { ... }
```

### Laisser TS déduire

Si on ne type pas, TS va comprendre tout seul les types des variables qui ont déjà une valeur assignée.

⚠️ Attention : quand une variable constante est définie avec une valeur, le type automatique ne sera pas le type de la valeur mais la valeur elle même. Il s'agit d'un [literal](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-types).

### Type assertion

Parfois le type déduit par TS est limité car on sort de sa portée.

```typescript
// Interprété comme type Element. TS ne connait pas l'élément qui possède cet Id
const elem = document.querySelector('#some-id')
```

On utilise l'affirmation de type ([type assertion](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-assertions)) pour forcer le type d'un variable (en restant dans la logique de ce que TS comprends).

```typescript
// Permet d'être plus spécifique
const elem = document.querySelector('#some-id') as HTMLButtonElement
const elem = <HTMLButtonElement>document.querySelector('#some-id')
```

⚠️ Attention : l'affirmation de type a aussi pour effet d'écarter les possibilités que le type soit null. Dans notre exemple, ça revient à dire que l'élément existe à 100% dans le code.

### Union

Le [type union](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-assertions) éfinit plusieurs possibilité quant au type attendu. S'écrit avec des types spéparés du caractère pipe `|`.

```typescript
function printId(id: number | string) { ... }
```

## Type narrowing

L'écriture de notre code permet à TypeScript de déduire certaines informations sur l'état du type de nos variables.

```typescript
// type HTMLSpanElement | null | undefined
const span = counter?.querySelector('span')

if (span) {
  // type HTMLSpanElement uniquement
  span.innerText = i.toString()
}
```

S'applique aussi aux "union types"

```typescript
function printId(id: string | number) {
  if (typeof id === "string") {
    // TS déduit le type string uniquement
  } else {
    // TS déduit le type number uniquement
  }
}
```

## Alias et Generics

### Alias

Pour ne pas se répéter, il est possible de déclarer des types qui vont servir d'alias.

```typescript
type User = { firstname: string, lastname: string }
const user: User = { firstname: 'John', lastname: 'Doe' }
```

Un type peut dépendre ou être déduit d'un autre d'un autre.

```typescript
type User = { firstname: string, lastname: string }
type P = keyof User

const firstname: P = 'lastname' // ok
const lastname: P = 'hello' // not ok

type Username = User['firstname'] // déduit le type string
```

Il est possible de déduire le type depuis une variable. On réservera cet usage dans des cas très particuliers, l'intérêt de TS étant de typer en amont.

```typescript
const newUser = {
  firstname: 'Jane',
  lastname: 'Doe',
  age: 42
}

// Déduit { firstname: string, lastname: string, age: number }
type newUser = typeof newUser
```

### Generics

Les generics permettent de donner des "paramètres" à nos types.

```typescript
function identity<T>(arg: T): T { ... }

// type number appliqué au paramètre et au retour
const id = identity<number>(3)

// pas de type précisé, TS va déduire 3 comme type
const id = identity(3)
```

Il est possible de créer des alias qui contiennent des generics.

```typescript
type Identity<T> = (arg: T) => T


function identity: Identity (arg) { ... }
```

Les generics permettent d'étendre le type générique définit pour qu'il conprenne d'autres paramètres

```typescript
function consoleSize<T extends { length: number }>(arg: T): T {
  console.log(arg.length)
  return arg
}

const arrr = consoleSize([ 2, 3 ])
```

## Documentation TypeScript

- [Documentation globale](https://www.typescriptlang.org/docs/).
- [Documentation tsconfig](https://www.typescriptlang.org/tsconfig).
