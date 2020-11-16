# TD AnimEstiam

Vous êtes en train de créer une application web nommée "AnimEstiam" vous permettant d'enregistrer vos animes préférés.

Vous n'avez pas de serveur pour rendre l'enregistrement de vos données persistantes, mais vous avez travaillé sur une interface pour vous permettre déjà de les afficher.
Après avoir fait la partie HTML et CSS, vous avez besoin maintenant de dynamiser la page avec javascript.

# Où trouver les données des animes

Par chance, on a trouvé une API nommée `Jikan` nous permettant de récupérer les informations d'anime du site `MyAnimeList`.

https://jikan.docs.apiary.io

Nous allons utilser Axios pour faciliter nos requêtes AJAX vers cette API

https://github.com/axios/axios



# Fonctionnalités de AnimEstiam à rendre dynamique

## Barre de recherche

Une barre de recherche est à notre disposition en haut à droite de la page :
* En tapant dans cette barre, à partir de 3 lettres tapées, cela lancera une recherche d'anime par son nom
* Une liste apparaît avec les résultats de recherches. En cliquant sur un des résultats, cela ajoutera une carte dans la liste des animes

### Remarques

* Nous devons utiliser la référence `Search` dans l'API
    * https://jikan.docs.apiary.io/#reference/0/search
* Il existe un évènement pour savoir quand la valeur d'un champ texte a changée
  * https://developer.mozilla.org/fr/docs/Web/API/HTMLElement/change_event
* Pour permettre un meilleur découpage et éviter d'utiliser le système qui ajoute une carte en dépendance direct dans le code, on pourrait créer un évènement `onAnimeChoosed` sur lequel un autre élement pourrait écouter pour savoir si un anime a été choisi
  * https://developer.mozilla.org/fr/docs/Web/Guide/DOM/Events/Creating_and_triggering_events

## Liste de cartes

Nous avons une liste de cartes.
 Chaque carte représente un anime qui a été choisi depuis la barre de recherche.

On y trouve :
* Une image
* Son titre
* Le score noté sur 10
* Le nombre d'épisode

Un bouton d'information est présent et ouvre une fenêtre modale.

## Détail d'un anime

Dans la fenêtre ouverte lorsque l'on a cliqué sur le bouton `Info` d'une carte, nous pouvons trouver les informations suivantes :

* Dans l'entête de la fenêtre :
  * Le titre
  * Le lien pour regarder une bande-annonce
* Dans le tableau
  * Sa source
  * La durée des épisodes
  * Le genre
  * Le synopsis

### Remarques

* Nous devons récupérer les informations détaillées avec la référence `Anime` dans l'API
  * https://jikan.docs.apiary.io/#reference/0/anime

# Remarques complémentaires

Utilisez `querySelector` pour récupérer les éléments dont vous avez besoin
* https://developer.mozilla.org/fr/docs/Web/API/Document/querySelector

Ne copiez pas de code html dans un code JS. Dans le cas d'une carte par exemple, utilisez l'élément HTML `template` pour stocker un contenu HTML qui sera utilisé en javascript en tant qu'instance
* https://developer.mozilla.org/fr/docs/Web/HTML/Element/template

Vous trouverez dans `scripts/api` plusieurs fichiers :
* Ces fichiers sont incomplets, à vous de les compléter
* Vous avez :
  * Une classe d'api qui utilise Axios pour faire les appels AJAX vers l'API Jikan
  * Une classe Resource qui est la classe de base pour chaque Resource référencée sur Jikan
  * Une classe AnimeResource qui hérite de Resource pour gérer spécifiquement la référence `Anime` sur Jikan
  * Une classe SearchResource qui hérite de Resource pour gérer spécifiquement la référence `Search` sur Jikan

Les classes vous permettent d'avoir une approche de ce que vous connaissez en orienté objet dans d'autres languages. Cela vous permettra de mieux découper chaque partie de code et d'y appliquer une logique algorithmique.

Je ne vous oblige pas à utiliser les classes, vous pouvez faire sans si vous vous sentez absolument pas à l'aise. Mais ça risque de vous faire défaut dans le futur si vous n'essayez pas au moins de découper au maximum votre code de manière claire.

Vous pouvez très facilement créer des classes pour gérer votre DOM.

Par exemple :
* Vous pouvez créer une classe `Anime` qui contient les informations d'un anime
* Vous pouvez créer une classe `CardAnime`
  * Qui contient dans une propriété une instance de `Anime`
  * Qui gère la création de l'élément HTML à partir du template d'une carte
* Vous pouvez créer une classe `CardAnimeList`
  * Qui contient une liste de `CardAnime`
  * Qui s'occupe d'ajouter l'élément HTML `CardAnime` dans l'élément HTML qui est le conteneur des cartes

---

Vous êtes en groupe de deux :
* Communiquez régulièrement et soutenez-vous si besoin
* Travaillez chacun sur votre branche
* Séparez bien vos tâches entre vous au maximum pour évitez de vous marcher sur les pieds
* Définissez vous bien vos points de jonction de code pour que lorsque vous fusionnez vos branches, il y ai le moins de conflits possibles et seulement quelques ajustements à faire.

Par exemple :
* Une personne peut travailler sur le mécanisme d'ajoute d'une carte en simulant les informations reçues en paramètres avec des données statiques
* L'autre personne peut quand à elle travailler sur la recherche
* Quand les tâches sont finies de manière isolée => fusion sur la branche `master` et faites les ajustements sur votre point de jonction, ici la jonction est : quand je cliques sur un résultat de la recherche, cela va créer une carte de l'anime dans la liste

---

ET SURTOUT :
* Prenez l'habitude de savoir vous documenter et faire des recherches pour trouver la solution à vos problématiques
* Osez demander de l'aide quand cela ne va vraiment pas, les intervenants sont là pour vous aider
* Ne trainez pas sur un point particulier pendant trop longtemps, il y a pleins de choses sur lequel on peut avancer