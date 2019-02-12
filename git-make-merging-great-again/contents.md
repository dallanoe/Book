# Est-il possible de déterminer à l’avance qu’un merge risque de poser problème ?

## Make git merge great again

**/! utilisation du terme "fusion" ou "merge"**

### Auteurs

Nous sommes 4 étudiants en dernière année à Polytech' Nice-Sophia en informatique dans la spécialité "Architecture Logicielle":

* Guillaume ANDRE [guillaume.andre@etu.unice.fr](mailto:guillaume.andre@etu.unice.fr)
* Alexandre HILTCHER [alexandre.hiltcher@etu.unice.fr](mailto:alexandre.hiltcher@etu.unice.fr)
* David LANG [david.lang@etu.unice.fr](mailto:david.lang@etu.unice.fr)
* Jean-Adam PUSKARIC [jean-adam.puskaric@etu.unice.fr](mailto:jean-adam.puskaric@etu.unice.fr)

### Introduction

### Lexique

Dans la suite du document, nous allons utiliser différents termes techniques qui seront définis ci-dessous afin d'éviter toute confusion.

**Merge :** Dans le monde de la gestion de version \(avec Git par exemple\) un merge, ou fusion en français, est le fait de fusionner deux branches afin d'obtenir un nouvel historique commun.

```text
       A---B---C topic
      /         \
 D---E---F---G---H master
```

Comme dans l'exemple ci-dessus, lorsque les commits C de la branche`topic` et et G de la branche `master` sont merge on obtient un nouveau commit H contenant les modifications faites sur la branche `topic` et la branche `master`.

**Merge conflict :** Un merge conflict est défini comme un merge qui entraîne la fusion d'un même fichier, entraînant l'apparition de marqueurs de conflit dans le cas où le merge ne peut pas être réglé automatiquement par Git

**Qualité logicielle :** L'[IEEE](https://www.ieee.org/) définit la qualité logicielle en deux points : 1. Le degré avec lequel un système, composant ou processus répond au exigences techniques spécifiées. 2. Le degré avec lequel un système, composant ou processus répond aux besoins et/ou attentes des utilisateurs.

Dans la suite de ce document, lorsque nous parlerons de qualité logicielle cela fera référence au point numéro 1. En effet, nous nous baserons sur des métriques de qualité logicielles fournies par des outils d'analyse de code. Nous ne tiendrons pas compte ici la manière dont le système répond aux attentes des utilisateurs.

### I. Contexte de recherche

Git est un logiciel de gestion de version libre utilisé par la majorité des projets open source. Aujourd'hui, utiliser Git pour gérer nos projets semble être une évidence, et il nous paraît intéressant d’analyser et quantifier l’impact de cet outil sur le code produit et sa qualité. Plus particulièrement nous nous intéresserons aux _merges conflicts_, qui sont une fonctionnalité de Git pouvant causer des problèmes sur le code \(et parfois pour les relations humaines!\). En effet, un merge conflict revient à fusionner des modifications concurrentes sur un même fichier, qui sont parfois des effets de bords résultants de modifications sur d'autres éléments. De plus, on peut trouver sur internet et dans la littérature de nombreux articles sur les bonnes pratiques de Git et comment bien réaliser des merges. Ceci montre bien que le _merge_ est un problème récurrent pour les développeurs et utilisateurs de Git ou de système de contrôle de version. \[2\]

Dès lors il nous semble pertinent de nous demander quel est l'impact réel de ces _merge conflicts_ dans les zones du code concernées par cette fonctionnalité, plus particulièrement vis à vis d'identificateurs de qualité logicielle précis: nombre de lignes, nombre de bugs, complexité cyclomatique.

### II. Question générale

Nous cherchons donc à savoir si, pour un fichier d'un projet donné, il est possible d'établir une corrélation entre le nombre de _merge conflict_ et la qualité logicielle. Si celle corrélation existe, il pourrait alors théoriquement être possible de déterminer à l’avance qu’un merge risque de poser problème sur un fichier en mesurant au préalable sa qualité. Notre problématique générale consiste donc à déterminer si effectuer cette prédiction est possible. Si cette prédiction est possible, on pourrait alors envisager d'établir un processus ou une méthode de travail permettant de limiter les problèmes liés aux merges.

Pour répondre à cette question, nous avons choisi de répartir notre travail à travers plusieurs questions plus précises. Ces différentes questions abordent des axes différents de la relation entre qualité logicielle et les _merges conflicts_.

**Est-ce qu’un fichier de mauvaise qualité logicielle aura beaucoup de merge conflict dans son historique ?** Cette question porte sur l'impact de la qualité logicielle sur le nombre de merge conflicts. On souhaite déterminer si un fichier ayant une mauvaise qualité logicielle aura plus de merge conflicts dans son historique qu'un fichier de meilleure qualité.

**Est-ce que les merge conflicts dégradent la qualité logicielle d’un fichier ?** Dans cette question, nous abordons la question avec un axe différent, en effet, ici nous souhaitons savoir si à l'inverse les merges conflicts dans un fichier impactent la qualité logicielle.

Avec ces deux questions, on souhaite voir si la corrélation qu'on cherche à démontrer a plus ou moins d'impact dans un sens ou dans un autre.

### III. Collecte d'information

![M&#xE9;thodologie d&apos;extraction de la qualit&#xE9; logicielle](../.gitbook/assets/methodologie.svg)

#### Sélection des projets à analyser

Les projets Git que nous allons analyser vont être extraits depuis la plateforme _github_. Elle nous semble idéale pour notre analyse étant donné le grand nombre de projets en libre accès qu'elle contient et la mise à disposition d'une API gratuite \(bien que limitée\). Nous cherchons dans les dépôts publics fournis par l'API, ce sont donc des projets publics ce qui pourrait conduire à plus de merges conflicts étant donné le plus grand nombre de contributeurs et la réduction de contrôle.

Nous avons de plus choisi d'appliquer d'autres restrictions afin de composer notre échantillon de projets:

* Un certain nombre de commits et de merges minimums: cela permet d'exclure des projets ne possédant pas assez de merges dans leur historique pour être pertinents à analyser, étant donné que les merges conflicts sont long à déterminer, nous nous basons sur les commits et les merges pour nous donner un bon indicateur.
* Un langage de programmation commun, afin de pouvoir mesurer la qualité logicielle des  différents projets de manière homogène. Nous avons choisi Java pour sa familiarité et sa compatibilité avec l'outil de mesure de qualité logicielle que nous avons choisi.

#### Extraction des merge conflicts

Une fois que l'on dispose d'un ensemble de projets Git, on peut facilement repérer quels commit sont des _merge_ à l'aide de l'API github ou des commandes Git standard: il s'agit de commits avec 2 parents _left_ et _right_. Pour identifier les _merge conflicts_, il suffit de rejouer le _merge_ en question en 2 commandes Git:

* `git checkout left`
* `git merge right`

On obtient alors l'ensemble des fichiers qui sont entrés en conflit, et si ces conflits ont été résolus automatiquement, nous permettant ainsi de mesurer le nombre de merges qu'a subi un fichier particulier sur l'ensemble de l'historique. Nous considérons les deux comme des _merge conflict_ pour le contexte de notre étude.

#### Mesure de la qualité logicielle

Afin de pouvoir mener à bien notre analyse de qualité logicielle, l'outil que nous utilisons doit satisfaire plusieurs critères.

Nous allons devoir analyser un grand nombre de dépôts, et il doit donc être automatisable. Il doit également être capable d'effectuer des mesures à plusieurs échelles: celle du projet et du fichier, afin de pouvoir analyser séparément les éléments concernés par un conflit de merge et afin de pouvoir rapporter la qualité logicielle d'un fichier à la qualité logicielle générale du projet le contenant. Ces mesures doivent être récupérables de manière rapide afin de pouvoir analyser un grand nombre de fichiers.

Enfin, il est important que l'outil ait d'ores et déjà fait ses preuves afin de s'assurer de la validité des métriques mesurées.

Pour ces raisons, nous avons choisi d'utiliser l'outil _SonarQube_. Il dispose de plusieurs avantages:

* Il est utilisé dans un cadre professionnel, avec l'usage de _quality gates_;
* Il permet d'obtenir des métriques de qualité à l'échelle d'un seul fichier;
* Il est compatible avec de nombreux langages de programmation, permettant la reproduction de nos expérimentations dans d'autres langages;
* Il est facilement scriptable à l'aide de simple requêtes HTTP sur un serveur local déployé après l'analyse des projets

#### Métriques de qualité logicielles choisies

A l'aide de l'outil _SonarQube_, nous avons accès aux métriques suivantes:

* Nombre de bug et code smells 
* Complexité cyclomatique totale, par classe et par fonction
* Nombre de lignes et proportion de code dupliqué

Le nombre de bugs et code smells, ainsi que les différentes métriques de complexité, vont nous permettre de mesurer objectivement la qualité d'un fichier ou d'un projet. Ces métriques ont également l'avantage être limtées à un langage de programmation particulier, ouvrant la possibilité pour la reproduction de nos expérimentations sur d'autres langages.

Afin de modérer l'impact que peut avoir la taille d'un fichier sur certaines métriques, nous allons les pondérer selon le nombre de lignes du fichier. En effet, il nous semble normal qu'un fichier de plusieurs centaines de lignes possède par exemple un nombre de bugs plus élevé qu'un fichier ne mesurant que 10 lignes.

## IV. Hypothèses et expérimentations

Dans cette partie, nous allons décrire les différentes expérimentations que nous avons mis en place pour apporter des éléments de réponse aux sous questions que nous avons posé précédemment.

#### 1. Est-ce qu’un fichier de mauvaise qualité logicielle aura beaucoup de merge conflict dans son historique ?

Nous avons l'intuition qu'un grand nombre de conflits sur un fichier va dégrader sa qualité, étant donné que cela implique à priori un grand nombre de modifications par des utilisateurs différents ne travaillant pas de manière totalement homogène. On s'attend donc à voir nos métriques mesurant le nombre de bugs et la complexité augmenter de manière proportionnelle aux nombre de conflits qu'a subi un fichier dans son historique.

Afin de tenter de valider cette hypothèse, nous avons extrait et analysé N dépôts github, analysé leur qualité logicielle en leur état actuel, puis extrait l'ensemble des conflits de merges à l'aide de la méthodologie décrite dans la partie précédente. Les dépôts ont été choisis aléatoirement parmi l'ensemble des dépôts Java disponibles sur github et possèdent tous un minimum de Z merges.

Nous avons ainsi pu extraire X merges, et analyser Y conflits de merge.

#### 2. Est-ce que les merge conflicts dégradent la qualité logicielle d’un fichier ?

En suivant un raisonnement similaire à l'hypothèse précédente, un conflit de merge implique souvent des modifications par un développeur sur un code qu'il n'a pas écrit lui même afin de résoudre le conflit. Pour nous, notre intuition est que cette action devrait mener à une baisse de la qualité du ficher.

Pour apporter des éléments de réponse à cette question, nous avons analysé N conflits de merge à travers X dépôts. Pour chacun de ces conflits, nous avons mesuré nos métriques de qualité logicielle sur les fichiers concernés avant et après l’occurrence du conflit.

## V. Analyse des résultats et conclusion

**Analyse des résultats & construction d’une conclusion : Une fois votre expérience terminée, vous récupérez vos mesures et vous les analysez pour voir si votre hypothèse tient la route.**   ****

## VI. Outils

Dans cette partie, nous allons brièvement décrire l'ensemble des scripts que nous avons développé afin de pouvoir conduire nos expérimentations. Des instructions plus détaillées sur leur usage sont disponible dans le dépôt github les contenant \[5\]: 

* **repository-finder** utilise l'api github afin de récupérer un échantillon aléatoire de dépôts selon les critères passés en paramètre;
* **merge-extractor** permet de cloner et récupérer l'ensemble des merge des dépôts;
* **merge-conflict-extractor** permet de rejouer les merges et de déterminer quels conflits ont eu lieu sur quels fichiers;
* **quality-analyser** permet l'analyse des dépôts et la collecte de métriques sur les fichiers concernés par les merge;
* **graph-generator** produit un ensemble de graphe montrant pour chaque dépôt la variation de la valeur d'une métrique selon le nombre de conflits de merge d'un fichier du dépôt

## VII. Références

\[1\] Présentation de l'IEE sur la qualité logicielle :

* [http://www.ieee.org.ar/downloads/Barbacci-05-notas1.pdf](http://www.ieee.org.ar/downloads/Barbacci-05-notas1.pdf)

\[2\] Articles en liens avec la qualité logicielle et l'utilisation de banche/merges :

* [https://hal.inria.fr/hal-00957168/file/ease.pdf](https://hal.inria.fr/hal-00957168/file/ease.pdf)
* [http://thomas-zimmermann.com/publications/files/shihab-esem-2012.pdf](http://thomas-zimmermann.com/publications/files/shihab-esem-2012.pdf)

\[3\] Outil SonarQube:

* [https://www.sonarqube.org/](https://www.sonarqube.org/)

\[4\] Best practice git merge :

* [https://www.atlassian.com/git/tutorials/advanced-overview](https://www.atlassian.com/git/tutorials/advanced-overview)

\[5\] Dépôt contenant les scripts pour reproduire l'expérimentation:

* [https://github.com/JAMamene/Rimel](https://github.com/JAMamene/Rimel)

\*\*\*\*

![](../.gitbook/assets/logo_uns%20%288%29.png) UCA : University Côte d'Azur \(french Riviera University\)





