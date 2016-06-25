# Guidelines pour Photoshop — Les polices

## Le texte n’est pas contrôlable

Un autre point essentiel : photoshop permet une gestion avancée des textes. On peut, à loisir, modifier le rendu d’une police, gérer son lissage, son inclinaison, lui donner divers effets, le positionner de façon fine et précise, etc.. **Ce n’est pas le cas sur le web** ! L’affichage d’une police dépend du navigateur, du système d’exploitation, du type d’écran… De même, les contrôles sur le texte sont relativement pauvres en CSS, et il est pour l’instant encore presqu'impossible de faire — par exemple — des colonnes fluides de texte, des couleurs dégradées dans des lettres, ou bien simplement d’aligner au centre la dernière ligne d’un texte justifié.

De même, je vois souvent des blocs de texte prévus dans les maquettes pour avoir un certain nombre de lignes, comme dans cet exemple :

![](https://www.emmanuelbeziat.com/wp-content/uploads/2015/01/photoshop-problem-3.png)

Le soucis, c'est qu'il est impossible d’être sûr à 100% que le texte sera affiché tel quel sur le site. Il se peut très bien qu'il dépasse, et donc que tout le principe de ce bout de design se retrouve par terre.

De la même façon, laissez "couler" le texte. N’essayez pas de forcer des retours à la ligne (hors quelques titres), ce sera calamiteux pour l’intégrateur, et ingérable en cas de redimensionnement du conteneur.

## Limitez les polices…

Attention à ne pas faire dans l’excentricité. Certes, aujourd’hui la propriété `@font-fac` permet de faire bien des choses pratiques, mais il y a mille et unes raisons (ou presque) pour qu’une typo ne se charge pas. Réservez donc les polices "excentriques" à des textes particuliers, tels que les titres, le menu de navigation ou des encarts occasionnels. Pour ce qui est du contenu textuel, restez-en aux polices dites "web safe" dont voici une liste (pas forcément exhaustive).

Vous pouvez bien sûr adapter en fonction de votre cible : pour un site à destination des utilisateurs de Windows Phone (par exemple), ou pour une majorité d’utilisateurs Windows, vous pouvez opter pour **Segoe UI**, qui sera très raccord avec le reste de l’environnement de travail. À l’inverse, pour le site de votre application OSX ou iOS, l’emploi de **Helvetica Neue** sera tout à fait approprié et safe puisque présente sur tous les systèmes Apple (du moins, ceux relativement récents).

Dans tous les cas, pensez à fournir les fichiers des typos que vous utilisez à l’intégrateur.

## … et ne les modifiez pas !

Il va sans dire que toute modification corporelle d’une typo est prohibée. J’entends par là modifier l’échelle horizontale ou verticale de celle-ci, ou bien utiliser les options *Faux-gras* ou *Faux-italique*, par exemple.

## Gardez des tailles de police cohérentes

Le rendu du texte par défaut (le contenu textuel) doit être le même partout, pour chaque page. Par défaut, la taille de texte d’un document web est définie à 16px, pour fournir un compromis entre confort de lecture et quantité de texte affichée. Vous pouvez bien sûr en changer, mais assurez-vous que cette taille soit la même pour toutes les pages. De même ne faites pas de variations entre les éléments occasionnels : la taille d’un titre devrait elle aussi rester la même d’une page à une autre, même si la mise en forme est différente (ça arrive, par exemple une page "article" et une page "liste des articles" ne sont pas forcément identiques).

Enfin, **assurez-vous d’utiliser des tailles de police réelles**. Photoshop laisse la liberté de mettre des tailles totalement délirantes (23.58px) qu'il n’est pas possible d’avoir en web.

De même, gardez une cohérence au niveau des valeur : restez plutôt sur des nombres pairs et privilégiez des écarts logiques et linéaires (Par exemple de 8 pixels : 16px, 24px, 32px).

## Attention à la casse

Il se peut que l’intégrateur-trice doive copier-coller les textes que vous aurez mis en maquette. Le contenu de certains projets est parfois validés directement en maquette, parfois dans des langues étrangères. J’ai eu le cas récemment avec du mongol, auquel je ne comprend pas un broque : il m'était impossible de réécrire le contenu moi-même. Pour ces raisons, faites attention à votre façon d’écrire du texte : **Ne mettez jamais tout en majuscules**. Si vous devez mettre un texte en capitales, utilisez le bouton "Tout en capitales" du panneau d’options Caractère. De la même façon, il m'arrive de copier coller des textes et de me retrouver avec `un ACCOMPAGNEMENT personnalisÉ`. Faites donc attention à ce genre de détails, et écrivez de façon normale même si le rendu diffère.

## Utilisez des font-icons

Plutôt que de piocher des images sur [iconfinder](http://www.iconfinder.com) (au demeurant très bon), **pourquoi ne pas utiliser une font-icon
** ? En fonction des besoins, [FontAwesome](http://fontawesome.io/) ou [Genericons](https://genericons.com/) sont de très bons choix. Pour être encore plus spécifique, vous pouvez faire les votre sur des sites comme [Fontello](http://fontello.com/) (auquel cas, pensez à fournir les typos et le CSS générés !).

D’abord, ça évitera à l’intégrateur-trice de devoir enregistrer chaque icône manuellement, devoir faire des sprites, et parfois utiliser des ruses de sioux pour des états différents (survol). Ensuite, ça évitera beaucoup de complications pour la gestion des différents supports, et des écrans (Par exemple, les fameux écrans Retina et leurs pendants chez la concurrence).

Bref, à moins d’avoir des besoins très spécifiques en matière d’icones (plusieurs couleurs, par exemple), il n’y a aucune raison de ne point utiliser ces petits bijoux.