# Projet 2 : Comment identifier les zones "sensibles" d'un projet Open Source ?

## Auteurs 

Nous sommes quatre étudiants en Master 2 d'Architecture logicielle : 

* Rudy Meersman &lt;rudy.meersman@etu.unice.fr&gt;
* Gaétan Duminy &lt;gaetan.duminy@etu.unice.fr&gt;
* Damien Fornali &lt;damien.fornali@etu.unice.fr&gt;
* Amandine Benza &lt;amandine.benza@etu.unice.fr&gt;

## Introduction

Des technologies émergent tous les jours. Les organisations, Open Source comme privées, produisent de plus en plus des systèmes qui utilisent une multitude de technologies, concepts et outils. Dans un tel contexte, de nouveaux problèmes apparaissent. Certaines de ces technologies \(par exemple HTML ou CSS\) ne sont pas forcément testables au sens où on l'entend \(tests unitaires, de non-régression...\) mais peuvent tout de même venir entraver l'expérience des utilisateurs du produit. De nombreuses questions sous-jacentes à ce problèmes émergent. Avant de proposer une méthodologie afin de tenter de répondre à ce problème, comment pouvons nous identifier ces technologies, ces zones qui nécessitent plus d'attention afin d'accroître la qualité globale du projet ?

Ce document va donc présenter les résultats de nos recherches sur l'identification de zones "sensibles" d'un projet Open Source. Open Source, car il est assez peu envisageable de travailler sur un projet sans posséder ses sources ainsi que les informations relatives aux problèmes rencontrés. Afin de les présenter concrètement, nous présentons dans une première partie le contexte de notre recherche. Ensuite, nous présenterons notre démarche ainsi que les résultats que nous avons obtenus.

## I. Contexte de la recherche

### 1.1. Qu'est-ce que XWiki ? <a id="docs-internal-guid-e7045e26-7fff-fbe0-966c-c04c74baeec5"></a>

**XWiki** est un projet **Open Source** mature \(2003\) écrit en **Java,** distribué selon les termes de la licence **GNU LGPL** et mettant l'accent sur l'extensibilité. Son objectif est de proposer une plateforme générique offrant des services d'exécution pour les applications construites sur cette plateforme

Même si ce type de solution est très courante sur le net ou dans les intranet de sociétés, attention à ne pas le confondre avec le premier venu. Il se targue en effet d’être non seulement un “**Wiki d’entreprise**” mais aussi un “**Wiki Applicatif**” ce qui fait de lui bien plus qu’un simple outil de gestion d’articles.

XWiki apporte une solution générique et configurable au client. Cela permet d'avoir un seul produit initial et de le décliner de moultes manières suivant les besoins du client. Cette solution va permettre aux clients de XWiki \(typiquement une entreprise nécessitant de regrouper des informations\) d'obtenir sa propre base de connaissance structurée. XWiki propose aussi une interface permettant à ses utilisateurs d'avoir en plus la possibilité de personnaliser les barres latérales de leur interface pour améliorer leur appréhension personnelle de l’outil.

Pour mettre en avant l'ampleur du projet, le code source de l'application dépasse les 100 000 lignes, il existe plus de 750 extensions et le nombre d'installations actives est estimé à 4500.

Étudier un tel projet a une valeur inestimable. Vu la croissance des projets ouverts à multiple contributeurs, il est probable que nous soyons impliqués dans de tel projets dans notre carrière professionnelle. 

### 1.2. Pourquoi des projets Open Source ?

Les projets Open Source sont de plus nombreux et populaires. Ceci est dû au fait qu'un tel projet implique généralement des contraintes différentes, souvent plus légères, que le développement d'un projet en entreprise. Cependant, ils peuvent très facilement grossir aussi bien au niveau du code qu’au niveau de sa communauté. Un projet d’une aussi grande taille créait des problèmes aussi bien gênants que variés. Son côté OpenSource est lui aussi source de bugs. En effet, plusieurs personnes pouvant participer inclus plusieurs façons de coder et donc plus de chance d’avoir des erreurs. Dans ce contexte, la qualité et la quantité de tests est primordial pour corriger ou éviter tous les soucis lié au code et à sa mise en place. Cependant, il est possible d’oublier ou alors de sauter une partie de code qui nous semble peu important mais qui peut mener à des cas problématiques mettant plusieurs heures, voir jours, pour être résolus dans un OpenSource entrainant donc une perte de temps qui accumulé, est considérable.

Dans ce contexte, nous allons analyser le projet Xwiki avec plusieurs outils, sur lesquels le programme est hébergé, afin de fournir une solution ou piste pour répondre à ce problème. Pour cela nous avons Jira qui, grâce à son dashboard, nous fournira certaines informations sur le code en lui-même. Nous allons aussi utiliser Clover pour voir plus en profondeur les tests déjà existants et leur portée. Le code est hébergé sur Github, permettant ainsi l’analyse en profondeur des tests ou encore du code en lui même. Les résultats de ces outils seront ensuite mis en corrélation afin de fournir une réponse à cette problématique et aux questions que nous allons traiter tout au long de ce chapitre.

* **Intérêts :**
* Étude d’un projet de grande envergure \(750 modules développés, + 100K lignes, de nombreuses branches et releases\): c’est l’opportunité de s’investir dans un gros projet open source. 
* **Objectifs :** 
* L’objectif concret serait le suivant : à partir des issues se trouvant sur JIRA, des tests existants, des rapports d'engagement et des rapports de Clover, identifier où la qualité devrait être améliorée et où des tests automatisés devraient être nécessaires dans XWiki .
* Augmenter la couverture de tests / automatisation de tests \(facilité à tester: augmentation de la fréquence de tests..\) devrait améliorer la qualité du code open sourc

## II. Question générale

### 2.1.  Hypothèse <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

Comme mentionné précédemment, notre objectif principal est ici de trouver une façon efficace et pertinente d'identifier les points sensibles d'un projet Open Source. Un point sensible étant, pour nous, un composant dont la panne/chute mettrait en péril le bon fonctionnement d'un projet.

Ainsi, plusieurs questions se posent. Nous pouvons, par exemple, nous demander où trouver les tests existants dans un tel projet. Si il existe une convention permettant de rapidement les différencier du reste du code. Nous pouvons également nous demander si il est réellement nécessaire de tout tester : certains composants \(en CSS, par exemple\) nécessitent-ils autant de tests que d'autres ? Comment pouvons nous alors identifier les zones chaudes d'un code ?

De ces diverses questions découle la problématique à laquelle nous allons essayer d'apporter une réponse dans ce chapitre : les zones chaudes d'un projet sont-elles celles qui causent le plus de problèmes ? Une zone chaude étant ici un composant fortement sollicité lors d'une utilisation classique de XWiki.

En cherchant à valider cette hypothèse, nous pourrons ainsi tenter d'identifier les zones les plus sensibles d'un projet tel que XWiki.

### 3.3.  Sources <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

### 2.2. Méthodologie de départ

La première méthodologie que nous avions envisagé de mettre en place était la suivante:

* 1° : Identifier les parties de XWiki les plus utilisées par des utilisateurs lambda.
* 2° : Installer XWiki et suivre des cas d'utilisations prédéfinis en gardant une trace de nos parcours.
* 3° : Comparer nos différentes utilisations afin d'identifier les composants les plus utilisés.
* 4° : S'assurer que les composants que nous avons le plus utilisés lors de nos parcours font bien partie de ceux par lesquels passent le plus les utilisateurs moyens.
* 5° : Essayer de lier ces points "chauds" du code de XWiki avec les parties posant le plus de problèmes. C'est à dire les composants ayant le plus d'issues critiques.

Malheureusement, plusieurs imprévus ont entravé la mise en œuvre de cette méthodologie.

Tout d'abord, nous avons rencontré une impossibilité à identifier les "points chauds" des utilisateurs lambdas. En effet, le cœur de XWiki étant composé d’un bundle d’extension, il n’y a malheureusement aucun moyen de savoir quelles parties sont les plus utilisées par l’utilisateur moyen. Faire une carte de chaleur à la main perd alors de son intérêt : en procédant uniquement de cette façon, nous ne serions capable de ne collecter qu’une faible quantité de données. De plus, celles-ci ne seraient pas forcément très représentatives car nos utilisations de XWiki ne seraient pas exhaustives.

Nous avons donc finalement décidé de choisir une nouvelle méthodologie sur laquelle nous appuyer, celle-ci n'étant pas adaptée à notre étude et ne fournissant pas des résultats significatifs. 

En revanche, dans le cas d'une étude sur les extensions additionnelles de XWiki, une telle méthodologie pourrait être adaptée. En effet, contrairement au cœur de XWiki, il est possible de savoir quelles extensions sont les plus utilisées, en se basant sur leur nombre de téléchargements. Ainsi, se baser sur ces informations et des informations récoltées à la main pourrait être intéressant si nous choisissions d'étendre le sujet de cette étude au delà du cœur de XWiki.

### 3.1.  Nouvelle Méthodologie <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

### 3.2.  Métriques <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

## III. Collecte d''informations

## IV. Recherches et experimentations

## V. Analyse de nos résultats

### 4.1. Hypothèses à démontrer <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

### 4.2.  Expériences sur XWiki <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

![](https://lh4.googleusercontent.com/wDkJcwofr25OJ468L0WWyRfI5Vbhn4M5YFN8SWRF989OMnRW_pFhsWC9f4oCm0hviZqjU7-2BOMwg4EVKd4m4BBLsSgL9-JpK6_BHWQqHcvcuyB30isNqORVeBJeX4G8a4hso7Up)

![XWiki components issues](https://lh6.googleusercontent.com/aQAXC5tdJANK-tJ-5yhXHY5sqmIBpZ8-UhLoybQ6agKSH9NNIpk4YOkNGC2FgyHgbac90q1KkwY2RMipSfBTiZW3ux1_YkNa1Mnh0969gEj5w0Gx3D04lZQF5qm9qyQ3Ctn1nQsq)

![](https://lh6.googleusercontent.com/3VCprCHxCBPLG9PrU0x2sRIdlp5UDA7FhcjUQgyf-w0MxtB9rwpbFU9S0aINDIoQwVzCtkyz2viSuTknpjYI_TOEwdxBrfbMgB-8R1qnUPGDmkCpyYoUrFF538KBMbISVfdo3hGG)

## VI. Conclusion 

## VI. Outils\(?\) / Références

UCA : University Côte d'Azur \(french Riviera University\)![](../.gitbook/assets/logo_uns%20%281%29.png)

### 5.1. ???? // Parties en fonction des différents types de résultats/des sources ? <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

### 5.2. ???? <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

