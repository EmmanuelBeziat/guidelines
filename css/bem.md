# Guidelines pour CSS — BEM (Block, Element, Modifier)

BEM est une syntaxe CSS conçue pour résoudre tous les problèmes de maintenabilité du CSS, inhérents au langage lui-même.

## Quelques problèmes de CSS

### Régression

```css
.item {
	display: block;
	color: green;
	font-size: 1rem;
}

.contexte .item {
	display: inline-block;
	color: red;
}
```

Si maintenant quelqu’un apporte une modification :

```css
.item {
	display: block;
	color: green;
	font-size: 1rem;
	border: 1px solid green;
}

.contexte .item {
	display: inline-block;
	color: red;
}
```

J’obtiens donc une régression dans `.contexte .item`, qui va obliger à ajouter une propriété supplémentaire afin de la corriger. En clair, à chaque changement minime dans le CSS, le risque d’impact sur l’ensemble du site est présent.

### Priorité

En CSS, il est impossible de définir une priorité sur une classe, par exemple en choisissant son ordre d’attribution dans le html comme suit :
```html
<div class="red blue">text</div>
<div class="blue red">text</div>
```

C’est l’ordre de la déclaration dans le CSS qui défini la priorité quoiqu’il arrive.

```css
.blue {
	color: blue;
}

.red {
	color: red;
}
```

Dans les deux cas, le texte sera affiché en rouge.

Le problème se retrouve complexifié avec un préprocesseur :

```sass
.blue {
	color: blue;
}

.red {
	color: red;
}

.mon-texte {
	@extend .red;
	@extend .blue;
}
```

Même si on défini `.red` avant `.blue` dans la classe `.mon-texte`, c’est la déclaration des classes au-dessus qui prime, le texte sera donc toujour rouge.

Le problème se pose également lorsqu’on veut moduler un peu son CSS grâce aux classes atomiques (une fausse bonne idée), par exemple avec des media-queries ou du Javascript :

```css
.relative {
	position: relative;
}

.absolute {
	position: absolute;
}

.static {
	position: static;
}
```

Si on ajoute une classe `.relative` à un élément ayant déjà la classe `.static`, ça ne fonctionnera pas car `.static` est défini avant `.relative`.

## BEM répond à ces problèmes

La solution est de définir des classes autonomes et explicites.

Classes autonomes :
```html
<article class="article">
	<h3 class="title">My title</h3>

	<div class="action-zone">
		<h4 class="title important">Action Title</h4>

		<button class="important">Button</button>
	</div>
</article>
```

Classes autonomes et explicites :
```html
<article class="article">
	<h3 class="article-title">My title</h3>

	<div class="action-zone">
		<h4 class="action-zone-title title-important">Action Title</h4>

		<button class="button-important">Button</button>
	</div>
</article>
```


**BEM** est une convention de nommage pour ces classes, dont la syntaxe est la suivante :

```
block-name[__element-name][--modifier-name]
```

Un excellent exemple vallant mieux que mille mots, voici un exemple de structure BEM :
```css
.humain {
	taille: 169cm;
	peau: #e1cbb9;
}

.humain__main {
	doigts: 5;
	décoration: ongles;
}

.humain__main--gauche {
	pouce: gauche;
}

.humain__main--droite {
	pouce: droit;
}
```

Ces classes sont très explicites, ce qui permet de savoir directement à quoi elles servent et correspondent sans devoir se référer au html. De plus, on supprime ainsi tous les risques de régression et de priorité évoqués plus haut.

Ainsi, l'exemple plus haut devient comme suit :
```html
<article class="article">
	<h3 class="article__title">My title</h3>

	<div class="action-zone">
		<h4 class="action-zone__title action-zone__title--important">Action Title</h4>

		<button class="button button--important">Button</button>
	</div>
</article>
```

## Comment BEM améliore le CSS ?

Grâce à BEM, on évite les "fuites" (régressions). Par exemple :

```html
<article class="article">
	<h3 class="title">My title</h3>

	<div class="action-zone">
		<h4 class="title important">Action Title</h4>
```
```css
.article .title {
	margin-top: 20px;
}
```

Les deux titres hériteront tous les deux du margin, à moins de définir un sélecteur de plus… Plus de problème avec BEM.

De plus, on obtient une meilleure séparation du markup :

```html
<input class="button">
<a class="button">
<button class="button">
```

```css
.button {
	color: blue;
}
```

Ou encore :
```html
<h1 class="article__title">
<h2 class="article__title">
<div class="article__title">
```

```css
.article__title {
	font-size: 2em;
}
```

Aucun risque donc si mon html change (il est fréquent que les titres changent suite au passage d’un expert SEO, par exemple).

Enfin, le poids des déclarations reste constant et donc facilement surchargeable (et donc facilement maintenable) :

```css
/* normalize.css */
a {
	background: transparent;
}

/* button.css */
.button {
	background: #3787ac;
}

.button--important {
	background: tomato;
}

/* theme/buttons.css */
.button--important {
	background: #a00000;
}
```

## Quelques règles d’écriture

### Un seul élément

BEM signifie `Block__Element--modifier` ; pas `Block__Element__Element--modifier`. Pas plus d’un élément par déclaration donc.

Cela pose parfois des problèmes de nommage pour ceux qui débutent avec BEM. Mais BEM n’étant pas dépendant de l’architecture HTML, il n’y a aucune obligation de conserver un système de hiérarchie dans le CSS.

Pas bien :
```html
<div class="card">
	<div class="card__header">
		<h2 class="card__header__title">Title text here</h2>
	</div>

	<div class="card__body">

		<img class="card__body__img" src="some-img.png" alt="description">
		<p class="card__body__text">Lorem ipsum dolor sit amet, consectetur</p>
		<p class="card__body__text">Adipiscing elit.
			<a href="#" class="card__body__text__link">Read more</a>
		</p>

	</div>
</div>
```

Bien :
```html
<div class="card">
	<div class="card__header">
		<h2 class="card__title">Title text here</h2>
	</div>

	<div class="card__body">

		<img class="card__img" src="some-img.png" alt="description">
		<p class="card__text">Lorem ipsum dolor sit amet, consectetur</p>
		<p class="card__text">Adipiscing elit.
			<a href="#" class="card__link">Read more</a>
		</p>

	</div>
</div>
```

En clair, tous les descendants d’un bloc ne sont affectés que par leur appartenance à ce bloc, pas à l’élément dans lequel ils se trouvent.
De fait, je peux modifier complètement la structure de ce html, en déplaçant l’image par exemple, sans avoir à revenir sur le CSS.

### Cross-components

Il n’y a aucun problème non plus à exploiter des classes BEM provenant d’un autre composant.

```css
<div class="card">
    <div class="card__header">
        <h2 class="card__title">Title text here</h2>
    </div>

    <div class="card__body">

        <img class="card__img" src="some-img.png" alt="description">
        <p class="card__text">Lorem ipsum dolor sit amet, consectetur</p>

		<!-- classes provenant d’un autre composant -->
        <button class="button button--primary">Click</button>
    </div>
</div>
```

### Grand nombre de classes

La syntaxe BEM nécessite d’appliquer un grand nombre de classes dans le html (mais jamais autant que le css atomique), parfois avec un nom un peu long. Mais les avantages contrebalancent largement ce problème. Du reste, rien n’oblige à appliquer une classe à un élément s’il n’a pas un rendu spécifique.

Ainsi, inutile d’appliquer des classes sur des `<p>`, à moins que l’un ait un style particulier.

Enfin, attention lorsqu’on laisse la main à un utilisateur (par exemple en utilisant un CMS) : il faut prendre en compte que tous les éléments qui seront intégrés dans les textes "manuels" ne pourront comporter aucune classe. Il conviendra donc de les styliser à l’ancienne.

## Bonus

Vous pouvez même utiliser BEM pour vos noms de fichiers : `PDF___Facture--2016-06.pdf`, `MonSite__Homepage--v2.psd` !
