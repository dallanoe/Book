# Projet 2 : Comment identifier les zones sensibles d'un code Open Source ?

**Date de rendu finale : March 2018 au plus tard**

Remarques :

Les titres peuvent changer pour être en adéquation avec votre étude.

De même il est possible de modifier la structure, celle qui est proposée ici est là pour vous aider.

Utilisez des références pour justifier votre argumentaire, vos choix etc.

## Authors

Nous sommes quatre étudiants en Master 2 d'Architecture logicielle : 

* Rudy Meersman &lt;rudy.meersman@etu.unice.fr&gt;
* Gaétan Duminy &lt;gaetan.duminy@etu.unice.fr&gt;
* Damoy Fornali &lt;damien.fornali@etu.unice.fr&gt;
* Amandine Benza &lt;amandine.benza@etu.unice.fr&gt;

## I. Contexte de recherche / projet

### 1.1. Présentation de XWiki <a id="docs-internal-guid-e7045e26-7fff-fbe0-966c-c04c74baeec5"></a>

* Présenter XWiki
* But/Contexte/Contributeur
* Pourquoi intéressant étudier XWiki et projets Open Source en général ? 
* Projet OpenSource lancé en 2003 \(+15 ans\)
* Wiki d’entreprise
* Plus de 100 000 lignes de code
* 750 extensions
* 4500 installations actives
* Projet de grande envergure

### 1.2 Objectifs et intérêt

* **Intérêts :**
* Étude d’un projet de grande envergure \(750 modules développés, + 100K lignes, de nombreuses branches et releases\): c’est l’opportunité de s’investir dans un gros projet open source.
* Opportunité de découvrir à quel point le test est pris au sérieux dans une application professionnelle commercialisée.
* Opportunité de tenter d’identifier des problèmes qui ne sont pas forcément connus des développeurs du projet 
* **Objectifs :** 
* L’objectif concret serait le suivant : à partir des issues se trouvant sur JIRA, des tests existants, des rapports d'engagement et des rapports de Clover, identifier où la qualité devrait être améliorée et où des tests automatisés devraient être nécessaires dans XWiki .
* Augmenter la couverture de tests / automatisation de tests \(facilité à tester: augmentation de la fréquence de tests..\) devrait améliorer la qualité du code open sourc

## II. Observations / Question générale

### 2.1  Question Générale <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

* Plusieurs questions se posent : Où trouver les tests existants ? Est-il nécessaire de tout tester ? Comment trouver les zones chaudes d'un code ?
* Une zone chaude étant ici un composant fortement sollicité lors d'une utilisation classique de XWiki. \(On associe ici la métrique de la chaleur à la fréquence d'accès à un composant lors d'une utilisation classique de XWiki\)
* On arrive donc à l'hypothèse suivante : les points chauds d'un projet sont-ils ceux qui causent le plus de problèmes?

### 2.2 Raisonnement/Méthodologie

* **Méthodologie de départ :**
* Trouver quelles parties de XWiki sont les plus utilisées par des utilisateurs lambda.
* Installer XWiki et suivre des cas d’utilisations prédéfinis.
* Comparer nos différentes utilisations pour trouver les composants les plus utilisés.
* Essayer de lier les points “chauds” du code avec les parties posant les plus de problèmes \(avec le plus d’issues\).
*  **Soucis d’une telle méthodologie :**
* Impossibilité d’identifier les points chauds des utilisateurs lambda : le coeur de XWiki étant composé d’un bundle d’extension, il n’y a malheureusement aucun moyen de savoir quelles parties sont les plus utilisées par l’utilisateur moyen. Il est en revanche possible de savoir quelles extensions additionnelles sont les plus utilisées, en se basant sur leur nombre de téléchargements. 
* =&gt; Cette partie n’est pas forcément utile pour nous puisque nous voulons nous baser sur le cœur de XWiki.
* Faire une heatmap à la main perd alors de son intérêt : car nous ne serions capable de ne collecter qu’une faible quantité de données. Ces données ne seraient pas forcément très représentatives car nos utilisations de XWiki ne seraient pas exhaustives.
* De plus difficultés à lier le code avec les pages XWiki associées.

## III. Collecte d''informations

Préciser vos zones de recherches en fonction de votre projet,

1. les articles ou documents utiles à votre projet
2. les outils

## IV. Expériences et hypothèses

1. Il s'agit ici d'énoncer sous forme d' hypothèses ce que vous allez chercher à démontrer. Vous devez définir vos hypothèses de façon à pouvoir les _mesurer facilement._ Bien sûr, votre hypothèse devrait être construite de manière à v_ous aider à répondre à votre question initiale_.Explicitez ces différents points.
2. Test de l’hypothèse par l’expérimentation. 1. Vos tests d’expérimentations permettent de vérifier si vos hypothèses sont vraies ou fausses. 2. Il est possible que vous deviez répéter vos expérimentations pour vous assurer que les premiers résultats ne sont pas seulement un accident.
3. Explicitez bien les outils utilisés et comment.
4. Justifiez vos choix



## V. Résultats, analyse et conclusion

1. Analyse des résultats & construction d’une conclusion : Une fois votre expérience terminée, vous récupérez vos mesures et vous les analysez pour voir si votre hypothèse tient la route. 

![](https://lh4.googleusercontent.com/wDkJcwofr25OJ468L0WWyRfI5Vbhn4M5YFN8SWRF989OMnRW_pFhsWC9f4oCm0hviZqjU7-2BOMwg4EVKd4m4BBLsSgL9-JpK6_BHWQqHcvcuyB30isNqORVeBJeX4G8a4hso7Up)

![XWiki components issues](https://lh6.googleusercontent.com/aQAXC5tdJANK-tJ-5yhXHY5sqmIBpZ8-UhLoybQ6agKSH9NNIpk4YOkNGC2FgyHgbac90q1KkwY2RMipSfBTiZW3ux1_YkNa1Mnh0969gEj5w0Gx3D04lZQF5qm9qyQ3Ctn1nQsq)

![](https://lh6.googleusercontent.com/3VCprCHxCBPLG9PrU0x2sRIdlp5UDA7FhcjUQgyf-w0MxtB9rwpbFU9S0aINDIoQwVzCtkyz2viSuTknpjYI_TOEwdxBrfbMgB-8R1qnUPGDmkCpyYoUrFF538KBMbISVfdo3hGG)

## VI. Outils \(facultatif\)

Précisez votre utilisation des outils ou les développements \(e.g. scripts\) réalisés pour atteindre vos objectifs. Ce chapitre doit viser à \(1\) pouvoir reproduire vos expériementations, \(2\) partager/expliquer à d'autres l'usage des outils.

## VI. Références



![](../.gitbook/assets/logo_uns%20%281%29.png) UCA : University Côte d'Azur \(french Riviera University\)

