# Guidelines pour Photoshop / Illustrator — Généralités

## Le bord du PSD n’est pas le bord de l’écran

Une première erreur très (trop) fréquente : tenir l’espace de travail comme "complet". Une image valant mieux que beaucoup de mots, voilà une illustration du problème :

![](https://www.emmanuelbeziat.com/wp-content/uploads/2015/01/photoshop-problem-1.jpg)
*
Le design est ici bien rendu, somme toute classique, et l’image sort de façon élégante du cadre du site pour aller rejoindre les bords. Oui, mais **les bords en question ne représentent pas l’écran d’un visiteur** potentiel du site. Ainsi, si on agrandi l’espace de travail pour se représenter la taille d’écran d’un visiteur du site, on se retrouve avec un problème graphique assez évident :

![](https://www.emmanuelbeziat.com/wp-content/uploads/2015/01/photoshop-problem-02.jpg)

L’image ne va plus jusqu'au bord. Outre le fait que ce soit très moche, le site perd toute sa consistance. Il n’y a aucun moyen de gérer ça proprement côté intégration : étirer l’image serait de toutes façons totalement affreux.

Pensez donc toujours à choisir un espace de travail large et à tester votre rendu sur plusieurs types d’écran, et prévoyez différents cas de figure.

## Limitez les couleurs

Pour des raisons de pratique, il est déconseillé d’utiliser une tripotée de couleurs différentes. Certaines différences sont parfois trop subtiles pour être remarquées par l’intégrateur, qui n’a pas les mêmes réglages d’écran que vous, et se verra donc attribuer un retour client parce que *"la couleur n’est pas la bonne"*. De plus, les préprocesseurs CSS d’aujourd’hui (SCSS, SASS, LESS, Stylus…) permettent aux intégrateurs de définir des variables (entre autres pour les couleurs), et en avoir une cinquantaine pour toutes les couleurs de la maquette n’a aucun intérêt…

*Limitez-vous à 5 couleurs maximum* (c'est une moyenne), avec **au plus deux variations par couleur**. Enfin, n’hésitez pas à créer un calque avec les couleurs en question, d’abord pour les réutiliser facilement vous-même (même si vous pouvez utiliser le nuancier de Photoshop prévu à cet effet), ensuite pour permettre à l’intégrateur de les pipeter facilement.

## Oubliez les ronds

Avec le CSS3 est arrivé un super outil : la propriété `border-radius`. Bien que celle-ci se fasse un peu plus discrète ces derniers temps, avec l’avènement du flat-design et le contrecoup d’une utilisation beaucoup trop massive (et avec souvent beaucoup de mauvais goût), elle permet de s'adonner aux joies des arrondis en CSS.

Cependant, une exception à cette règle concerne les ronds parfaits contenant du texte. En effet, si un bouton rond contenant un picto (Comme l’icone de twitter) ne pose à priori aucun problème à l’intégrateur, la question d’un disque contenant du texte est beaucoup plus délicate.

![](https://www.emmanuelbeziat.com/wp-content/uploads/2015/01/photoshop-problem-4.png)

Pour les raisons précédemment citées, la gestion du texte dans une page web est délicate. Or, la rondeur de cet élément repose sur la taille fixe de celui-ci (sinon, ça devient un ovale), car les dimensions d’un conteneur dépendent de son contenu. Il devient de facto très pénible d’obtenir le rendu souhaité en CSS pur, il faut donc ruser et adapter le texte à son conteneur — ce qui pose là encore certains soucis en CSS.

Du reste, si l’intégrateur doit tenir compte de navigateurs antédiluviens (IE8 ou inférieur (ouille !)), il devra en sus utiliser une image pour le disque, ce qui l’obligera à encore plus d’ajustements de texte.

Alors, utilisez les ronds avec parcimonie !

## Attention aux rotations

Là encore, si la troisième release de CSS nous a apporté de sympathiques propriétés permettant — entre autres — d’appliquer une rotation à un élément, ces propriétés ne sont pas envisageables avant IE9, il convient donc de **bien se renseigner sur la portée du projet** avant toute chose.

## Prévoyez plusieurs cas de figure

Si vous faites un menu déroulant, faites le design de ce menu une fois déroulé. Prévoyez les différents états des onglets (standard, survolé, page en cours), des boutons, des liens, des champs de formulaire (focus), et des différentes interactions — s'il doit y en avoir — de la page.

De même, vérifiez avec votre chef de projet si le design doit être fluide, adaptatif, fixe, responsive… Et prévoyez les différentes modifications de la maquette en fonction des besoins — le plus courant étant de prévoir au moins une version mobile.

Pensez à tous les cas de figure !

## Faites des maquettes "au plus petit"

Un problème très recurrent lorsque l’on reçoit des maquettes pour plusieurs formats (mobile, tablette, desktop) : aucune intervalle n’est prévue.

Typiquement, les maquettes pour tablettes sont toujours prévues en 1024px de large, et tous les éléments sont calés de façon à tenir "pile poil". Donc, si j’enlève 10px à cette taille, plus rien ne rentre. Alors oui, la majorité des tablettes font au moins 1024px de large. Oui, mais si je mets ma tablette en portrait ? Hé bien tout va se supperposer, se décaler.

Idem lorsque la maquette desktop est en 1280px (voire parfois en 1600 ou 1920) : qu’est-ce qu’il se passe à 1101px si mon navigateur n’est pas en plein écran ?

> Il est beaucoup plus facile d’étendre des éléments d’une page que de les contracter : on évite tous les problèmes de chevauchement

En clair, lorsque vous faites une maquette pour un *breakpoint* particulier, faites-le au plus "étroit" possible. La maquette "mobile" devrait donc faire 320px pour tenir compte des petits smartphones, la maquette pour tablettes 768px (par exemple), et la version desktop 1024px.

Ainsi, on peut prendre la maquette mobile à 320px et étendre ses éléments jusqu'à 767px, puis passer à la version tablette et étendre ses éléments jusqu’à 1023px, et enfin passer à la version desktop.

## Ne pas faire de maquette "retina"

Une fausse bonne idée qui revient trop souvent : faire des maquettes pour mobile à 640px (le double de 320px) en se disant que ça permet de prendre en compte le retina (densité de pixels x2 sur les iPhones, et équivalents chez Androïd).

Le problème en faisant ça, c'est que la taille native de l'iPhone reste toujours 320px, et que toutes les tailles sont calculées à partir de là. Donc dans votre maquette, vous aurez des titres en 64px parce que vous imaginez que ça deviendra du 32px dans votre iPhone car tout sera divisé par deux ; sauf que non. La typo fera quand même 64px sur votre mobile. Le téléphone va faire lui-même les opérations nécessaires pour doubler sa densité de pixels, elle n'est pas à prévoir en amont, à l’exception des images.

Du reste, le fonctionnement du rétina est beaucoup plus complexe que juste "tout multiplier par deux". Lire cet excellent article de Matthieu Lechat : [pixel CSS et pixel physique](https://www.matthecat.com/pixel-css-et-pixel-physique/)

## Utilisez des grilles

Un point essentiel du design de ces dernières années : l’arrivée des grilles. Elles permettent de structurer facilement ses pages, autant pour le designer que le codeur. Cela permet une cohérence visuelle impeccable et évite d’avoir à gérer plusieurs tailles différentes.

Vous pouvez par exemple utiliser les scripts de [960.gs](http://960.gs/) (ou les modèles fournis), ou bien [des templates prédéfinis](http://www.ravelrumba.com/photoshop-grids/). Plus d’explications dans cet article de Smashing Magazine : [Establishing your grid in photoshop (en)](http://www.smashingmagazine.com/2011/11/09/establishing-your-grid-in-photoshop/).

Demandez à votre intégrateur-trice ce qu'il-elle utilise généralement, vous trouverez sûrement un outil commun.

## Les modes de fusion

Photoshop propose différents modes de fonctionnement des calques entre eux :

![](https://www.emmanuelbeziat.com/wp-content/uploads/2015/09/modes-de-fusion.jpg)

Vous voyez de quoi je parle ? C'est un outil très cool, pour faire plein d’effets sympatoches. Hé bien **vous n’y touchez pas** ! Il est strictement impossible de reproduire ces effets en web. Alors n’en faites rien, sauf si vous pouvez aplatir le résultat final (et dans le doute, demandez, encore une fois).

# Conclusion : discutez avec tout le monde

La meilleure façon de ne pas compliquer le travail des autres reste encore d’en discuter avec eux au long du processus de création. Si l’intégrateur-trice chargé-e de mettre votre maquette en boîte n’est pas un gros manche et connaît un peu son métier, il-elle saura vous aiguiller sur certains points, vous conseiller sur ce qui fonctionne et ce qui est raisonnable, faisable ou inenvisageable en fonction des contraintes qui sont imposées sur le projet. De même, ces gens sont souvent de bon conseil en ce qui concerne la facilité de navigation ou la pertinence de certains éléments.

La plupart des webdesigners avec qui j’ai travaillé n’ont en fait aucune formation en webdesign. Ce sont généralement des maquettistes print et/ou infographistes PAO reconvertis ou qui ont ajouté une compétence à leur panel d’activités. Si vous êtes dans ce cas, n’hésitez pas à chercher quelques journées de formation en webdesign, et lisez des bouquins qui pourront vous aider à vous imprégner plus efficacement du travail de webdesigner.

> La maquette est une étape importante et ne doit pas être expédiée ni négligée. Les maquettes présentées au client devraient toujours d’abord être validées par des développeurs et des ergonomes.
