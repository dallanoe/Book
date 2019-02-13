# Est-ce que les erreurs de merges viennent du code ajouté ou du code déjà présent ?

## Authors

* Chennouf Mohamed &lt;mohamed.chennouf@etu.unice.fr&gt; 
* Huang Shiyang &lt;shiyang.huang@etu.unice.fr
* Swiderska Joanna &lt;joanna.swiderska@etu.unice.fr&gt;
* Wilhelm Andreina &lt;andreina-simonett.wilhelm-garcia@etu.unice.fr&gt;

## I. Context

GIT est le logiciel de gestion de version le plus populaire au monde. Git gère l'évolution du contenu d'un projet et permet de synchroniser du code entre plusieurs collaborateurs. 

Durant nos études et nos expériences professionnelles, nous avons tous été confronté à travailler en équipe sur des projets divers et variés. Dans la majorité des cas, nous utilisons GIT pour versionner nos travaux. Au sein d’une équipe de travail, il est courant de créer des branches avec git afin que les membres de l’équipe puissent travailler sur des parties du projet sans impacter le projet actuel. Une fois le travaille sur la branche X accompli, il est nécessaire d’ajouter ce travail dans la branche principale du projet. Pour synchroniser ces branches, il existe deux méthodes : Merge et Rebase. 

Pour notre étude nous nous intéressons aux merges car c’est la synchronisation que l’on utilise le plus souvent durant nos projets. Un merge permet d’avancer la branche principale en incorporant le travail d’une autre branche. Cette opération join et fusionne les deux points de départ de ces deux branches dans un commit de fusion.

Voici un schéma pour illustrer un merge :

![1. Sch&#xE9;ma d&#x2019;un merge](../.gitbook/assets/image.png)





Un merge permet d’avancer la branche principale \( en blue \) en incorporant le travail d’une autre branche \(en vert\) . Bien que GIT soit un excellent logiciel de gestion de versions, les merges nous ont parfois causé quelques problèmes :

**Les conflits :** 

En effet, il nous est déjà arrivé d’avoir des conflits sur des merges. Les conflits se produisent lorsqu'on fusionne des branches ayant des commits concurrents. Git a besoin de notre aide pour décider quelles modifications seront intégrées à la fusion finale. La plupart du temps cela a lieu : lorsque plusieurs utilisateurs modifient la même section de code ou lorsqu'une personne modifie un fichier et une autre le supprime. Après résolution du conflit, les merges peuvent provoquer des erreurs dans le projet.

**Les erreurs de merges :** 

Qu’il y ai conflit ou pas, les merges peuvent mal se passer lorsque le projet ne se compile pas ou s'exécute de façon inattendue \(erreurs …\). Par exemple cela peut se produire quand: 

* Du code ajouté est mal écrit
* Du code ajouté marche mais s’intègre mal avec le reste du projet
* Des tests qui ne sont pas mise à jour
* Des tests mal écrit

## II. Questions générales

**1. Existe-t'il vraiment des erreurs de merge ?**  


Nous nous sommes dit qu’il est possible qu’un merge se passe bien mais qu’il entraîne des erreurs dans le code. Afin de prouver que ce cas existe, nous avons pris les deux exemples suivants comme point appuis :

* Un merge se passe bien mais le projet ne se compile pas car il y a une ou plusieurs fautes de codes comme par exemple une erreur de frappes.
* Un merge se passe bien et il n’y a pas d’erreur de compilation mais certaines fonctions du projet ne marchent pas car il y a des modifications sur des interfaces ou des conditions qui ont impacté l’intégralité du système.

Ces deux exemples nous amène à nous poser la question suivante :  
****

**2. Comment repérer qu’un système ne se compile pas ou se compile mais a un comportement inattendu ?**  


De nos connaissances, le moyen le plus efficace pour savoir si un projet ne compile pas est de s'intéresser aux outils d'intégration continue qui propose, pour la plupart, des états du projet lors de chaque merge.  


Par exemple, sur les outils Jenkins et Travis, lorsqu’un projet ne compile pas un voyant rouge est affiché alors que lorsque les tests ne passent pas un voyant orange est affiché. Nous avons fait l’hypothèse que le projet compile et ne marche pas lorsque les tests ne passent pas.

De cette manière, en inspectant les outils intégrations, il nous sera possible de déterminer quelles sont les merges qui se sont en erreur. Pour débuter, nous allons choisir un projet qui:

* utilise un langage qu’on connais.
* a un accès public à son outils d'intégration continue.
* a suffisamment de merge qui se passe mal.

**3. Comment savoir si les erreurs de merges viennent du code ajouté ou du code déjà présent ?**

Intuitivement nous nous somme dit que les erreurs de merge peuvent venir :

* du code ajouté mal écrit
* du code ajouté qui marche mais qui s’intègre mal avec le reste du projet
* des tests qui ne sont pas mis à jour
* des tests mal écrit

A partir de ces idées nous avons décidé de prouver nos intuitions en créant des règles. Ces règles sont spécifique à chacune de nos intuitions que l’on testera sur plusieurs projet afin de conclure sur la provenance des erreurs \(codé ajouté ou code présent ? \) .

**Règles :**

_**Tests pas mis à jour :**_ 

_`Commit_Error : files [ x.java, v.java] ---> Commit_Good : files [x.test ]`_

_**Tests mal écrit :**_ 

_`Commit_Error : files [ x.test, v.test] ---> Commit_Good : files [ x.test ]`_

_**Code ajouté défectueux :**_ 

_`Commit_Error : files [x.java, v.java] ---> Commit_Good : files [ x.java]`_

_`Commit_Good : files [ x.java, o.java] ---> Commit_Error : files [x.test, v.test, o.test] ---> Commit_Good : files [x.java]`_

_**Code ajouté marche mais produit des erreurs avec le reste du système :**_

_`Commit_Error : files [x.java , v.java] ---> Commit_Good : files [ o.java ]`_  **``**  


Dans un premier temps nous nous basé sur les nom des fichiers qui interviennent lors d’un Merge qui se passe mal. En raisonnant sur les commites avant et après celui qui a causé l’erreur, il est possible d’en déduire que :

* les tests n’ont pas été mis à jour ,
* les tests ont été mal écrit
* le code ajouté est défectueux
* le code ajouté marche mais produit des erreurs au sein du système.

**4. A t’on accès aux informations qui nous intéresse ?**

Durant la question “Comment savoir si les erreurs de merges viennent du code ajouté ou du code déjà présent ?”, nous avons supposé avoir :

* les commites en erreurs d’un Merge
* les commites qui précède et succède celui en erreur
* le nom des fichiers qui interviennent durant un commite

Mais comment avoir accès au informations qui nous intéresse ?

Deux idées sont possible : Commande **Git shell** ou **API gitHub**. Nous avons préféré prendre API de github car grâce à l’API il est possible de  récupérer directement les objets que l’’on cherche sans avoir à faire du traitement sur les données reçus \(parsing, différence …\).

**5. Sur quelle projet tester nos règles?**

Nous avons décidé de prendre SonarQube comme premier projet test car il a :

* Un serveur d’intégration accessible : travis
* Un nombre de merge conséquent qu’il soit bon ou en erreur
  * 3185 pull request fermés
  * 2181 pull request mergés

**6. Comment pousser l’analyse plus loin \( comparer les sections de code \)  ?**

Nous avons trouvé un moyen de pousser notre analyse plus loin en inspectant le code des fichiers modifier. De ce manière, on peut être plus précis sur nos résultats. En plus de dire que c'est le code ajouté qui a provoqué l'erreur, nous serons capable de préciser si la personne a enlever ou ajouter du code et préciser la fonction/ligne qui provoque l'erreur modulo les erreurs d'implémentation.

## III. Expériences

Nous avons décidé de nous intéresser au merge qui sont des pulls resquest afin de restreindre la taille des données manipulé. Dans un premier temps nous avons extrait automatiquement 61 pulls requests contenant un total de 665 commis dont 36 commis sont en erreurs.

Nous avons ensuite développé un logiciel qui exécute nos règles sur ces pull requests. Voici le résultat de l’expérience 1:  


![r&#xE9;sultat de l&apos;exp&#xE9;rience](https://lh5.googleusercontent.com/n4hr-T78q49VnqskW-aOdefKocb-Mste4XO-iCe7U5O5AMoJTuEae7zK4i5pCgA_muFc3tTu-51yoavkQX1jzDp1UwXYmsVSmgW5K766OjhnBdgdkt-TLezUjhYnpuEBSS_FHpw)

* les tests n’ont pas été mis à jour : 2
* les tests ont été mal écrit : 4
* le code ajouté est défectueux  : 12
* le code ajouté marche mais produit des erreurs au sein du système : 24

![Graphe mod&#xE9;lisant le r&#xE9;sultat de l&apos;exp&#xE9;rience](https://lh4.googleusercontent.com/KNJlrsbmL2GiHfV52jzCWTAn5Boj3v1oOy7KtOzWpV3BtKSgxdLpXUFBoz4WQyc10hvA6DFLy2XZQXDklvmlkLa0kmjTeTZL4SUR2nvaSf-8qgAVlVmLgKOqbm_oxge_SbdhG50)

Après cette première expérience, on peut se rendre compte que ⅔ des merges qui se passe mal sont dus à l’impact du nouveau code dans le reste du système. Afin de pouvoir confirmer cette première expérience nous avons décidé de lancer nos clauses sur d'autres projets :  
****

**ReactiveX/RxJava :**

* [https://github.com/ReactiveX/RxJava](https://github.com/ReactiveX/RxJava)
* 3000+ pull request
* 0 failed merged pull request ****

**mockito/mockito:**

* [https://github.com/mockito/mockito](https://github.com/mockito/mockito)
* 700+ pull request
* build avec different verison de jdk \(8-11\), le build avec jdk11 fail très souvent
* eg. [https://github.com/mockito/mockito/pull/1592](https://github.com/mockito/mockito/pull/1592) ****

**apache/incubator-dubbo:**

* [https://github.com/apache/incubator-dubbo](https://github.com/apache/incubator-dubbo)
* 1300+ pull request
* build avec jdk 8 et 11
* eg. [https://github.com/apache/incubator-dubbo/pull/3240](https://github.com/apache/incubator-dubbo/pull/3240) ****

**apache/incubator-shardingsphere:**

* [https://github.com/apache/incubator-shardingsphere](https://github.com/apache/incubator-shardingsphere)
* ~700 pull request
* only jdk8
* need check ****

**apache/incubator-skywalking:**

* [https://github.com/apache/incubator-skywalking](https://github.com/apache/incubator-skywalking)
* 1200+ pull request
* single jdk
* need check ****

**apache/incubator-heron:**

* [https://github.com/apache/incubator-heron](https://github.com/apache/incubator-heron)
* 2200+ pull request
* jdk8
* need check ****

