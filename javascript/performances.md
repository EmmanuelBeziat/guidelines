# Guidelines pour Javascript — Performances

## Court-circuiter les blocs au lieu de les imbriquer

Recourir à `return`, `break` ou `continue` pou sauter une partie d‘un code, pour épargner des codes imbriqués inutiles.

Pas bien :
```Javascript
function maFonction(items) {
	var result = [];
	if (items.length) {
		for (var i = 0, len items.length; i < len; ++index) {
			// …
		}
	}

	return result;
}
```

Bien :
```Javascript
function maFonction(items) {
	var result = [];

	if (items.length) {
		return result;
	}

	for (var i = 0, len items.length; i < len; ++index) {
		// …
	}

	return result;
}
```

Pas bien :
```Javascript
while (items.length > 0) {
	if (item.hasOwnProperty('taggable')) {
		// Long code de traitement
	}
}
```

Bien :
```Javascript
while (items.length > 0) {
	if (!item.hasOwnProperty('taggable')) {
		continue;
	}

	// Long code de traitement
}
```

## Utiliser la délégation d‘événements

Lorsque plusieurs éléments ont le même événement attaché, il est préférable d‘utiliser la délégation d‘événements. Ça consiste à attacher l‘*event handler* sur le plus proche parent des éléments communs, plutôt qu‘à chacun des éléments eux-mêmes.

Pas bien :
```javascript
$('.navigation a').on('click', function(event) {

});
```

```javascript
$('.navigation').on('click', 'a', function(event) {

});
```

Dans les deux cas avec jQuery, `this` revenrra bien le lien.

## Ne pas concaténer les chaînes

Souvent en Javascript, il faut construire tout un code html en y insérant plusieurs variables. Quand une chaîne devient un peu trop longue, les performances s‘écroulent. Il est préréfable alors d‘utiliser un *push* sur un *array*.

Pas bien :
```javascript
function maFonction(info) {
	var html = '';

	html += '<div>';
	for (var i = 0; i < info.length; ++i) {
		html += '<a href="' + info.link + '">' + info.content + '</a>';
	}
	html += '</div>';

	return html;
}
```

Bien :
```javascript
function maFonction(info) {
	var html = ['<div>'];

	for (var i = 0; i < info.length; ++i) {
		html.push('<a href="' + info.link + '">' + info.content + '</a>');
	}
	html.push('</div>');

	return html.join('');
}
```
