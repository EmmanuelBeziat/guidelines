# Guidelines pour CSS — Nomenclature des classes

Il existe différentes nomenclatures pour s’y retrouver dans son CSS. Certaines sont totalement compatibles avec [BEM](bem.md).

## Préfixes

L’une de ces nomenclatures propose d’ajouter un préfixe (souvent limité à une voire deux lettres) avant chaque classe « utilitaire ».

### Exemples

| Type | Classe | Exemple |
| - |:-: | -: |
| Typographique | `t-` | `t-title` |
| Helpers | `h-` | `h-align-right` |
| État | `is-` | `is-hidden` |
| Possession d’attributs | `has-`  | `has-submenu` |
| Classe dédiée à Javascript | `js-` | `js-slider` |

Ces préfixes peuvent parfaitement coïncider avec la méthodologie [ITCSS](itcss.md).

## Chaînage de _modifiers_

Par défaut, la syntaxe de BEM peut se révéler lourde à l’écriture si on cummule plusieurs _modifiers_. L’idée consiste à faire varier *BEM* vers ce qui pourrait être *BEVM* :

```
block-name[__element-name][--variation-name] -modifier
```

```html
<input class="input input--full-width input--string">
```

Il existe des nomenclatures plus pratiques pour leur nommage (et en plus, compatible avec le _nesting_ des [préprocesseurs](preprocesseurs.md) :

```html
<input class="input -full-width -string">
```

Ce qui se traduirait dans un préprocesseur comme suit :

```scss
.input {
	&.-full-width { }
	&.-string { }
}
```

Ce qui permet de garder un CSS propre tout en exploitant la puissance du _nesting_.