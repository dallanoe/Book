# Les feature toggles créent-ils de la dette technique ?

**Date de rendu finale : March 2018 au plus tard**

Remarques :

Les titres peuvent changer pour etre en adéquation avec votre étude.

De même il est possible de modifier la structure, celle qui est proposée ici est là pour vous aider.

Utilisez des références pour justifier votre argumentaire, vos choix etc.

## Authors

We are four students in last year of Polytech' Nice-Sophia specialized in Software Architecture :

* Couvreur Alexis
* Matteo Lucas
* Junac Jérémy
* Melkonian François

## I. Research context /Project

> _"Feature Toggles \(often also refered to as Feature Flags\) are a powerful technique, allowing teams to modify system behavior without changing code."  
> --_ Pete Hodgson, sur le site[ martinfowler.com](https://martinfowler.com/)

Comme expliqué par Pete Hodgson, le _feature toggling_ permet de changer le comportement d'une application sans changer son code source, et donc sans la recompiler.

Ce principe est très largement utilisé pour tout type d'application. Il peut être utilisé sur les logiciels pour que l'utilisateur puisse le régler à sa guise, comme par exemple un navigateur web, mais aussi dans les applications de type _Software as a Service_, notamment lors de l'ajout de nouvelle fonctionnalité, comme c'est le cas pour Gmail par exemple.

La quasi totalité des projets utlise un principe de _feature toggling_, la plupart du temps sans même le savoir, tout simplement en utilisant un bloc conditionnel. Il existe cependant des _frameworks_, qui permettent d'ajouter une plus-value sur ce système conditionnel. Ils fournissent par exemple une API ou interface graphique pour la modification des valeurs.

De plus, découle du _feature toggling_ d'autre technique, utiliser pour rendre disponible petit à petit les nouvelles fonctionnalités aux utilisateurs. On peut par exemple citer le _dark launch_.



## II. Observations/General question

1. Commencez par formuler une question sur quelque chose que vous observez ou constatez ou encore une idée émergente. Attention pour répondre à cette question vous devrez être capable de quantifier vos réponses.
2. Préciser bien pourquoi cette question est intéressante de votre point de vue et éventuellement en quoi la question est plus générale que le contexte de votre projet \(ex: Choisir une libraire de code est un problème récurrent qui se pose très différemment cependant en fonction des objectifs\)

Dans ce contexte, nous pouvons demander ce qu'il advient du code necessaire au _feature toggle._ En effet, qu'il soit réalisé à l'aide d'un if ou par le biais d'un framework spécialisé, il est tout de même d'introduire du nouveau code pour le _feature flag_. Ce code, qui n'est pas lié au métier de l'application, devra être maintenu en même temps que le reste de l'application.

L'utilisation de ce genre de pratique a donc un impact sur la base de code, ce qui peut soulever la question de la rentabilité de ce genre de pratique. En d'autres termes, est-ce que l'utilisation d'un _feature toggle_ a un impact sur la qualité de notre code, et peut-on la quantifier ? Nous sommes donc arrivé à la problématique suivante:

**Question générale : Les features toggles créent-ils de la dette technique ?**

Ainsi, l'objectif pour nous sera de chercher une corrélation en l'évolution de la technique, et plus spécifiquement son augmentation, et l'ajout de _feature toggle,_ s'il en existe une_._

Afin de faciliter notre étude, nous avons restreint notre analyse au projet utilisant effectivement un framework de _feature toggling_ \(sachant que ceux-ci peuvent être "fait maison"\) et de laisser de côté les simples if. En effet, il serait beaucoup trop compliqué pour nous dans un grand nombre de projet de disinguer les if lié aux métiers de l'application et les if liés à un _feature flag_.

## III. Information gathering

Préciser vos zones de recherches en fonction de votre projet,

1. les articles ou documents utiles à votre projet
2. les outils

Afin de mener notre étude à bien, nous avons entamés la recherche d'un jeu de données. Pour prouver notre point, nous devions avoir des projets utilisant du _feature toggling_ de manière régulière, mais aussi avec une base de code conséquente, nécessaire pour mesurer l'évolution de la dette technique. Pour la base de projet, nous avons utilisé la plateforme [GitHub](https://github.com/), une source reconnue inépuisable de projet opensource.

Nous allons voir dans les paragraphes suivants que la recherche de ce jeu de données a été bien plus compliqué que nous l'anticipions, et a connu de nombreuses évolutions au cours du temps.

Considérant ces points, nous avons tout d'abord choisi le langage sur lequel nous voulions travailler, ce qui est aussi lié au framework de _feature toggle_ disponible dans le dit langage. Deux couples langage/framework nous a alors paru assez populaire pour garantir une bonne base de projet dans notre jeu de données: le framework "[Togglz](https://www.togglz.org/)" dans le langage Java, et le framework "[LaunchDarkly](https://launchdarkly.com/)" en JavaScript.

Il aurait été trop complexe d'étudier les deux frameworks et les deux langages en même temps, il a donc fallu trancher entre les deux couples. Après étude des projets utilisant les deux frameworks via l'API de dépendance GitHub, la base de projet utilisant Togglz nous paraissait plus intéressante à étudié que LaunchDarkly. En effet, les projets utilisant ce framework étaient globalement plus gros, _ie._ avaient plus de commits, plus de contributeurs et était plus "sérieux". De plus, Java étant plus structuré et plus restricitf, ce qui facilite l'analyse de la dette technique.

Sur la centaine de projet utilisant Togglz, nous avons ensuite filtré les projets qui nous semblait les plus intéressant pour notre étude. Nous sommes arrivé au jeu de données suivant:

* [Estatio](https://github.com/estatio/estatio) \(4,300 commits, 9 contributeurs, 170 stars\)
* [ORCID-Source](https://github.com/ORCID/ORCID-Source) \(20,800 commits, 29 contributeurs, 158 stars\)
* [lightblue-migrator](https://github.com/lightblue-platform/lightblue-migrator) \(1,100 commits, 11 contributeurs, 3 stars\)
* [isis-app-todoapp](https://github.com/isisaddons/isis-app-todoapp) \(155 commits, 5 contributeurs, 37 stars\)

Ce jeu de données rassemble des assez gros projets comme des projets plus petit, mais tous utilisant de manière assidu le _feature toggle_. Nous avons donc établi le protocole suivant pour analyser notre jeu de données, pour chaque commit: identifier sa dette technique et identifier s'il introduit un _feature toggle_.

Ce protocole nous permettrait donc d’identifier la dette introduite par un feature toggle, et de corréler son évolution. A ce point du projet, la "dette technique" est une métrique "magique", _ie._ on ne sait pas comment et quoi calculer mais on considère qu'on sait le faire. Cette question sera résolue dans la partie 4.

Cependant, il y avait un problème dans notre raisonement. Après discussion avec [Xavier Blanc](https://fr.linkedin.com/in/xavier-blanc-3b9785a), enseignant-chercheur à l'Université de Bordeaux et co-fondateur de ProMyze, notre jeu de données manqutait de "projets témoins". Ces projets aurait le même métier que les projets que nous analysions, et premettrait d'appuyer nos observation. En effet, une augmentation de la dette peut ne pas être forcément lié au _feature toggle_, mais tout simplement au métier de l'application.   
Ces projets témoins \(avec le même métier donc\) aurait donc la même évolution de dette technique.

Néanmoins, il aurait été beaucoup trop compliqué et fasitdieux pour nous de trouvé pour chaque projet selectionné un projet témoin de la même envergure avec le même métier. S'en sont suivies d'autres discussion avec Xavier Blanc et notre professeur encadrant Philippe Collet. 

A ce point, nous avons décidé de radicalement changer notre jeu de données. Si nous nous concentions sur un unique projet, nous aurions toutes les données dont nous avions besoin, et le témoin serait le projet lui-même, pour peut qu'il soit assez gros.



## IV. Hypothesis & Experiences

1. Il s'agit ici d'énoncer sous forme d' hypothèses ce que vous allez chercher à démontrer. Vous devez définir vos hypothèses de façon à pouvoir les _mesurer facilement._ Bien sûr, votre hypothèse devrait être construite de manière à v_ous aider à répondre à votre question initiale_.Explicitez ces différents points.
2. Test de l’hypothèse par l’expérimentation. 1. Vos tests d’expérimentations permettent de vérifier si vos hypothèses sont vraies ou fausses. 2. Il est possible que vous deviez répéter vos expérimentations pour vous assurer que les premiers résultats ne sont pas seulement un accident.
3. Explicitez bien les outils utilisés et comment.
4. Justifiez vos choix

## V. Result Analysis and Conclusion

1. Analyse des résultats & construction d’une conclusion : Une fois votre expérience terminée, vous récupérez vos mesures et vous les analysez pour voir si votre hypothèse tient la route. 

![](../.gitbook/assets/logo_uns%20%287%29.png) UCA : University Côte d'Azur \(french Riviera University\)

## VI. Tools \(facultatif\)

Précisez votre utilisation des outils ou les développements \(e.g. scripts\) réalisés pour atteindre vos objectifs. Ce chapitre doit viser à \(1\) pouvoir reproduire vos expériementations, \(2\) partager/expliquer à d'autres l'usage des outils.

## VI. References

1.

1. 
