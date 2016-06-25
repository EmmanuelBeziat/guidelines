# Guidelines pour Javascript — Bonnes pratiques

### === au lieu de ==

Javascript est un langage qui comporte quelques faiblesses, et il convient d’être strict à sa place.

Par exemple, si on lui donne un entier et qu’on vérifie une chaîne de caractère, il n’y verra aucun problème :

```javascript
var nombre = 5;
var chaîne = '5';

if (nombre == chaine) {
	// …
}
```

Le code de la condition sera exécuté, ce qui n’est à priori pas normal (un `int` et un `string` n’ont pas à être identiques !). Le fait d’utiliser `===` au lieu de `==` permet de véirifier que le type correspond également. Cela évite de nombreux problèmes.

Il existe toute une liste d’erreurs courrantes dans l’exécution d’un script à cause de ça :
```javascript
'' == '0'           // false
0 == ''             // true
0 == '0'            // true

false == 'false'    // false
false == '0'        // true

false == undefined  // false
false == null       // false
null == undefined   // true

' \t\r\n ' == 0     // true
```

Ce qu’il se passe en réalité, c’est que lorsque deux types ne correspondent pas, le Javascript va tenter de convertir les valeurs (ce qui est plus lent à l’exécution). Mais c’est très hasardeux dès qu’on traite des données utilisateur.

En revanche, il peut parfois s’avérer utile d’exploiter ce point :

Pas bien :
```javascript
if (value === null || value === undefined) {
	// …
}
```

Bien :
```javascript
if (value == null) {
	// …
}
```

Car dans cette configuration, `null` et `undefined` sont équivalents pour Javascript. **Mais il s’agit d’un cas particulier**.
