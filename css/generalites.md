# Guidelines pour CSS — Généralités

* Un site ne devrait avoir qu'un seul fichier CSS à charger, unique et minifié.
* Les versions pour médias alternatifs (mobile, print), devraient être déclarés en fin de document via la déclaration `@media` (exception faite des media-queries via un préprocesseur)
* Toujours utiliser le même mode d’indentation pour tout le document. Installer le plugin [EditorConfig](http://editorconfig.org/) pour votre éditeur/IDE préféré, et toujours exploiter le fichier `.editorconfig` du projet. Naturellement, tout projet doit avoir un tel fichier
* Toujours utiliser le même type de guillemets, de préférence les doubles : `"`
* Garder les déclarations CSS les plus légères possibles : limitation à 2 classes maximum dans la mesure du possible (cf. [Bonnes pratiques](bonnes-pratiques.md)). Et ne (presque) jamais utiliser `!important`
* À part pour de très rares cas qui se comptent sur les doigts d’une seule main (les tableaux, de temps en temps input, et parfois les images), ne jamais utiliser `width: 100%;`.
