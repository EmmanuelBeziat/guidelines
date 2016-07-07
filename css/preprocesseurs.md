# Guidelines pour CSS — Préprocesseurs

## BEM quand même !

L’utilisation d’un préprocesseurs ne doit pas empêcher le maintient des bonnes pratiques, notamment l’usage de [BEM](bem.md) et des règles qui l’accompagnent : des déclarations les plus courtes possibles, limitées à deux classes maximum. Le *nesting* (le fait de pouvoir imbriquer les déclarations) doit se faire avec parcimonie.

Pas bien :
```less
.maClasse {
	color: blue;

	.monBloc {
		color: red;
	}
}
```

Bien :
```less
.maClasse {
	color: blue;
}

.monBloc {
	color: red;
}
```

On ne réservera le *nesting* qu’aux cas des pseudo-classes (`:hover`, `:focus`, `:active`) ou des pseudo-élements `::before` et `::after`.

## De l’importance des variables

L’un des principaux intérêts d’utiliser un préprocesseur, c’est de pouvoir avoir recours à l’utilisation de variables. De fait, lorsque vous codez, **gardez toujours le fichier contenant toutes les variables du projet ouvert**. Si vous voulez exploiter quelque chose (une taille, une famille de polices, une couleur), vérifiez d’abord que ce ne soit pas déjà présent dans les variables. Auquel cas, utilisez-les !

Dans le cas où aucune variable ne correspondrait, considérez la possibilité d’ajouter une nouvelle variable à la liste. Si vous devez utiliser une valeur récurrente, alors faites-en une variable.

