# Projet 2 : Comment identifier les zones "sensibles" d'un projet Open Source ?

## Auteurs 

Nous sommes quatre étudiants en Master 2 d'Architecture logicielle : 

* Rudy Meersman &lt;rudy.meersman@etu.unice.fr&gt;
* Gaétan Duminy &lt;gaetan.duminy@etu.unice.fr&gt;
* Damien Fornali &lt;damien.fornali@etu.unice.fr&gt;
* Amandine Benza &lt;amandine.benza@etu.unice.fr&gt;

## Introduction

Des technologies émergent tous les jours. Les organisations, Open Source comme privées, produisent de plus en plus des systèmes qui utilisent une multitude de technologies, concepts et outils. 

Dans un tel contexte, de nouveaux problèmes apparaissent. Certaines de ces technologies \(par exemple HTML ou CSS\) ne sont pas forcément testables au sens où on l'entend \(tests unitaires, de non-régression...\) mais peuvent tout de même venir entraver l'expérience des utilisateurs du produit. De nombreuses questions sous-jacentes à ce problèmes émergent. Avant de proposer une méthodologie afin de tenter de répondre à ce problème, comment pouvons nous identifier ces technologies, ces zones qui nécessitent plus d'attention afin d'accroître la qualité globale du projet ?

Ce document va présenter les résultats de nos recherches sur l'identification de zones "sensibles" d'un projet Open Source. Nous présentons donc dans une première partie le contexte de notre recherche puis, dans un second temps ,la démarche que nous avons suivie que les différents résultats obtenus.

## I. Contexte de la recherche

### 1.1. Pourquoi des projets Open Source ? <a id="docs-internal-guid-e7045e26-7fff-fbe0-966c-c04c74baeec5"></a>

À l'heure actuelle, les projets Open Source sont de plus en plus nombreux et populaires. De tels projets impliquent généralement des contraintes différentes et souvent plus "légères", que le développement d'un projet en entreprise. Cela n'impacte pas forcément pour autant la taille de ce genre de projets. En effet, il n'est pas rare qu'un projet Open Source grossisse grandement au fil du temps, tant au niveau de son code que de sa communauté.

Avec la croissance du nombre de contributeurs, on voit également apparaitre une diversité de styles de développement. Cette croissance s’accompagnant de son lot de problèmes divers et variés, il est alors nécessaire d'être plus vigilant quant aux zones "sensibles" du code développé.

Dans ce contexte, la quantité et la qualité des tests sont des métriques primordiales. Ces tests sont nécessaires pour corriger ou éviter des erreurs pouvant survenir.

Cependant, dans un projet de grande envergure, il peut s’avérer difficile de tout tester. Des parties déjà considérées comme stables par les développeurs ne sont plus forcément mises à jour, or elles peuvent à terme devenir une source de problèmes.

C'est dans ce contexte que se situe notre étude. Nous allons analyser un projet Open Source de grande envergure, ici **XWiki**, et tenter d'identifier ses zones sensibles afin de mieux cibler les zones nécessitant plus d'attention.

### 1.2. Qu'est-ce que XWiki ?

**XWiki** est un projet **Open Source** mature \(2003\) écrit en **Java,** distribué selon les termes de la licence **GNU LGPL** et mettant l'accent sur l'extensibilité. Son objectif est de proposer une plateforme générique offrant des services d'exécution pour les applications construites sur cette plateforme.

Même si ce type de solution est très courante sur le net ou dans les intranet de sociétés, attention à ne pas le confondre avec le premier venu. Il se targue en effet d’être non seulement un “**Wiki d’entreprise**” mais aussi un “**Wiki Applicatif**” ce qui fait de lui bien plus qu’un simple outil de gestion d’articles.

XWiki apporte une solution générique et configurable au client. Cela permet d'avoir un seul produit initial et de le décliner de moultes manières suivant les besoins du client. Cette solution va permettre aux clients de XWiki \(typiquement une entreprise nécessitant de regrouper des informations\) d'obtenir sa propre base de connaissance structurée. XWiki propose aussi une interface permettant à ses utilisateurs d'avoir en plus la possibilité de personnaliser les barres latérales de leur interface pour améliorer leur appréhension personnelle de l’outil.

Pour mettre en avant l'ampleur du projet, le code source de l'application dépasse aujourd'hui les 100 000 lignes, il existe plus de 750 extensions et son nombre d'installations actives est estimé à 4500.

## II. Première approche

### 2.1.  Hypothèse de départ <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

Comme mentionné précédemment, notre objectif principal est ici de trouver une façon efficace et pertinente d'identifier les points sensibles d'un projet Open Source. Un point sensible étant, pour nous, un composant dont la panne/chute mettrait en péril le bon fonctionnement d'un projet.

Ainsi, plusieurs questions se posent. Nous pouvons, par exemple, nous demander où trouver les tests existants dans un tel projet. Si il existe une convention permettant de rapidement les différencier du reste du code. Nous pouvons également nous demander si il est réellement nécessaire de tout tester : certains composants \(en CSS, par exemple\) nécessitent-ils autant de tests que d'autres ? Comment pouvons nous alors identifier les zones chaudes d'un code ?

De ces diverses questions découle la problématique à laquelle nous allons essayer d'apporter une réponse dans ce chapitre : _**les zones chaudes d'un projet sont-elles celles qui causent le plus de problèmes ?**_ Une zone chaude étant ici un composant fortement sollicité lors d'une utilisation classique de XWiki.

En cherchant à valider cette hypothèse, nous pourrons ainsi tenter d'identifier les zones les plus sensibles d'un projet tel que XWiki.

### 2.2. Première méthodologie 

Afin de valider cette hypothèse, nous avons envisagé de mettre en place la méthodologie décrite ci-dessous. 

Tout d'abord, nous souhaitions identifier quelles parties de XWiki sont les plus utilisées par des utilisateurs lambda, en récupérant par exemple des statistiques sur le nombre d'utilisations de certains composants. Cette première étape nous aurait permis de commencer à discerner des zones chaudes.

Ensuite, chaque membre de notre groupe aurait installé XWiki puis suivi des cas d'utilisation prédéfinis. Par exemple en éditant certaines pages, en commentant des sections, etc...Nous aurions gardé des traces de nos parcours afin de comparer nos différentes utilisations. Ces traces nous auraient permis de distinguer les composants les plus utilisés lors d'une utilisation très basique de XWiki.

Une fois cette étape complétée, nous aurions comparé les zones chaudes des utilisateurs type de XWiki avec celles identifiées lors de notre propre cartographie. Nos utilisations étant plutôt basiques, il aurait été normal que certains composants n'apparaissent pas dans nos résultats mais soient visibles en récupérant des statistiques globales. En revanche, nous nous attendions à ce que les zones que nous aurions identifiées comme "chaudes" le soient aussi pour des utilisateurs lambdas de XWiki.

En dernier lieu, nous aurions essayé d'établir une corrélation entre les points chauds identifiés dans le code et les composants ayant le plus d'_issues_ critiques.

Malheureusement, plusieurs imprévus ont entravé la mise en œuvre de cette méthodologie.

![](../.gitbook/assets/responsexwiki.png)

Tout d'abord, nous avons rencontré une impossibilité à identifier les "points chauds" des utilisateurs lambdas. En effet, le cœur de XWiki étant composé d’un bundle d’extension, il n’y a malheureusement aucun moyen de savoir quelles parties sont les plus utilisées par l’utilisateur moyen. Faire une carte de chaleur à la main perd alors de son intérêt : en procédant uniquement de cette façon, nous ne serions capable de ne collecter qu’une faible quantité de données. De plus, celles-ci ne seraient pas forcément très représentatives car nos utilisations de XWiki ne seraient pas exhaustives.

Nous avons donc finalement décidé de choisir une nouvelle méthodologie sur laquelle nous appuyer, celle-ci n'étant pas adaptée à notre étude et ne fournissant pas des résultats significatifs. 

En revanche, dans le cas d'une étude sur les extensions additionnelles de XWiki, une telle méthodologie pourrait être adaptée. En effet, contrairement au cœur de XWiki, il est possible de savoir quelles extensions sont les plus utilisées, en se basant sur leur nombre de téléchargements. Ainsi, se baser sur ces informations et des informations récoltées à la main pourrait être intéressant si nous choisissions d'étendre le sujet de cette étude au delà du cœur de XWiki.

## III. Nouvel objectif 

Comme mentionné plus tôt, il n'est pas possible de savoir de façon précise quels composants sont les plus sollicités par les utilisateurs de XWiki. Ainsi, notre première hypothèse reposant sur cette métrique, il a été nécessaire d'en trouver une nouvelle. 

Nous nous sommes donc penchés sur l'hypothèse suivante : _**dans un projet Open Source, une zone sensible est-elle forcément une zone dans laquelle le nombre de bugs soulevés est important ?**_

Avec cette nouvelle approche, nous avons mis en place une nouvelle méthodologie expérimentale : 



## IV. Recherches et expérimentations

### 4.1. Collecte d'informations <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

Métriques + Sources + Hypothèses à prouver

Métriques: Chaleur, complexité d'une méthode, sévérité d'un bug

### 4.2.  Expériences sur XWiki <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

Description des expérimentations menées 

![](../.gitbook/assets/schemaexperiences%20%281%29.png)

## V. Analyse de nos résultats

### 5.1 ???? // Parties en fonction des différents types de résultats/des sources ? <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

### 5.2 ???? <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

###  <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

![](https://lh4.googleusercontent.com/wDkJcwofr25OJ468L0WWyRfI5Vbhn4M5YFN8SWRF989OMnRW_pFhsWC9f4oCm0hviZqjU7-2BOMwg4EVKd4m4BBLsSgL9-JpK6_BHWQqHcvcuyB30isNqORVeBJeX4G8a4hso7Up)

![XWiki components issues](https://lh6.googleusercontent.com/aQAXC5tdJANK-tJ-5yhXHY5sqmIBpZ8-UhLoybQ6agKSH9NNIpk4YOkNGC2FgyHgbac90q1KkwY2RMipSfBTiZW3ux1_YkNa1Mnh0969gEj5w0Gx3D04lZQF5qm9qyQ3Ctn1nQsq)

![](https://lh6.googleusercontent.com/3VCprCHxCBPLG9PrU0x2sRIdlp5UDA7FhcjUQgyf-w0MxtB9rwpbFU9S0aINDIoQwVzCtkyz2viSuTknpjYI_TOEwdxBrfbMgB-8R1qnUPGDmkCpyYoUrFF538KBMbISVfdo3hGG)

## VI. Conclusion 



## VI. Outils\(?\) / Références

###  <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

![](../.gitbook/assets/logo_uns_epu_uca.png)



