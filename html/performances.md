# Guidelines pour HTML — Performances

## Un seul fichier

Une page html (et un site, de manière générale) devrait ne charger qu‘un seul fichier CSS et qu‘un seul fichier Javascript. De préférence, bien sûr, minifiés.

## Le Javascript se charge à la fin

À l‘exception notable de *html5shiv* pour les projets compatibles avec IE8-, tous les javascript sont déclarés en fin de `<body>`.