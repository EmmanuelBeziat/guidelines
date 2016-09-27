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