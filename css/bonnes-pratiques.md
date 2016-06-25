# Guidelines pour CSS — Bonnes pratiques

## Modèle de boite

Si le projet permet de coder pour Internet Explorer 8 *a minima*, exploiter le modèle de boite `border-box` en ajoutant ceci au début du fichier CSS :

```css
* {
	box-sizing: inherit;
}

html {
	box-sizing: border-box;
}
```

Cela permet à la propriété `width` de prendre en compte les `padding` et `border` d‘un élément, et évite donc les [dépassements inutiles](http://codepen.io/EmmanuelBeziat/pen/ryhaC), les calculs préalables ou à la volée…

## Flux

Éviter de sortir les éléments du flux autant que possible.

Pas bien :
```css
div {
	float: left;
	width: 100%;
	clear: both;
}
```

Bien:
```css
div {
	float: none;
}
```

Pas bien :
```css
div {
	position: absolute;
	right: 0;
}

/* ou */

div {
	float: right;
}
```

Bien :
```css
div {
	margin-left: auto;
}
```

Si on est sur un projet "*navigateurs modernes*", alors le module **flexbox** résoudra la majorité des problèmes qui nécessitaient auparavant l‘emploi hasardeux de `position: absolute;`.


## Positionnement

Utiliser les méthodes de positionnement dans cet ordre de préférence :

1. `display: block | inline;`
2. `display: flex | inline-flex;`
3. `display: inline-block | table-cell;`
4. `float: left | right;`
5. `position: relative | absolute | sticky | fixed;`

Dans le meilleur des mondes, chaque type a un rôle bien précise :

* Le layout et les grid sont faits avec le module `grid-layout` (bientôt exploitable, mais pour l‘instant faire avec `flexbox`).
* Les mises en page complexe interne (formulaires, boites de même hauteur, etc.) se font avec le module `flexbox`.
* Les icônes, images et autres petits éléments alignés se font via `display: inline-block;`
* `float` ne sert qu‘à ce pour quoi il a été conçu : avoir une image "au milieu" du texte

## Déclarations

### Déclarations légères

Ne jamais utiliser d‘ID dans le CSS. Les classes et les sélecteurs d’attributs suffisent à couvrir la très large majorité des cas. Et si on doit quand même cibler un ID, utiliser le sélecteur d’attribut :

```css
[id="monId"] {
	color: red;
}
```

Ceci pour une question de [poids des déclaration](https://www.emmanuelbeziat.com/blog/principes-du-css-poids-des-declarations/).

Des déclarations légères sont la clé d‘un CSS propre, puissant, réutilisable et maintenable. Un "poids" maximum de 20 est une bonne limite, un poids de 10 (une classe ou un sélecteur d‘attributs est une bonne moyenne).

De la même façon, moins une déclaration est spécifique, plus elle est pratique et facile à surcharger en cas de besoin.

Pas bien :
```css
input[type="submit"] {}
```

Bien :
```css
[type="submit"] {}
```

Ainsi, je n‘ai pas à me soucier que mon élément soit un `input`, un `button`, ou n‘import quel élément fantaisiste qui ne devrait pas être là.

### Déclarations de structure

De manière générale, il faut éviter une déclaration qui serait trop dépendante d‘une structure html rigide (pour la simple et bonne raison que le moindre changement dans le html peut entrainer de gros chamboulements dans le CSS).

Pas bien :
```css
article > h1 + p {
}
```

Bien :
```css
.article-intro {
}
```

## Factorisation

Il est utile, lisible (et plus propre) de rassembler les propriétés identiques sur des éléments similaires.

Pas bien :
```css
div::before {
	content: "";
	position: absolute;
	top: 5%;
	background: #fff;
}

div::after {
	content: "";
	position: absolute;
	top: 20%;
	background: #fff;
}
```

Bien :
```css
div::before,
div::after {
	content: "";
	position: absolute;
	top: 5%;
	background: #fff;
}

div::after {
	top: 20%;
};
```

## Surcharges

Éviter de créer des règles pour annuler des règles précédentes.

Pas bien :
```css
li {
	display: none;
}

li:first-child {
	display: block
}
```

Bien :
```css
li + li {
	display: none;
}

/* ou */

li:not(:first-child) {
	display: none;
}
```
