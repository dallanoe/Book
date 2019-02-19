# Projet 1 : How to improve contributors onboarding

## Auteurs

Nous sommes quatre étudiants en dernière année de Sciences Informatiques à Polytech Nice-Sophia en spécialité Architectures Logicielles :

* BOUNOUAS Nassim &lt;nassim.bounouas@etu.unice.fr&gt;
* CANCELA VAZ Joël &lt;joel.cancela-vaz@etu.unice.fr&gt;
* MORTARA Johann &lt;johann.mortara@etu.unice.fr&gt;
* ROUSSEAU Nikita &lt;nikita.rousseau@etu.unice.fr&gt;

## I. Les contributeurs, la vraie ressource de l'open-source

Le sujet ayant retenu notre attention concernait le projet XWiki. Le sujet initial, était subdivisé en deux questions :

* Comment améliorer la qualité de code chez XWiki ?
* Comment améliorer l'onboarding des contributeurs chez XWiki ?

En partant de ces sujets nous avons redéfini une nouvelle problématique : Comment introduire une dynamique de contribution dans un projet open source et pérenniser sa communauté ?

L'intérêt principal de cette recherche réside dans l'importance de la communauté dans le monde open source. De nombreux projets open-source constituent le socle de l'informatique moderne que ce soit des éditeurs, aux outils de build jusqu'aux librairies "habituelles" : Visual Code Studio, Maven, Gradle, Junit, Mockito, Apache Kafka, Jenkins, Docker...

L'ensemble de ces projets constituent le paysage technologique de notre époque et sont devenus incontournables pour la plupart des développeurs. Derrière ces projets et organisations se cachent souvent des centaines de contributeurs, rémunérés ou non par des sociétés pour participer à l'avancée desdits projets. Le noyau Linux peut être considéré comme le projet open source ayant le plus impacté le monde de l'informatique ces 30 dernières années. Compte tenu de son usage, le noyau Linux regroupe de nombreux contributeurs professionnels \(ie. rémunérés par une entreprise pour contribuer\).

Qu'en est-il des projets plus petits ? Comment peuvent-ils faire grandir leur communauté ? Comment peuvent-ils inciter les contributeurs à participer activement et sur le long terme au développement du projet ?

## III. Collecte d'informations

Nous avons ciblé 4 projets de taille comparable à XWiki afin d'en étudier les contributions :

* Junit 5
* Mockito
* Hibernate ORM
* Log4j2

Afin de cadrer notre recherche nous avons du définir la notion de contributeur. Nous avons donc restreint la définition de contributeur à toute personne ayant proposé un commit accepté sur la branche principale du projet.

Un entretien avec Vincent Massol nous a permis d'ajouter une nuance dans notre analyse puisque l'ensemble des projets retenus reposent tous sur une communauté alors qu'XWiki est soutenu avec la société XWiki SAS. Ce point est néanmoins nuancé par l'implication d'industriels dans l'ensemble de ces projets \(condition préalable à notre sélection\).

Nous avons de plus cherché des articles de recherche traitant de l'open source et des dynamiques de contributions. Parmi les papiers ayant attiré notre attention, ceux ayant eu un réel intêrét :

* Papier 1
* Papier 2
* Papier 3

Nous souhaitions initialement réaliser un sondage en ligne afin de pouvoir confronter nos résultats à l'avis d'un groupe plus ou moins grands de développeurs. Nous avons décider de réaliser ce sondage en fin d'analyse afin d'une part de ne pas être guidé dans nos recherches par les résultats de ce dernier et d'autre part pour nous permettre d'affiner les questions. En effet, l'étude des métriques tangibles nous a conduit à des métriques subjectives ne pouvant pas être mesurées autrement qu'en interrogeant les contributeurs.

## IV. Une chambre bien rangée est-elle plus accueillante ?



## V. Analyse des résultats et Conclusion

### JUnit5

JUnit est un framework de test unitaire, un des plus utilisés pour le langage Java. Cette version majeure 5 succède à la version 4 et apporte beaucoup de nouvelles fonctionnalités majeures. Cette version 5 est aussi une refonte du framework et par conséquent se trouve sur un “repository” à part.

En débutant cette étude chaque membre de l'équipe a posé sur le papier ses impressions et ses préjugés. Nous nous sommes alors rendu compte que nous arrivions à la même hypothèse : Pour nous les principaux facteurs permettant d'attirer des contributeurs dans un projet open-source résidaient dans la bonne tenue de celui, une bonne documentation et des régles de contributions mises en avant et détaillées.

En partant de cette hypothèse nous avons défini des métriques pouvant, d'après nous, la valider ou l'invalider.  Les métriques retenues étaient donc :

* KPI 1
* KPI 2
* KPI 3

#### Analyses des KPI \(analyse faite le 27 Janvier 2019\)

* Présence d'un README.md :
  * Présent et est assez complet, contient les parties \(_Contributing, Getting Help, Continuous Integration Builds, Code Coverage_ et _Building from Source_\).
* Méthode de contribution :
  * Chercher les issues taguées avec "_up-for-grabs_" \(qui sont très peu nombreuses, 10 seulement au moment la vérification\)
* Badges \(ou _shields_\) :
  * Travis.CI et Appveyor, tous les deux au vert au moment de la vérification avec le label "_Build passing_"
* Présence d'une intégration continue sur Travis.CI et Appveyor.
* Présence d'un CONTRIBUTING.md
  * Présent et détaille très bien les conventions de nommage et formatage du code.
* Exemples de code :
  * Présent sur un autre repository, lien référencé dans le README.md
* Présence de Javadoc, à jour et mise à jour automatiquement à chaque commit
* Temps moyen de réponse aux issues: environ 1h
* Nombre de commits sur master : 5417 au moment de la vérification
* Nombre de contributeurs : 95

#### Analyses des contributions

Le projet a démarré en octobre 2015, comporte plus de 5400 commits et 95 contributeurs.

Parmis ces contributeurs :

* 44 contributeurs avec 1 commit \(46,3%\)
* 43 contributeurs avec 2 à 16 commits \(45,3%\)
  * dont seulement 6 contributeurs avec au moins 2 commits espacés d’une semaine.
  * et un membre de Neo4j \(un autre projet Java de gestion de base de données basé sur les graphes\).
* 8 principaux contributeurs: \(8.4%\)
  * Top 8: un compte nommé “junit-buildmaster” qui sert pour des opérations de gestion du code \(indentation de code, renommage de variables, mise à jour de headers dans la documentation\).
  * Top 7: un contributeur lambda qui ne contribute plus depuis 2 ans \(dernier commit octobre 2017\)
  * Top 6 : un autre contributeur lambda qui ne contribue plus depuis janvier 2017
  * Top 5 : un contributeur lambda encore très actif \(dernier commit 24 janvier 2019 au moment de la vérification\)
  * Top 4 : un membre de JUnit, son premier commit a été plus tardif que les autres membres, aussi très actif \(dernier commit 14 janvier 2019\)
  * Top 3: un contributeur lambda, grosse contribution entre fin 2015 et 2016, depuis plus rien.
  * Top 1 et 2: deux membres de JUnit qui ont contribué au projet depuis le début et qui continuent.

Une recherche sur le [site portfolio](https://blog.johanneslink.net/2016/04/16/goodbye-junit-5/) d'un des 8 contributeurs a montré que les contributeurs 2, 3, 5 et 7 se connaissent et ont travaillé en équipe ensemble, et que suite à des conflits dans l’équipe ils sont cessés de travailler ensemble. Les contributeurs 3, 5 et 7 ne sont donc pas si “étrangers” au projet. Il semble donc qu’il n’y ait qu’un seul “vrai” contributeur externe au projet dans les 8 principaux contributeurs, le contributeur 6, qui ne contribue plus.  
Le projet est porté par les membres de l'équipe JUnit.

Il est possible de discuter avec la team de développement sur Gitter ou indirectement via StackOverflow.

Une KPI qui n'a pas vraiment été prise en compte est la complexité du projet, en effet, le projet JUnit5 est composé d'une vingtaine de modules Java et le coup d'entrée dans le projet semble être assez conséquent, même les issues "_up-for-grabs_" sont parfois incompréhensibles pour un néophyte.

De plus, en regardant certains commentaires de certains membres de JUnit à l'égard de nouveaux contributeurs qui demandent s'il peuvent essayer d'implémenter une fonctionnalité ne sont pas très encourageants. Ce qui a pour effet de créer une sorte de syndrome de la tour d'ivoire.

#### Analyses des contributions

![Pas de r&#xE9;ponse pour les questions de ce pauvre contributeur](../.gitbook/assets/no-answer-to-question-issue.png)

![Pull request ferm&#xE9;e, mainteneur &quot;qui n&apos;a pas le temps&quot; de review le code](../.gitbook/assets/denied-pull-request.png)

![Pas tr&#xE8;s encourageant de dire: &quot;on promet rien&quot;](../.gitbook/assets/essaie-mais-on-promet-rien.png)

Pour confirmer mes propos je me suis rendu sur le **Gitter** de l'équipe JUnit, me suis fait passé pour un nouveau contributeur qui aimerait contribuer mais qui ne sait pas par où commencer. Le résultat est assez décevant... les membres de l'équipe JUnit ne m'ont pas répondu et ont continué leur discussion. C'est un contributeur externe qui m'a aiguillé sur une de ses _issues_ qu'il a fait il y'a quelques années et qui s'est proposé de m'aider si j'en avais le besoin.

![Capture d&apos;&#xE9;cran de la discussion sur Gitter](../.gitbook/assets/snobe.png)

Avec tous ces exemples, on en déduit que les contributions externes ne semble pas être une priorité pour l'équipe.

### Mockito

#### Analyses des KPI \(analyse faite le 10 Février 2019\)

* Présence d'un README.md :
  * Présent et à jour. Le document  contient les grandes lignes permettant l'accueil dans le projet \( Version courante, liens vers les documentations fonctionnelles et techiques et les différents moyens de contacter l'équipe\)
  * Il est clairement écrit que le projet désire des contributions externes et tout est fait pour qu'un nouvel entrant puisse construire le projet et proposer des modifications / envoyer du code.
* Méthode de contribution :
  * Sur les 239 tickets ouverts, 14 portent un label "please contribute" et sont adaptés à un nouveau contributeur
  * Un fichier CONTRIBUTING.md est préset et commence par les différents endroits où un externe au projet peut entrer en contact avec la communauté pour obtenir du support. Ce fichier décrit clairement les deux branches principales du projet \(version courante et version à venir\). Les attentes en terme de pull request \(commits, coding style et procédures\) sont décrites.
* Badges \(ou _shields_\) :
  * Travis.CI \(build : passing\)
  * Codecov : Couverture en test unitaire de 88%
  * Versions : Licence, Release notes, Dernière version téléchargeable \(binaire et maven\), dernière version documentée
* Présence d'une intégration continue sur Travis.CI et Codecov.
* Présence d'un CONTRIBUTING.md
  * Présent et détaillé, voir méthodes de contributions.
* Exemples de code :
  * Présent sur le site officiel du projet
* Présence de Javadoc, à jour et mise à jour automatiquement à chaque commit
* Temps moyen de réponse aux issues: environ ??
* Nombre de commits sur master : ??? au moment de la vérification
* Nombre de contributeurs : ???

#### Analyse des contributions

### Hibernate

#### Analyse des KPI

* Présence d'un `README.md` :
  * Contient les consignes de base permettant de construire le projet.
  * Propose une redirection vers le `CONTRIBUTING.md`.
* Méthode de contribution :
  * Un fichier CONTRIBUTING.md est présent. Il apporte des précisions sur les licences utilisées dans le projet et fournit un guide des étapes à réaliser pour pouvoir contribuer au projet.
  * Les issues sont gérées avec un JIRA externe. Les premières réponses sont de l'ordre de quelques heures.
* Badges :
  * Jenkins : _build passing_
  * LGTM \(qualité du code\) : A
* Intégration continue : Jenkins, LGTM
* Documentation : présence d'une AsciiDoc sur le dépôt du projet.
* Nombre de contributeurs au moment de l'étude : 346
* Nombre de commits sur `master` au moment de l'étude : 9436

#### Analyse des contributions

En analysant la répartitions des commits sur la branche `master` du projet, nous pouvons dégager plusieurs profils de contributeurs :

* 1 → 2 : contributeurs réguliers
* 3 → 10 : contributeurs ayant bien contribué sur une période
* 11 → 50 : contributions occasionnelles
* 51+ : contribution unique

Il est intéressant de remarquer que les 18 premiers contributeurs font partie de l'organisation GitHub _Hibernate_. Hibernate étant développé par JBoss \(qui est une division de RedHat\), nous pouvons supposer que ces contributeurs sont rémunérés pour contribuer au projet.

Le projet Hibernate est composé de 39 dépôts. Nous avons choisi de concentrer notre étude sur le dépôt de _Hibernate ORM_.

Ce projet vérifie également la loi de Pareto : de par la quantité de contributions produite par les développeurs de l'organisation _Hibernate_, moins de 20% des contributeurs ont produit et maintiennent plus de 80% du projet.

#### Conclusion



1. Analyse des résultats & construction d’une conclusion : Une fois votre expérience terminée, vous récupérez vos mesures et vous les analysez pour voir si votre hypothèse tient la route. 

UCA : University Côte d'Azur \(french Riviera University\)

## VI. Tools \(facultatif\)

Précisez votre utilisation des outils ou les développements \(e.g. scripts\) réalisés pour atteindre vos objectifs. Ce chapitre doit viser à \(1\) pouvoir reproduire vos expériementations, \(2\) partager/expliquer à d'autres l'usage des outils.

## VI. References

1.

1. 
