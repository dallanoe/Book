# Projet Java Properties

**Date de rendu finale : March 2018 au plus tard**

Remarques :

Les titres peuvent changer pour etre en adéquation avec votre étude.

De même il est possible de modifier la structure, celle qui est proposée ici est là pour vous aider.

Utilisez des références pour justifier votre argumentaire, vos choix etc.

## Authors

We are four students in last year of Polytech' Nice-Sophia specialized in Software Architecture :

* .... &lt;xxx@gmail.com&gt;

## I. Research context /Project

La création de la classe Properties remonte à Java 1.0 bien avant que des concepts objet plus ou moins équivalent soient introduits comme les maps. Les properties jouent un rôle important dans un grand nombre de projets Java. Elles sont généralement utilisées pour sauvegarder les données de configuration des projets Java ou les paramètres. Le moyen le plus répandu pour les stocker est de les inscrire dans des fichiers .properties qui seront par la suite lus par le programme, cependant elles peuvent aussi être créé dans le code à l'aide de la méthode setProperty\(\).

Un autre avantage des properties est que lors d'un changement dans un des fichiers il n'est pas nécessaire de recompiler le code java pour prendre en compte cette modification. Un des objectifs des properties est de permettre une modification fréquente si besoin.

Même si cette "technologie" date de 1996 elle reste indispensable et il serait très difficile de la remplacer non seulement par sa longévité et l'habitude des développeurs à l'utiliser, mais surtout, car sa disparition entraînerait des importants problèmes de compatibilité.

Cependant même si les properties sont omniprésentes dans les projets Java on peut se demander où et comment les développeurs les utilisent. Ce sont ces aspects-là que nous souhaitons approfondir.

## II. Observations/General question

### A Question

Nous avons constaté que la plupart des projets Java utilisent à un moment donné des properties. Nous nous sommes donc demandé jusqu'où les développeurs poussent l’utilisation de cette technologie.

En effet, nous trouvons intéressant de comprendre et de pouvoir quantifier l’utilisation que font les développeurs de cette brique élémentaire de java.

Nous avons découpé ce thème en trois questions : 

* Où les développeurs utilisent les properties ? Uniquement dans le code ou bien dans l’ensemble du projet ?  
* Comment les properties sont utilisés ? Directement grâce aux méthodes natives de java ou sont-elles manipulées par le biais de librairie ou de wrappers ?  
* Est ce que la majorité des projets utilisent les properties Java dans un même but ?

### B KPI

Pour répondre à ces trois questions, nous avons défini les KPI suivants. En ce qui concerne la question d'où sont utilisé les properties, nous allons, afin d’y répondre, localiser l’ensemble des appels aux méthodes permettant d’accéder ou de modifier les properties. Que ce soit grâce aux méthodes natives de java ou bien à l’aide d’une librairie / wrapper. Nous avons défini que les properties sont utilisés dans une des parties d’un projet \(par exemple la partie test\) si le rapport entre le nombre d’appels aux méthodes trouvées dans la partie courante sur le nombre total d’utilisations des properties doit être supérieur à 0,05 \(5%\) . Nous avons défini cette limite a 5% pour éviter de nous retrouver dans le cas extrême ou un projet qui appellerait 40 000 fois les properties dans le code, mais qui appellerait seulement 4 fois les properties dans ses tests ne soit considéré comme un projet qui utilise les properties dans ses tests. Cependant, nous avons défini ce seuil assez bas, car nous estimons qu’en dessous de ce seuil, il n’y a pas assez d’appels pour considérer la partie comme utilisant réellement les properties. Une fois que nous aurons listé la position de ces appels grâce au nom des classes / package qui les contiennent, nous serons en mesure de répondre à cette première question.

Afin de pouvoir différencier les projets qui utilises les méthodes natives de ceux qui utilise des librairies / wrapper, nous allons comparer le nombre de properties créées dans les fichiers .property avec le nombre d’appels aux accesseurs de ces properties. Nous allons considérer qu’un projet utilise des librairies / wrapper à partir du moment ou le rapport nombre d’appels au getter trouvé sur le nombre de properties déclaré dans le fichier properties est inférieur à 0,10 \(10%\). Sinon, nous considérons que le projet utilise les méthodes natives de java. Nous avons choisi 10% comme seuil par une première observation rapide de notre dataset ou les projets qui utilisaient des librairies ou wrappeur s'approchait de cette valeur sans jamais la dépasser.

Pour répondre à notre dernière question, nous allons lister les noms des properties utilisés dans l’ensemble des projets. Nous allons par la suite vérifier naïvement si certains noms se retrouvent dans différents projets.

Nous avons conscience que cette méthode de validation reste limitée puisqu'il est possible que deux projets utilisent une properties pour les mêmes raisons, mais nommée différemment. Cependant, cette métrique nous donnera une première réponse partielle.





## III. information gathering

### A. Dataset

Nous avons fait le choix de l'imiter le scope des projets que nous allons analyser afin de nous créer un point d'entrée et de rendre le projet réalisable en deux mois.

Nous nous sommes dans un premier temps restreints au projet GitHub car c’est une des sources de données les plus rapidement utilisables et les plus populaires. De plus, nous avons préféré nous concentrer sur les trente premiers projets Java qui avaient le plus d’étoiles. Nous avons fait ce choix dans l’optique d’obtenir un dataset contenant seulement des “gros” projets Java qui ont du vécu et qui donc, pour nous, sont bien plus représentatif dans l’utilisation qu’ils vont faire des Properties que si nous avions sélectionné des projets de manière aléatoire par l’API GitHub. Au vu de l’ancienneté des Properties \(Java 1.0\), nous n’avons pas exclu les projets qui ne sont plus maintenus, car ils restent pertinents dans notre contexte. Enfin, nous avons réduit une seconde fois notre dataset en nous focalisant uniquement sur des projets Maven puisqu’ils offrent une structure définie et constante, ce qui nous permet de plus facilement parcourir et localiser les appels au properties.



### B. Protocole

Notre protocole est découpé en trois parties distinctes.

#### Récupération et filtrage des répositories

* Dans un premier temps, on collecte l’ensemble des repository \(30 premiers projets java qui ont le plus d’étoiles sur GitHub\).  
* Afin d’épurer le dataset, nous allons lancer plusieurs scripts bash qui ont pour but de nous indiquer les projets qui ne sont pas pertinents pour notre étude. 
  * Un premier script bash nous indique quels projets ne sont pas des projets Maven.
  * Un second script qui permet de vérifier la présence de properties java pour éliminer les projets qui n’en contiennent pas.

#### Analyse et cartographie des projets

* Dans un premier temps, nous parcourons l’ensemble des fichiers properties afin de lister les properties et récupérer leurs noms. 
* Ensuite, grâce a Spoon, nous allons effectuer un premier passage pour répertorier la localisation des différents appels aux méthodes Java “System.setProperties” et System.getProperties”. Cette étape est importante, car elle nous permet de différencier les deux types de projets que nous allons traiter. Ceux qui utilise directement les méthodes Java natives \(“System.setProperties” et System.getProperties”\) des projets qui utilise une librairie ou un wrapper pour interagir avec les properties.   Cette différenciation est cruciale, car dans le premier cas, nous ne devons effectuer qu’un seul passage avec spoon pour localiser les appels aux méthodes natives. Alors que dans le second cas, nous ne devons pas cette fois-ci localiser les méthodes natives Java, mais identifier quelles méthodes du wrapper / librairie encapsule ces méthodes. Puis, effectuer une seconde passe avec spoon pour localiser l’utilisation de ces méthodes encapsulantes. 
* Nous exportons ces résultats au format CSV pour qu’ils puissent être utilisés par notre générateur de graphique.

#### Génération des graphiques

Nous passons nos CSV précédemment générés à un script R qui va construire les graphiques pour chaque projet analysé, mais également, des graphiques pour l’ensemble des projets.

### C. **Limites de notre dataset**

Nous avions dans la partie filtrage des repositories un script bash qui nous permettait de vérifier la présence de fichiers liés au déploiement \(DockerFile, JenkinsFile, docker-compose.yml…\) afin de vérifier s’il était possible de cartographier l’utilisation des properties dans le déploiement. Nous avons constaté que sur les trente projets traités, seulement quatre comportaient ce type de fichier. Ces projets n’avaient pas de cohérence au niveau de la rédaction de ces fichiers ce qui rendait l’analyse automatique impossible. De plus, les fichiers étant très complexes, même une analyse manuelle aurait été difficile et chronophage. Pour toutes ces raisons, nous avons décidé de ne plus prendre en compte la partie déploiement dans notre étude.

## IV. Hypothesis & Experiences

Intuitivement, d’après notre expérience et une analyse rapide des projets de notre dataset, nous avons formulé les hypothèses suivantes.

#### Les properties Java sont principalement utilisées grâce aux méthodes Java natives

Nous pense qu’au vu de la simplicité de l’utilisation des properties java \( appel à un simple getter ou setter\), nous pouvons supposer qu’il n’est pas nécessaire de mettre en place une encapsulation pour utiliser ces méthodes.

Pour vérifier cette hypothèse, nous allons nous appuyer sur le rapport entre le nombre de properties set et le nombre d’utilisations de “System.getProperty”

#### Seules quelques properties sont présentes dans les tests 

Nous avons l’intuition que seul un sous-ensemble des properties sont utilisées dans les tests. Notamment les properties de configuration par exemple celles qui indiquent quel type base de données utiliser ou encore son adresse.

Pour valider cette hypothèse, nous allons utiliser notre cartographie des projets afin de vérifier qu’effectivement, le nombre d’appels aux properties dans les tests est supérieur à 5% du nombre d’appels total, mais est bien inférieur au nombre de properties utiliser dans le code.

#### Une partie des properties sont génériques, un sous-ensemble des properties java sont donc utilisé de la même manière dans tous les projets

Nous avons constaté en parcourant les ReadMe des différents projets qu’en plus des properties spécifiques au métier de chaque projet, une partie était identiques dans plusieurs projets. Notamment les properties qui permettent de configurer les éléments communs au projet tels que les bases de données, les loggers ou la localisation des fichiers en entrée et en sortie.

Pour répondre à cette question , nous allons lister le nom des properties utilisées dans chaque projet. Nous allons ensuite vérifier que les mêmes noms apparaissent dans plusieurs projets.

## V. Result Analysis and Conclusion

1. Analyse des résultats & construction d’une conclusion : Une fois votre expérience terminée, vous récupérez vos mesures et vous les analysez pour voir si votre hypothèse tient la route. 

![](../.gitbook/assets/logo_uns.png) UCA : University Côte d'Azur \(french Riviera University\)

## VI. Tools \(facultatif\)

Précisez votre utilisation des outils ou les développements \(e.g. scripts\) réalisés pour atteindre vos objectifs. Ce chapitre doit viser à \(1\) pouvoir reproduire vos expériementations, \(2\) partager/expliquer à d'autres l'usage des outils.

## VI. References

1.

1. 
