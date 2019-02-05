# En quoi la qualité des dépendances influe sur la qualité globale du projet ROCKFlows ?

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

## II. Questionnement

### II.1 Observations et problématique générale

Plusieurs membre de notre équipe ont réalisé leur projet de fin d'étude en relation avec ROCKFlows. Avant de commencer le développement, nous avons été confrontés à un projet imposant et dans lequel il est difficile d'entrer. Cela nous a donc pris beaucoup de temps avant de nous familiariser avec l'ensemble du projet. Ceci est un problème commun à beaucoup de projets, dès lors qu'ils sont conséquents. Cette dette technique était notamment empirée par des dépendances autant internes qu'externes. C'est donc sur cet aspect que nous avons voulu diriger notre étude. L'objectif est d'analyser l'impact des dépendances sur la qualité de ROCKFlows et nous en sommes donc arrivés  à la question suivante : 

_**Les dépendances impactent-elles la qualité du projet ROCKFlows ?**_

  
__La qualité pouvant être exposé par plus métriques comme le "code-smell", le nombre de bug, les vulnérabilités du code. Néanmoins, nous nous sommes pas attardé sur le pourcentage de couverture des tests puisque ce dernier était trop faible \(Un seul dépôt contenait des tests\).

###  II.2. Sous-parties

L'état de fait dans lequel nous trouvions nous a mené à deux sous-parties qu'il nous semblait intéressantes à développer :

1. **Mise en place d'un guide permettant à un débutant de visualiser un projet imposant dans son ensemble**.
2. **Analyse des fuites de qualité logicielle provenant des dépendances au sein d'un projet**.

### II.3. Intérêt de ces questionnements

L'intérêt principal de notre point de vue est de fournir une aide tant aux développeurs qu'aux nouveaux arrivants. De plus, nous avons eu des retours de développeurs de ROCKFlows rapportant que ce problème est récurrent. Les développeurs déjà présents sur le projet ont seulement connaissance de leur partie du projet et ont rarement une vision globale. De ceci découle notre premier problème : les développeurs arrivant sur le projet ne trouvent pas de documentation générale sur le projet étant donné qu'aucun développeur expérimenté sur le projet a la connaissance sur la totalité du projet.

Fournir cet outil permettra donc d'élargir la vision des développeurs de ROCKFlows, ainsi que fournir un point d'entrée dans le projet pour les nouveaux arrivants.

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
