# Guidelines pour Javascript — Bonnes pratiques

### === au lieu de ==

Javascript est un langage qui comporte quelques lacunes, et il convient d‘être strict à sa place.

Par exemple, si on lui donne un entier et qu‘on vérifie une chaîne de caractère, il n‘y verra aucun problème :

```javascript
var nombre = 5;
var chaîne = '5';

if (nombre == chaine) {
	// …
}
```

Le code de la condition sera exécuté, ce qui n‘est à priori pas normal (un `int` et un `string` n‘ont pas à être identiques !). Le fait d‘utiliser `===` au lieu de `==` permet de véirifier que le type correspond également. Cela évite de nombreux problèmes.

Il existe toute une liste d‘erreurs courrantes dans l‘exécution d‘un script à cause de ça :
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

En revanche, il peut parfois s‘avérer utile d‘exploiter cette faiblesse :

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

Car dans cette configuration, `null` et `undefined` sont équivalents pour Javascript. **Mais il s‘agit d‘un cas particulier**.
