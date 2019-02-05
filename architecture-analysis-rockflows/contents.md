# En quoi la qualité des dépendances influe sur la qualité globale du projet ROCKFlows ?

**Date de rendu finale : March 2018 au plus tard**

Remarques :

Les titres peuvent changer pour etre en adéquation avec votre étude.

De même il est possible de modifier la structure, celle qui est proposée ici est là pour vous aider.

Utilisez des références pour justifier votre argumentaire, vos choix etc.

## Auteurs

Nous sommes quatre étudiants en dernière année à Polytech Nice Sophia Antipolis, dans la spécialité Architecture Logicielle :

* CANAVA Thomas &lt;thomas.canava@etu.unice.fr&gt;
* GARDAIRE Loïc &lt;loic.gardaire@etu.unice.fr&gt;
* PICARD-MARCHETTO Ivan &lt;ivan.picard-marchetto@etu.unice.fr&gt;
* SPINELLI Aurélien &lt;aurelien.spinelli@etu.unice.fr&gt;



## Introduction

Ce chapitre présente le travail d'étude produit par notre groupe sur le projet de _machine learning_ ROCKFlows, dans le cadre de la matière Rétro-Ingénierie, Maintenance et Évolution des Logiciels \(RIMEL\). 

Pour commencer, nous allons présenter notre contexte de recherche. Nous continuerons par une présentation de notre question, accompagnée de nos hypothèses. Ensuite, nous expliquerons notre démarche et nous terminerons par une analyse des résultats obtenus.

## I. Contexte de recherche : ROCKFlows

**ROCKFlows** \(pour _Request your Own and Convenient Knowledge Flows_\) est un projet de _machine learning_ développé par le laboratoire I3S de Sophia Antipolis. Son objectif principal est de fournir une interface simple d’utilisation à des utilisateurs non-experts en machine learning dans le but de trouver le meilleur workflow leur permettant de classifier au mieux leur ensemble de données. En effet, ROCKFlows ne peut que classifier des données, il n’a pas la possibilité de faire de la régression.

Pour l’utilisateur non-expert, ce produit se base sur le principe de boîte noire : toutes les spécifications liées au domaine du _machine learning_ lui sont cachées, lui permettant de simplement fournir un jeu de données en entrée et de récupérer des résultats compréhensibles en sortie.

Ayant, pour la majorité du groupe, travaillé sur ROCKFlows lors de projets précédents, il nous semblait intéressant d'analyser ce projet plus en détails. Nous avons fait face à cet imposant projet \(39 dépôts différents\) et il a été difficile de visualiser le projet dans son ensemble. Nous avions donc à cœur d'aider les nouveaux arrivants ainsi que les contributeurs déjà présents sur le projet à avoir une vision plus globale de ROCKFlows. 

## II. Observations/General question

1. Commencez par formuler une question sur quelque chose que vous observez ou constatez ou encore une idée émergente. Attention pour répondre à cette question vous devrez être capable de quantifier vos réponses. --&gt;  Plusieurs membre de notre équipe ont réalisé leur projet de fin d'étude en relation avec ROCKFlows. Avant de commencer le développement, nous avons été confrontées dans un premier temps à une dette technique très importante et cela nous a donc pris beaucoup de temps avant de se familiariser avec l'ensemble du projet. Ceci est un problème commun à beaucoup de projets, dès lors qu'ils sont conséquent. Cette dette technique était notamment augmenter à cause des dépendances autant internes qu'externes. C'est donc sur cet aspect que nous avons voulu dirigé notre étude sur l'impact des dépendances sur la qualité de ROCKFlows et nous en sommes donc venu à la question suivante : _Les dépendances impactent-elles la qualité du projet ROCKFlows ?_ La qualité pouvant être exposé par plus métriques comme le "code-smell", le nombre de bug, les vulnérabilités du code. Néanmoins, nous nous sommes pas attardé sur le pourcentage de couverture des tests puisque ce dernier était trop faible \(Un seul dépôt contenait des tests\).

  


1. Préciser bien pourquoi cette question est intéressante de votre point de vue et éventuellement en quoi la question est plus générale que le contexte de votre projet \(ex: Choisir une libraire de code est un problème récurrent qui se pose très différemment cependant en fonction des objectifs\)

Cette première étape nécessite beaucoup de réflexion pour se définir la bonne question afin de poser les bonnes bases pour la suit.

## III. information gathering

Préciser vos zones de recherches en fonction de votre projet,

1. les articles ou documents utiles à votre projet
2. les outils

## IV. Hypothesis & Experiences

1. Il s'agit ici d'énoncer sous forme d' hypothèses ce que vous allez chercher à démontrer. Vous devez définir vos hypothèses de façon à pouvoir les _mesurer facilement._ Bien sûr, votre hypothèse devrait être construite de manière à v_ous aider à répondre à votre question initiale_.Explicitez ces différents points.
2. Test de l’hypothèse par l’expérimentation. 1. Vos tests d’expérimentations permettent de vérifier si vos hypothèses sont vraies ou fausses. 2. Il est possible que vous deviez répéter vos expérimentations pour vous assurer que les premiers résultats ne sont pas seulement un accident.
3. Explicitez bien les outils utilisés et comment.
4. Justifiez vos choix

## V. Result Analysis and Conclusion

1. Analyse des résultats & construction d’une conclusion : Une fois votre expérience terminée, vous récupérez vos mesures et vous les analysez pour voir si votre hypothèse tient la route. 

![](../.gitbook/assets/logo_uns%20%284%29.png) UCA : University Côte d'Azur \(french Riviera University\)

## VI. Tools \(facultatif\)

Précisez votre utilisation des outils ou les développements \(e.g. scripts\) réalisés pour atteindre vos objectifs. Ce chapitre doit viser à \(1\) pouvoir reproduire vos expériementations, \(2\) partager/expliquer à d'autres l'usage des outils.

## VI. References

1.

1. 
