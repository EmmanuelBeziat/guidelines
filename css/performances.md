# Guidelines pour CSS — Performances

## Transitions

Certaines propriétés sont peu gourmandes à animer. C’est le cas pour `opacity`, `transform`, `color`, `background-color`… D’autres en revanche, sont plus lourdes et gourmandes en ressourcz, et le calcul de chaque état intermédiaires de la transition est tout aussi lourd à faire. C’est notamment le cas de toute modification sur le flux (`margin`), ou des propriétés lourdes à calculer de base (`filter`);

Dans certains cas (par exemple sur mobile, ou sur des configurations trop modestes), ces animations peuvent s’avérer très lourdes, saccader, voire entrainer un blocage.

Pour pallier à ça, si vraiment il est impossible de faire autrement, on peut avoir recours à la propriété `will-change`, qui va permettre de précalculer l’animation avant qu’elle ne survienne. **Il est très important de ne pas abuser de cette propriété**.

Exemple :
```css
div:hover {
	transition: .2s ease;
	margin-left: 50px;
	will-change: margin-left;
}
```

## @font-face

Il est recommandé de ne pas imposer de chargement aux anciens navigateurs. Privilégiez le woff2 et le woff, et gardez l’astuce du #iefix. Il est également recommandé d’éviter le format svg.

Enfin, la valeur `locale` permet de vérifier si une typo est présente sur l’ordinateur du visiteur, lui épargnant une requête http et un chargement si celle-ci est trouvée.

Déclaration optimale :
```css
@font-face {
	font-family: "Source Sans Pro";
	src: locale("Source Sans Pro Regular"),
		 url("fonts/source-sans-pro.woff2?#iefix") format("woff2"),
		 url("fonts/source-sans-pro.woff") format("woff");
}
```

De plus, les convertisseurs tels que FontSquirrel ne permettent pas de regrouper automatiquement des polices par familles, mais il est fortement recommandé de le faire.

Pas bien :
```css
@font-face {
	font-family: "matypo_regular";
	src: url("fonts/matypo_regular.woff2?#iefix") format("woff2"),
		 url("fonts/matypo_regular.woff") format("woff");
}

@font-face {
	font-family: "matypo_bold";
	src: url("fonts/matypo_bold.woff2?#iefix") format("woff2"),
		 url("fonts/matypo_bold.woff") format("woff");
}
```

Bien :

```css
@font-face {
	font-family: "matypo";
	src: url("fonts/matypo_regular.woff2?#iefix") format("woff2"),
		 url("fonts/matypo_regular.woff") format("woff");
}

@font-face {
	font-family: "matypo";
	src: url("fonts/matypo_bold.woff2?#iefix") format("woff2"),
		 url("fonts/matypo_bold.woff") format("woff");
	font-weight: bold;
}
```

Ainsi, on n’a pas à appeler une police spéficique sur un élément juste parce que la graisse change ; juste à utiliser la propriété `font-weight` comme avec n’importe quelle font dite websafe. Même chose avec l’italique.

## Propriétés raccourcies

Pas bien :
```css
div {
	padding-top: 5px;
	padding-right: 0;
	padding-bottom: 10px;
}
```

Bien:
```css
div {
	padding: 5px 0 10px;
}
```

Pas bien :
```css
div {
	border-radius: 5% 5% 5% 5%;
}
```

Bien :
```css
div {
	border-radius: 5%;
}
```

## Unités

Les unités doivent (presque) toujours être précisées, afin d’éviter de gros problèmes d’interprétation par le navigateur, à l’exception de `line-height` qui est automatiquement en `em`. L’unité est inutile si la valeur est 0.

Pas bien :
```css
h2 {
	margin: 0px;
	font-size: 0.8em;
	line-height: 2em;
	border: none;
}
```

Bien:
```css
h2 {
	margin: 0;
	font-size: .8em;
	line-height: 2;
	border: 0;
}
```

## Préfixes vendeurs

Utiliser autoprefixer (via un task-runner), plutôt que de le faire à la main.

Dans l’éventualité d’un code à rédiger à la main, il faut vérifier [quelles propriétés ont besoin d’être préfixées, et avec quels préfixes](https://www.emmanuelbeziat.com/blog/prefixes-css-jusqua-quand/).

La propriété non-préfixée doit **toujours** se trouver après les versions préfixées.
