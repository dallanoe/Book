# Est-il possible de déterminer à l’avance qu’un merge risque de poser problème ?

## 

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

**Merge conflict :** Un merge conflict est défini comme un merge qui entraine la fusion d'un même fichier, entrainant l'apparition de marqueurs de conflit dans le cas où le merge ne peut pas être réglé automatiquement par Git

**Qualité logicielle :** L'[IEEE](https://www.ieee.org/) définie la qualité logicielle en deux points : 1. Le degré avec lequel un système, composant ou processus répond au exigences techniques spécifiées. 2. Le degré avec lequel un système, composant ou processus répond aux besoins et/ou attentes des utilisateurs.

Dans la suite de ce document, lorsque nous parlerons de qualité logicielle cela fera référence au point numéro 1. En effet, nous nous baserons sur des métriques de qualité logicielles fournies par des outils d'analyse de code. Nous ne tiendrons pas compte ici la manière dont le système répond aux attentes des utilisteurs.

### I. Contexte de recherche

Git est un logiciel de gestion de version libre utilisé par la majorité des projets open source. Aujourd'hui, utiliser Git pour gérer nos projets semble être une évidence, et il nous paraît intéressant d’analyser et quantifier l’impact de cet outil sur le code produit et sa qualité. Plus particulièrement nous nous intéresserons aux _merges conflicts_, qui sont pour nous la fonctionnalité basique de Git pouvant être la plus disruptive pour le code \(et parfois pour les relations humaines\). En effet, on peut trouver sur internet et dans la littérature de nombreux articles sur les bonnes pratiques de Git et comment bien réaliser des merges. Ceci montre bien que le _merge_ est un problème récurrent pour les développeurs et utilisateurs de Git ou de système de contrôl de version.

Dès lors il nous semble pertinent de nous demander quel est l'impact réel de ces _merge conflicts_ dans les zones du code concernées par cette fonctionnalité, plus particulièrement vis à vis d'identificateurs de qualité logicielle précis: nombre de lignes, nombre de bugs, complexité cyclomatique.

### II. Question générale

Nous cherchons donc à savoir si, pour un fichier d'un projet donné, il est possible d'établir une corrélation entre le nombre de _merge conflict_ et la qualité logicielle. Si celle corrélation existe, il pourrait alors théoriquement être possible de déterminer à l’avance qu’un merge risque de poser problème sur un fichier en mesurant au préalable sa qualité. Notre problématique générale consiste donc à déterminer si effectuer cette prédiction est possible. Si cette prédiction est possible, on pourrait alors envisager d'établir un processus ou une méthode de travail permettant de limiter les problèmes liés aux merges.

Pour répondre à cette question, nous avons choisi de répartir notre travail à travers plusieurs questions plus précises. Ces différentes questions abordent des axes différents de la relation entre qualité logicielle et les _merges conflicts_.

**Est-ce qu’un fichier de mauvaise qualité logicielle aura beaucoup de merge conflict dans son historique ?** Cette question porte sur l'impact de la qualité logicielle sur le nombre de merge conflicts. On souhaite déterminer si un fichier ayant une mauvaise qualité logicielle aura plus de merge conflicts dans son historique qu'un fichier de meilleure qualité.

**Est-ce que les merge conflicts dégradent la qualité logicielle d’un fichier ?** Dans cette question, nous abordons la question avec un axe différent, en effet, ici nous souhaitons savoir si à l'inverse les merges conflicts dans un fichier impactent la qualité logicielle.

Avec ces deux questions, on souhaite voir si la corrélation qu'on cherche à démontrer a plus ou moins d'impact dans un sens ou dans un autre.

**Les zones de code où les merge conflicts apparaissent le plus souvent sont-elles de bonne qualité logicielle ?** Cette dernière question nous permet d'approfondir la première en essayant de se concentrer sur des zones précises de fichiers et non plus sur un fichier tout en entier. En effet, il est possible que dans un fichier certaines zones soient plus souvent merge que d'autres. De ce fait il est possible que l'impact de ces derniers soient plus ou moins visible dans ces différentes zones. On peut donc imaginer qu'au sein d'un même fichier la qualité logicielle varie s'il y a eu plus ou moins de merge sur une zone de code.

### III. Collecte d'information

![M&#xE9;thodologie d&apos;extraction de la qualit&#xE9; logicielle](../.gitbook/assets/methodologie.svg)

#### Sélection des projets à analyser

Les projets git que nous allons analyser vont être extraits depuis la plateforme _github_. Elle nous semble idéale pour notre analyse étant donné le grand nombre de projets en libre accès qu'elle contient et la mise à disposition d'une API gratuite.

Nous avons de plus choisi d'appliquer d'autres restrictions afin de composer notre échantillon de projets:

* Un certain nombre de commits minimums: cela permet d'exclure des projets ne possédant pas assez de merges dans leur historique pour être pertinents à analyser
* Un langage de programmation commun, afin de pouvoir mesurer la qualité logicielle des  différents projets de manière homogène. Nous avons choisi Java pour sa familiarité et sa compatibilité avec l'outil de mesure de qualité logicielle que nous avons choisi.

#### Extraction des merge conflicts

Une fois que l'on dispose d'un ensemble de projets git, on peut facilement repérer quels commit sont des _merge_ à l'aide de l'API github ou des commandes git standard: il s'agit de commits avec 2 parents _left_ et _right_. Pour identifier les _merge conflicts_, il suffit de rejouer le _merge_ en question en 2 commandes git:

* `git checkout left`
* `git merge right`

On obtient alors l'ensemble des fichiers qui sont entrés en conflit, et si ces conflits ont été résolus automatiquement, nous permettant ainsi de mesurer le nombre de merges qu'a subi un fichier particulier sur l'ensemble de l'historique. Nous considérons les deux comme des _merge conflict_ pour le contexte de notre étude.

#### Mesure de la qualité logicielle

Pour obtenir un ensemble de métriques nous permettant de mesurer la qualité logicielle d'un fichier, nous avons choisi d'utiliser l'outil _SonarQube_. Il dispose de plusieurs avantages:

* Il est utilisé dans un cadre professionnel, avec l'usage de _quality gates_;
* Il permet d'obtenir des métriques de qualité à l'échelle d'un seul fichier;
* Il est compatible avec de nombreux langages de programmation, permettant la reproduction de nos expérimentations dans d'autres langages;
* Il est facilement scriptable à l'aide de simple requêtes HTTP sur un serveur local déployé après l'analyse des projets.

#### Métriques de qualité logicielles choisies

A l'aide de l'outil _SonarQube_, nous collectons les métriques suivantes:

* Nombre de bug et code smells 
* Complexité cyclomatique totale, par classe et par fonction
* Nombre de lignes et proportion de code dupliqué

Afin de modérer l'impact que peut avoir la taille d'un fichier sur certaines métriques, nous allons les pondérer selon le nombre de lignes du fichier. En effet, il nous semble normal qu'un fichier de plusieurs centaines de lignes possède par exemple un nombre de bugs plus élevé qu'un fichier ne mesurant que 10 lignes.

### IV. Hypothèses et expérimentation

**Il s'agit ici d'énoncer sous forme d' hypothèses ce que vous allez chercher à démontrer. Vous devez définir vos hypothèses de façon à pouvoir les mesurer facilement. Bien sûr, votre hypothèse devrait être construite de manière à vous aider à répondre à votre question initiale.Explicitez ces différents points.** **Test de l’hypothèse par l’expérimentation.** 1. **Vos tests d’expérimentations permettent de vérifier si vos hypothèses sont vraies ou fausses.** 2. **Il est possible que vous deviez répéter vos expérimentations pour vous assurer que les premiers résultats ne sont pas seulement un accident.** **Explicitez bien les outils utilisés et comment.** **Justifiez vos choix**

### V. Analyse des résultats et conclusion

**Analyse des résultats & construction d’une conclusion : Une fois votre expérience terminée, vous récupérez vos mesures et vous les analysez pour voir si votre hypothèse tient la route.**   **UCA : University Côte d'Azur \(french Riviera University\)** **VI. Tools \(facultatif\)**

**Précisez votre utilisation des outils ou les développements \(e.g. scripts\) réalisés pour atteindre vos objectifs. Ce chapitre doit viser à \(1\) pouvoir reproduire vos expériementations, \(2\) partager/expliquer à d'autres l'usage des outils.**

\*\*\*\*

![](../.gitbook/assets/logo_uns%20%288%29.png) UCA : University Côte d'Azur \(french Riviera University\)

### VI. References

Présentation de l'IEE sur la qualité logicielle :

* [http://www.ieee.org.ar/downloads/Barbacci-05-notas1.pdf](http://www.ieee.org.ar/downloads/Barbacci-05-notas1.pdf)

Articles en liens avec la quailité logicielle et l'utilisation de banche/merges :

* [https://hal.inria.fr/hal-00957168/file/ease.pdf](https://hal.inria.fr/hal-00957168/file/ease.pdf)
* [http://thomas-zimmermann.com/publications/files/shihab-esem-2012.pdf](http://thomas-zimmermann.com/publications/files/shihab-esem-2012.pdf)

Outil SonarQube:

* [https://www.sonarqube.org/](https://www.sonarqube.org/)



