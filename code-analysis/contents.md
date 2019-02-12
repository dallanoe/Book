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



### B. Protocole



### C. **Limites de notre dataset**

## IV. Hypothesis & Experiences

1. Il s'agit ici d'énoncer sous forme d' hypothèses ce que vous allez chercher à démontrer. Vous devez définir vos hypothèses de façon à pouvoir les _mesurer facilement._ Bien sûr, votre hypothèse devrait être construite de manière à v_ous aider à répondre à votre question initiale_.Explicitez ces différents points.
2. Test de l’hypothèse par l’expérimentation. 1. Vos tests d’expérimentations permettent de vérifier si vos hypothèses sont vraies ou fausses. 2. Il est possible que vous deviez répéter vos expérimentations pour vous assurer que les premiers résultats ne sont pas seulement un accident.
3. Explicitez bien les outils utilisés et comment.
4. Justifiez vos choix

## V. Result Analysis and Conclusion

1. Analyse des résultats & construction d’une conclusion : Une fois votre expérience terminée, vous récupérez vos mesures et vous les analysez pour voir si votre hypothèse tient la route. 

![](../.gitbook/assets/logo_uns.png) UCA : University Côte d'Azur \(french Riviera University\)

## VI. Tools \(facultatif\)

Précisez votre utilisation des outils ou les développements \(e.g. scripts\) réalisés pour atteindre vos objectifs. Ce chapitre doit viser à \(1\) pouvoir reproduire vos expériementations, \(2\) partager/expliquer à d'autres l'usage des outils.

## VI. References

1.

1. 
