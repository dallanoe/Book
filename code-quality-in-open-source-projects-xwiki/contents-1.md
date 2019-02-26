# Projet 2 : Comment identifier les zones "sensibles" d'un projet Open Source ?

## Auteurs 

Nous sommes quatre étudiants en Master 2 d'Architecture logicielle : 

* Rudy Meersman &lt;rudy.meersman@etu.unice.fr&gt;
* Gaétan Duminy &lt;gaetan.duminy@etu.unice.fr&gt;
* Damien Fornali &lt;damien.fornali@etu.unice.fr&gt;
* Amandine Benza &lt;amandine.benza@etu.unice.fr&gt;

## Introduction

De nouvelles technologies émergent chaque jour. Les organisations, Open Source comme privées, produisent de plus en plus de systèmes qui utilisent une multitude de technologies, concepts et outils. 

Dans un tel contexte, de nouveaux problèmes apparaissent. Certaines de ces technologies \(par exemple HTML ou CSS\) ne sont pas forcément testables au sens où on l'entend \(tests unitaires, de non-régression...\) mais peuvent tout de même venir entraver l'expérience des utilisateurs du produit. De nombreuses questions sous-jacentes à ces problèmes émergent. Ainsi, comment pouvons-nous identifier ces technologies, ces zones qui nécessitent plus d'attention afin d'accroître la qualité globale du projet ?

Ce document va présenter les résultats de nos recherches sur l'identification de zones "sensibles" d'un projet Open Source. Nous présenterons donc dans une première partie le contexte de notre recherche puis, dans un second temps, la démarche que nous avons suivie ainsi que les différents résultats obtenus.

## I. Contexte de la recherche

### 1.1. Pourquoi des projets Open Source ? <a id="docs-internal-guid-e7045e26-7fff-fbe0-966c-c04c74baeec5"></a>

À l'heure actuelle, les projets Open Source sont de plus en plus nombreux et populaires. De tels projets impliquent généralement des contraintes différentes et souvent plus "légères", que le développement d'un projet en entreprise du fait de sa liberté de conception. Cela n'impacte pas forcément pour autant la taille de ce genre de projets. En effet, il n'est pas rare qu'un projet Open Source grossisse énormément au fil du temps, tant au niveau de son code que de sa communauté.

Avec la croissance du nombre de contributeurs, on voit également apparaitre une diversité de styles de développement. Cette croissance s’accompagnant de son lot de problèmes divers et variés, lié aussi bien au code des contributeurs que lié aux technologies utilisés, il est alors nécessaire d'être plus vigilant quant aux zones "sensibles" du code développé.

Dans ce contexte, la quantité et la qualité des tests sont des métriques primordiales. Ces tests sont nécessaires pour corriger ou éviter des erreurs pouvant survenir et ainsi pouvoir faire avancer un projet plus rapidement ou encore avec une meilleure gestion.

Cependant, dans un projet de grande envergure, il peut s’avérer difficile de tout tester. Des parties déjà considérées comme stables par les développeurs ne sont plus forcément mises à jour, or elles peuvent à terme devenir une source de problèmes plus ou moins important.

C'est dans ce contexte que se situe notre étude. Nous allons analyser un projet Open Source de grande envergure, ici **XWiki**, et tenter d'identifier ses zones sensibles afin de mieux cibler les zones nécessitant plus d'attention et donner une piste possible à suivre pour améliorer la qualité des tests.

### 1.2. Qu'est-ce que XWiki ?

_**XWiki**_ est un projet **Open Source** mature, démarré en 2003, qui est écrit en très grande partie en **Java,** distribué selon les termes de la licence **GNU LGPL** et mettant l'accent sur l'extensibilité. Son objectif est de proposer une plateforme générique offrant des services d'exécution pour les applications construites sur cette plateforme.

Même si ce type de solution est très courante sur le net ou dans les intranet de sociétés, attention à ne pas le confondre avec le premier venu. Il se targue en effet d’être non seulement un “**Wiki d’entreprise**” mais aussi un “**Wiki Applicatif**” ce qui fait de lui bien plus qu’un simple outil de gestion d’articles.

_XWiki_ apporte une solution générique et configurable au client. Cela permet d'avoir un seul produit initial et de le décliner de diverses façon suivant les besoins du client. Cette solution va permettre aux clients de _XWiki_ \(typiquement une entreprise nécessitant de regrouper des informations\) d'obtenir sa propre base de connaissance structurée. _XWiki_ propose aussi une interface permettant à ses utilisateurs d'avoir en plus la possibilité de personnaliser les barres latérales de leur interface pour améliorer leur appréhension personnelle de l’outil.

Pour mettre en avant l'ampleur du projet, le code source de l'application dépasse aujourd'hui les 100 000 lignes, il existe plus de 750 extensions et son nombre d'installations actives est estimé à 4500.

## II. Approche initiale

### 2.1.  Hypothèse de départ <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

Comme mentionné précédemment, notre objectif principal est ici de trouver une façon efficace et pertinente d'identifier les points sensibles d'un projet Open Source. Un point sensible étant, pour nous, un composant dont la panne/chute mettrait en péril le bon fonctionnement d'un projet.

Ainsi, plusieurs questions se posent. Nous pouvons, par exemple, nous demander où trouver les tests existants dans un tel projet. Si il existe une convention permettant de rapidement les différencier du reste du code. Nous pouvons également nous demander si il est réellement nécessaire de tout tester : certains composants, comme ceux écrit en CSS par exemple, nécessitent-ils autant de tests que d'autres ? Comment pouvons nous alors identifier les zones chaudes d'un code ?

De ces diverses questions découle la problématique à laquelle nous allons essayer d'apporter une réponse dans ce chapitre : _**les zones chaudes d'un projet sont-elles celles qui causent le plus de problèmes ?**_  Une zone chaude étant ici un composant fortement sollicité lors d'une utilisation classique de _XWiki_.

En cherchant à valider cette hypothèse, nous pourrons ainsi tenter d'identifier les zones les plus sensibles d'un projet tel que _XWiki_.

### 2.2. Première méthodologie 

Afin de valider cette hypothèse, nous avons envisagé de mettre en place la méthodologie décrite ci-dessous. 

Tout d'abord, nous souhaitions identifier quelles parties de _XWiki_ sont les plus utilisées par des utilisateurs lambda, en récupérant par exemple des statistiques sur le nombre d'utilisations de certains composants. Cette première étape nous aurait permis de commencer à discerner des zones chaudes.

Ensuite, chaque membre de notre groupe aurait installé _XWiki_ puis suivi des cas d'utilisation prédéfinis. Par exemple en éditant certaines pages, en commentant des sections, etc...Nous aurions gardé des traces de nos parcours afin de comparer nos différentes utilisations. Ces traces nous auraient permis de distinguer les composants les plus utilisés lors d'une utilisation très basique de _XWiki_.

Une fois cette étape complétée, nous aurions comparé les zones chaudes des utilisateurs type de _XWiki_ avec celles identifiées lors de notre propre cartographie. Nos utilisations étant plutôt basiques, il aurait été normal que certains composants n'apparaissent pas dans nos résultats mais soient visibles en récupérant des statistiques globales. En revanche, nous nous attendions à ce que les zones que nous aurions identifiées comme "chaudes" le soient aussi pour des utilisateurs lambdas de _XWiki_.

En dernier lieu, nous aurions essayé d'établir une corrélation entre les points chauds identifiés dans le code et les composants ayant le plus d'_issues_ critiques.

Malheureusement, plusieurs imprévus ont entravé la mise en œuvre de cette méthodologie.

![](../.gitbook/assets/responsexwiki.png)

Tout d'abord, nous avons rencontré une impossibilité à identifier les "points chauds" des utilisateurs lambdas. En effet, le cœur de _XWiki_ étant composé d’un bundle d’extension, il n’y a malheureusement aucun moyen de savoir quelles parties sont les plus utilisées par l’utilisateur moyen. Faire une carte de chaleur à la main perd alors de son intérêt : en procédant uniquement de cette façon et en n'utilisant que les données récupérées de nos propre parcours, nous ne serions capable de ne collecter qu’une faible quantité de données et donc avoir des résultats biaisés, ce qui n'est pas notre objectif. De plus, celles-ci ne seraient pas forcément très représentatives car nos utilisations de _XWiki_ ne seraient pas exhaustives.

Nous avons donc finalement décidé de choisir une nouvelle méthodologie sur laquelle nous appuyer, celle-ci n'étant pas adaptée à notre étude et ne fournissant pas des résultats significatifs. 

En revanche, dans le cas d'une étude sur les extensions additionnelles de _XWiki_, une telle méthodologie pourrait être adaptée. En effet, contrairement au cœur de _XWiki_, il est possible de savoir quelles extensions sont les plus utilisées, en se basant sur leur nombre de téléchargements. Ainsi, se baser sur ces informations et des informations récoltées à la main pourrait être intéressant si nous choisissions d'étendre le sujet de cette étude au delà du cœur de _XWiki_.

## III. Nouvel objectif 

Comme mentionné plus tôt, il n'est pas possible de savoir de façon précise quels composants sont les plus sollicités par les utilisateurs de _XWiki_. Ainsi, notre première hypothèse reposant sur cette métrique, il a été nécessaire d'en trouver une nouvelle. 

Nous nous sommes donc penchés sur l'hypothèse suivante : _**dans un projet Open Source, une zone sensible est-elle forcément une zone dont la couverture de tests est importante ?**_

Avec cette seconde approche, nous avons mis en place une nouvelle méthodologie expérimentale :

1. Tout d'abord, partir du projet complet, ici _XWiki_, et déterminer, parmi les plus gros sous-projets, ceux ayant le plus de **bugs** non résolus. _XWiki_ propose de nombreuses extensions, de ce fait, nous ne pouvons malheureusement pas toutes les étudier dans le cadre de cette étude. Nous avons donc cherché à restreindre notre **scope** de recherche sur un ou plusieurs sous-projets.
2. Ensuite, afin que l'étude soit la plus représentative possible, identifier le sous-projet le plus populaire grâce au nombre de participations dessus ainsi que le nombre de branches actuelle pour localiser les bugs ayant le plus de chance d'entraver l’expérience utilisateur. 
3. Une fois le sous-projet choisi, définir la **sévérité** des bugs des composants présentant le plus d'issues.
4. Parmi ces composants, identifier, cette fois, les **classes** associées à ces issues.   
5. Indépendamment des points deux, trois et quatre, se baser sur le sous-projet identifié dans le second point. Récupérer la **complexité** ainsi que la **couverture** de tests de chacune des classes de ce sous-projet.
6. Essayer d'établir une corrélation entre les classes identifiées dans le quatrième point et leur complexité et couverture de code.

Cette nouvelle approche va nous permettre de valider ou invalider l'hypothèse précédente, qui elle même propose une piste à la résolution de notre question globale.

## IV. Recherches et expérimentations

### 4.1. Collecte d'informations <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

**Sources**

Afin de collecter des données \(voir expériences, _Livrable L3_\), nous avons utilisé différentes sources.

* **Github**

_Github_ est l'hôte des sources de _XWiki_. Il nous a permis d'avoir une meilleur vu de l'architecture global du projet ainsi que de définir le sous-projet \(repository\) sur lequel nous concentrer. Avec plus de temps, nous aurions pu en plus faire une analyse plus en profondeur des parties chaudes, qu'on a découvertes au fil de cette recherche, grâce au code fournis.

* **Jira**

_Jira_ est le système de tickets utilisé par _XWiki_. Il nous a permis de parcourir les tickets levés par l'équipe de développement et d'en récupérer les bugs associés. Ces bugs nous on fournit leurs sévérité ainsi que leurs emplacement dans le code.

* **Clover**

_XWiki_ utilise _Clover_ afin d'obtenir de nombreuses informations quant à la qualité de son code. C'est notre source principale de métriques \(complexité et couverture de code\). Par ailleurs, il stocke les rapports générés. Étant disponibles au public, nous en avons utilisé dans nos expériences. Ces informations sont la complexité du code ainsi que leurs couvertures. Ces informations nous ont d'ailleurs aussi donné une sorte de carte de chaleur.

* **Jenkins**

_Jenkins_ nous permet de relier le code source \(_Github_\) aux problèmes relevés \(_Jira_\). Cependant il ne stocke seulement que les informations des 20 derniers builds générés. Il nous aura permis de connaitre les tests effectués et d'avoir une idée des problèmes du projet actuel. Cependant il nous aura été que peu utile après la découverte du Clover du projet.

**Métriques**

Ayant fait évoluer notre direction au cours du projet, nous avons aussi fait évoluer nos métriques. De ce fait, nous les avons choisis en fonction à la fois des données initialement collectées, mais aussi, en fonction de celles récupérées lors de l'application de notre nouvelle démarche.

Afin que nos expériences puissent être claires pour les lecteurs, nous définissons ici les métriques utilisées.

#### **Métriques de couverture de code**

Nos expériences introduisent la notion de couverture de code. Cette notion est composite et pour obtenir la couverture globale, une fonction est appliquée sur les trois métriques suivantes.

* _Couverture de branche._ 

Cette métrique mesure quelles branches possibles dans les structures de contrôle de flux sont suivies. Sur _Clover_, elle est obtenue en enregistrant si l'expression booléenne dans la structure de contrôle a été évaluée à la fois à vraie et à la fois fausse pendant l'exécution.

* _Couverture d'instruction_

La couverture d'instruction est une métrique mesurant quelles instructions d'un corps de code ont été exécutées au cours d'un test, et quelles instructions ne l'ont pas été.

* _Couverture de méthode_

La couverture de méthode est une métrique mesurant si une méthode a été accédée pendant l'exécution d'un programme.

#### **Métriques de complexité de code**

Nous introduisons aussi la notion de complexité d'un code.

* _Complexité_

C'est la métrique globale donnant la complexité cyclomatique d'une entité dans un contexte donné. Les contextes possibles étant une _classe_, un _package_ ou encore un _projet_.

* _Complexité d'une méthode_

C'est une métrique calculée de manière arbitraire, par exemple, sous _Clover_ le calcul est effectué de la façon suivante:

1. _`Méthode vide: 1 point`_
2. _`Instruction unique: 0 point`_
3. _`Bloc Switch: (nombre de Case) points`_
4. _`Bloc Try Catch: (nombre de Catch) points`_ 
5. _`Expression Ternaire: 1 point`_
6. _`Expression Booléenne: (nombre de && ou ||) points`_

### 4.2.  Expériences sur XWiki <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

En suivant la méthodologie présentée plus tôt, nous pouvons discerner cinq expérimentations distinctes.

Vous trouverez ci-dessous un schéma résumant notre démarche.

![](../.gitbook/assets/schemaexperiences.png)

### 4.2.1. Expériences 1-2-3 <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

Les trois premières vont consister à de plus en plus réduire le scope de nos recherches : nous allons initialement nous baser sur un projet complet, puis sur un sous-projet, puis sur certains de ses composants, et enfin sur des classes présentes dans ces composants. Dans ce cas, il s'agit de récupérer les données sur Jira afin de pouvoir les exploiter.

Pour la première nous allons pouvoir récupérer, sur les 1000 derniers bugs recensés, leurs propriétés allant de leurs emplacements à leurs descriptions ainsi que la priorité de ceux-ci nous donnant ainsi une piste à exploiter. 

Pour la seconde, on va exploiter les résultats de la première pour cibler les composants les plus touchés par les bugs. On récupère ensuite les bugs de ces composants-ci et regardons leurs sévérité afin de pouvoir créer nos premières métriques utilisables pour notre hypothèse.

Pour la troisième, nous zoomons une dernière fois sur les classes pour obtenir leur chemin, et ainsi donc des détails supplémentaires, sur les classes causant des problèmes. On aura ainsi une métrique plus fine et détaillé.

### 4.2.2. Expériences 4 <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

La quatrième expérience va consister à repartir du sous-projet identifié dans la première expérience, puis à récupérer la complexité et la couverture de test de chacune des classes du dit sous-projet. On va pour cela utiliser les données fournis par Clover. On va récupérer les données de couverture de test afin d'avoir des données avec des valeurs plus lisibles, et surtout exploitables, que ceux présents sur le site.

### 4.2.3. Expériences 5 <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

Il s'agit de la mise en relation des résultats des expériences 3 et 4. On va prendre les résultats obtenus lors de l'expérience 3 sur les classes du projet puis on va récupérer les résultats des couvertures de tests sur les classes de l'expérience 4 pour avoir des données correspondantes au résultat de notre hypothèse. 

## V. Analyse de nos résultats

Nous présentons dans cette partie les résultats de nos différentes expériences.

### 5.1. Expériences 1-2-3 <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

* _Expérience 1_ 

Les données recueillies lors de l’expérience sont compté par sous-projet et priorité de bugs. Nous avons ainsi obtenu les résultats suivant:

![](../.gitbook/assets/image%20%286%29.png)

On remarque qu’une énorme parties des bugs ce retrouvent être le projet XWiki Platform. Parmi les autres données, bien moins représentatives, nous avons XWiki Rendering et XWiki Commons. Cependant XWiki Platform confirme sa place de sous-projet à analyser grâce à la sévérité de ses bugs

![](../.gitbook/assets/image%20%285%29.png)

* _Expérience 2_

Suite aux résultats obtenus dans l’expérience 1, nous avons pu créer ce tableau de valeurs:

![](../.gitbook/assets/image%20%283%29.png)

On remarque un total de bug assez élevé dont les plus nombreux sont présents dans le module _OldCore_ et _Web - Templates & Ressources._ Les parties les moins touchées 

* _Expérience 3_ 

\_\_

### 5.2. Expérience 4 <a id="docs-internal-guid-51382e29-7fff-2108-5bbb-1ef6c6d7fddd"></a>

### 5.3. Expérience 5

## VI. Conclusion 



## VI. Références

* Les [sources](https://github.com/xwiki/xwiki-platform) _Github_ du projet.
* Le topics utilisés sur le forum _XWiki_ pour communiquer avec les développeurs:
  * [Topic 1](https://forum.xwiki.org/t/student-what-are-the-hot-spots-of-xwiki-code/4213/2)
  * [Topic 2](https://forum.xwiki.org/t/student-issues-code-linking/4329)
* Les données [Clover](http://maven.xwiki.org/site/clover/20190202/clover-commons+rendering+platform-20190202-0222/dashboard.html) permettant de lier _Jira_ et _Github_ pour les 20 derniers commits.
* Le tableau d'ensemble listant tous les serveurs composant l'écosystème [_XWiki_](https://dev.xwiki.org/xwiki/bin/view/Community/DevelopmentPractices#HGeneralDevelopmentFlow).
* Le [système](https://jira.xwiki.org/secure/Dashboard.jspa) de tickets utilisé par _XWiki_.
* Les [extensions](https://extensions.xwiki.org/xwiki/bin/view/Main/WebHome) _XWiki_.

![](../.gitbook/assets/logo_uns_epu_uca.png)



