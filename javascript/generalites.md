# Guidelines pour Javascript — Généralités

* Toujours utiliser les single-quotes `'`
* Installer un linter en temps réel sur son éditeur/IDE. J’utilise actuellement jshint (via sublime-linter). Et respecter ses recommandations.
* Toujours utiliser le même mode d’indentation pour tout le document. Installer le plugin [EditorConfig](http://editorconfig.org/) pour votre éditeur/IDE préféré, et toujours exploiter le fichier `.editorconfig` du projet. Naturellement, tout projet doit avoir un tel fichier.
* `'use strict'` est obligatoire.
* Encapsulation de tout le code, aucune empreinte globale. Si nécessaire, créer un namespace.
* Toutes les variables d’un bloc sont déclarées en début de celui-ci.
