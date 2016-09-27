# Guidelines pour CSS — ITCC (Block, Element, Modifier)

ITCC est une méthodologie de gestion de projets (à l’échelle du CSS). Dans le [chapitre sur BEM](bem.md), un certain nombre de points concernant les problèmes inhérents à la structure même du CSS étaient mis en avant, et BEM y est présenté comme une méthodologie permettant d’y répondre éfficacement. ITCSS est une méthodologie permettant d’organiser son CSS efficacement, à l’échelle de tout un projet, et se combine parfaitement avec BEM et les préprocesseurs.

## Organisation : Triangle inversé

![ITCSS](https://images.emmanuelbeziat.com/Managing_CSS_Projects_with_ITCSS____Speaker_Deck_et_8_pages_suppl%C3%A9mentaires_%E2%80%8E-_Microsoft_Edge-wb3j7-laco6.jpg)

Ce diagramme représente les différentes couches utilisables, des plus génériques aux plus spécifiques (lourdes) :
* **Settings:** Variables globales, configuration
* **Tools:** Mixins, fonctions
* **Generic:** Le niveau zéro des styles (normalize, box-sizing, etc.)
* **Base:** Les éléments CSS basiques, sans classes (les sélecteurs types)
* **Objects:** Les éléments de design sans "cosmétique" (grids)
* **Components:** Éléments de design, d’interface (UI)
* **Trumps:** Helpers et surcouches

### Settings

Paramètres généraux, configuration (dev / prod), couleurs, etc.

```stylus
$color-brand = #fa0000
$font-size-heading = 2rem
```

### Tools

Mixins, fonctions et outils globaux

```stylus
font-brand()
	font-familiy "Segoe UI", arial, sans-serif
	font-weight 700
```

### Generic

Spécificité la plus basse possibile (normalize, resets, etc.).

```css
* {
	box-sizing: border-box;
}
```

### Base

Éléments html sans classes (liens, titres, etc.). C’est la dernière couche dans laquelle on placera des sélecteurs de type (`a {}`, `blockquote {}`, etc.)

```css
a {
	text-decoration: none;
}

ul {
	list-style: square outside;
}
```

### Objects

_design pattern_, sans cosmétique. Composé uniquement de classes, nommés de façon agnostique (`.ui-list {}`).

```css
.ui-list {
	margin: 0;
	padding: 0;
	list-style: none;
}

.ui-list__item {
	padding: 10px;
}
```

### Components

Éléments de design, toujours uniquement composés de classes. Nommage plus spécifique (`.product-list {}`).

```css
.products-list {
	font-size: 1.25rem;
	border-top: 1px solid #fa0000;
}

.products-list__item {
	border-bottom: 1px solid #fa0000;
}
```

### Trumps

Éléments utilitaires, qui n’affectent qu’un seul élément du DOM à la fois. On l’utilisera généralement pour les classes "helpers".

```css
.sr-only {
	width: 1px !important;
	height: 1px !important;
	position: absolute !important;
	opacity: 0 !important;
	visibility: hidden !important;
}
```

## Spécificité

La spécificité augmente petit à petit à mesure qu’on descend dans les couches, en affectant des parties du DOM de plus en plus petites. On ajoute progressivement des styles, on évite d’en retirer.

En clair, ITCSS permet de garder un contrôle sur la cascade et l’héritage. Il permet à chacun de savoir où se trouvent les éléments, et réduit le gâchis et la redondance. De fait, il augmente aussi le potentiel de réutilisation, de modularité, et d’amélioration (_scalability_).

