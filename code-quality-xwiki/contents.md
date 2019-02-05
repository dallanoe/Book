---
description: >-
  Problématique finale : Comment introduire une dynamique de contribution dans
  un projet open source et pérenniser sa communauté ?
---

# Projet 1 : How to improve contributors onboarding

## Auteurs

Nous sommes quatre étudiants en dernière année de Sciences Informatiques à Polytech Nice-Sophia en spécialité Architectures Logicielles :

* BOUNOUAS Nassim &lt;nassim.bounouas@etu.unice.fr&gt;
* CANCELA VAZ Joël &lt;joel.cancela-vaz@etu.unice.fr&gt;
* MORTARA Johann &lt;johann.mortara@etu.unice.fr&gt;
* ROUSSEAU Nikita &lt;nikita.rousseau@etu.unice.fr&gt;

## I. Contexte de recherche

Le sujet ayant retenu notre attention concernait le projet XWiki. Le sujet initial, était subdivisé en deux questions :

* Comment améliorer la qualité de code chez XWiki ?
* Comment améliorer l'onboarding des contributeurs chez XWiki ?

En partant de ces sujets nous avons redéfini une nouvelle problématique : Comment introduire une dynamique de contribution dans un projet open source et pérenniser sa communauté ?

L'intérêt principal de cette recherche réside dans l'importance de la communauté dans le monde open source. De nombreux projets open-source constituent le socle de l'informatique moderne que ce soit des éditeurs, aux outils de build jusqu'aux librairies "habituelles" : Visual Code Studio, Maven, Gradle, Junit, Mockito, Apache Kafka, Jenkins, Docker...

L'ensemble de ces projets constituent le paysage technologique de notre époque et sont devenus incontournables pour la plupart des développeurs. Derrière ces projets et organisations se cachent souvent des centaines de contributeurs, rémunérés ou non par des sociétés pour participer à l'avancée desdits projets. Le noyau Linux peut être considéré comme le projet open source ayant le plus impacté le monde de l'informatique ces 30 dernières années. Compte tenu de son usage, le noyau Linux regroupe de nombreux contributeurs professionnels \(ie. rémunérés par une entreprise pour contribuer\).

Qu'en est-il des projets plus petits ? Comment peuvent-ils faire grandir leur communauté ? Comment peuvent-ils inciter les contributeurs à participer activement et sur le long terme au développement du projet ?

## II. Question générale

1. Commencez par formuler une question sur quelque chose que vous observez ou constatez ou encore une idée émergente. Attention pour répondre à cette question vous devrez être capable de quantifier vos réponses.
2. Préciser bien pourquoi cette question est intéressante de votre point de vue et éventuellement en quoi la question est plus générale que le contexte de votre projet \(ex: Choisir une libraire de code est un problème récurrent qui se pose très différemment cependant en fonction des objectifs\)

Cette première étape nécessite beaucoup de réflexion pour se définir la bonne question afin de poser les bonnes bases pour la suit.

## III. Collecte d'informations

1. les articles ou documents utiles à votre projet
2. les outils

Nous avons ciblé 4 projets de taille comparable à XWiki afin d'en étudier les contributions :

* Junit 5
* Mockito
* Hibernate ORM
* Log4j2

Afin de cadrer notre recherche nous avons du définir la notion de contributeur. Nous avons donc restreint la définition de contributeur à toute personne ayant proposé un commit accepté sur la branche principale du projet.

Un entretien avec Vincent Massol nous a permis d'ajouter une nuance dans notre analyse puisque l'ensemble des projets retenus reposent tous sur une communauté alors qu'XWiki est soutenu avec la société XWiki SAS. Ce point est néanmoins nuancé par l'implication d'industriels dans l'ensemble de ces projets \(condition préalable à notre sélection\).



Nous avons de plus cherché des articles de recherche traitant de l'open source et des dynamiques de contributions. Parmi les papiers ayant attiré notre attention, ceux ayant eu un réel intêrét :

## IV. Hypothèses et expériences

1. Il s'agit ici d'énoncer sous forme d' hypothèses ce que vous allez chercher à démontrer. Vous devez définir vos hypothèses de façon à pouvoir les _mesurer facilement._ Bien sûr, votre hypothèse devrait être construite de manière à v_ous aider à répondre à votre question initiale_.Explicitez ces différents points.
2. Test de l’hypothèse par l’expérimentation. 1. Vos tests d’expérimentations permettent de vérifier si vos hypothèses sont vraies ou fausses. 2. Il est possible que vous deviez répéter vos expérimentations pour vous assurer que les premiers résultats ne sont pas seulement un accident.
3. Explicitez bien les outils utilisés et comment.
4. Justifiez vos choix

## V. Analyse des résultats et Conclusion

### JUnit5

JUnit est un framework de test unitaire, un des plus utilisés pour le langage Java. Cette version majeure 5 succède à la version 4 et apporte beaucoup de nouvelles fonctionnalités majeures. Cette version 5 est aussi une refonte et par conséquent se trouve sur un “repository” à part.

#### Analyses des KPI

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

Une recherche sur les sites portfolio de chacun des 8 contributeurs a montré que les contributeurs 2, 3, 5 et 7 se connaissent et ont travaillé en équipe ensemble, et que suite à des conflits dans l’équipe ils sont cessés de travailler ensemble. Les contributeurs 3, 5 et 7 ne sont donc pas si “étrangers” au projet. Il semble donc qu’il n’y ait qu’un seul “vrai” contributeur externe au projet dans les 8 principaux contributeurs, le contributeur 6, qui ne contribue plus.

#### Conclusion



1. Analyse des résultats & construction d’une conclusion : Une fois votre expérience terminée, vous récupérez vos mesures et vous les analysez pour voir si votre hypothèse tient la route. 

![](../.gitbook/assets/logo_uns%20%286%29.png) UCA : University Côte d'Azur \(french Riviera University\)

## VI. Tools \(facultatif\)

Précisez votre utilisation des outils ou les développements \(e.g. scripts\) réalisés pour atteindre vos objectifs. Ce chapitre doit viser à \(1\) pouvoir reproduire vos expériementations, \(2\) partager/expliquer à d'autres l'usage des outils.

## VI. References

1.

1. 
