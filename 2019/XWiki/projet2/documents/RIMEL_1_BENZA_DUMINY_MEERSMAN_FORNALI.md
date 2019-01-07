# Rétro-ingénierie - Livrable 1
<h2><i>Sujet: XWiki</i></h2>
<h2><i>Master 2 IFI - Architecture Logicielle</i></h2>
<h2><i>Authors</i></h2>
<ul>
    <li>BENZA Amandine</li>
    <li>DUMINY Gaétan</li>
    <li>MEERSMAN Rudy</li>
    <li>FORNALI Damien</li>
</ul>

<h3><i>> Question générale</i></h3>

> vous n'êtes pas du tout sur la question ici.


XWiki est un projet open source mature dont le but est de proposer une plateforme générique offrant des services d'exécution pour les applications construites sur cette plateforme.

Nous avons choisi de travailler sur XWiki car nous trouvons le principe d'apporter une solution générique et configurable suivant le client, particulièrement intéressante. Cette solution va permettre au client de XWiki (typiquement une entreprise) d'apporter sa propre base de connaissance ainsi qu'une interface utilisateur optimisée pour ses propres clients. Cette façon d'améliorer l'expérience utilisateur est aussi une caractéristique nous intéressant dans ce sujet.

De plus, le sujet va nous permettre d'analyser la façon dont est testé un code estimé à plusieurs centaines de milliers de lignes et d'éventuellement pouvoir détecter certaines zones n'étants pas couvertes (et donc potentiellement sources de bugs). 

Etudier de manière approfondie un projet de cette taille est donc, pour nous quatre, une expérience nouvelle qui va nous permettre de mieux réaliser la complexité de l'architecture d'une solution logicielle de cette envergure.


<h3><i>> Décomposition du sujet</i></h3>

> ok pour ces questions ... mais pas du tout convaincue apr votre approche.

Le sujet nous fait émettre les questions suivantes:
<ul>
    <li>Quelles sont les solutions d'automatisation de tests déjà existantes ?</li>
    <li>Comment identifier les zones qui manquent de tests et / ou d'automatisation (zones froides / chaudes) ?</li>
    <li>Comment définir quels rapports doit recevoir un collaborateur afin de filtrer seulement les informations qui le concernent ?</li>
</ul>

Afin de répondre à ces questions nous planifions d'utiliser les outils suivants:
    <ul>    
        <li>SonarQube et CodeCity afin d'établir un profiling du code et donc de définir la couverture de test existante, les zones chaudes et froides.<br>
        L'utilisation des deux outils se complète bien puisqu'ils proposent des métriques différentes.<br>
        De plus, CodeCity apporte une visualisation graphique ce qui va nous permettre de rapidement identifier d'éventuels problèmes et / ou manques.
 
 > pas si clair... la couverture de tests ce n'est pas SonarQube et surtout vous n'aurez la couverture que des technologies comprises par SonarQube ou bien je ne vous ai pas compris.
 
    </li>
        <li>Jira propose différentes métriques comme les tickets / incidents levés, résolus ou encore à réaliser. Il nous permettra aussi d'observer (en plus de Github) l'historique du code et extraire certaines informations.</li>
    </ul>

<h3><i>> Démarche prévue</i></h3>
La démarche prévue inclut les points énoncés précédemment.<br>
Nous allons définir certains points sur lesquels nous concentrer. Ces points seront définis selon nos connaissances préalables ainsi que les informations pertinentes que nous allons extraire des articles mentionnés ci-dessous.<br>

Une des approches que nous allons suivre est d'observer attentivement l'évolution du code afin de définir l'automatisation des tests mise en place ainsi que son évolution.<br>

Nous avons de plus pensé à déterminer les zones froides / chaudes du code et identifier la répartition des dépendances afin de définir quels sont les points qui manquent de tests.<br>

<h3><i>> Les 3 articles utilisés comme base</i></h3>
Afin de répondre à la question mentionnée précédemment, nous avons choisi de nous baser sur les trois articles suivants après avoir estimé que leur sujet est en accord avec le notre.<br>

Le premier, se trouvant dans la rubrique générale, est : <i><b>Your Code as a Crime Scene</i></b>, d'Adam Tornhill.<br>

Les 2 autres articles, étants disponibles dans la rubrique étude, sont les suivants :
<ul>
    <li><i><b>Test Case Selection in Industry: an Analysis of Issues Related to Static Approaches</i></b> de Vincent Blondeau, Anne Etien, Nicolas Anquetil, Sylvain Cresson, Pascal Croisy et Stéphane Ducasse.</li>
    <li><i><b>Who Broke the Build? Automatically Identifying Changes That Induce Test Failures In Continuous Integration at Google Scale</i></b> de Celal Ziftci et Jim Reardon.</li>
    
    > j'ai encore du mal à identifier vos questions et je ne peux pas encore vous aider sur les articles.
    > Peut etre : http://sci-hub.tw/10.1109/MALTESQUE.2018.8368456
    > https://www.sciencedirect.com/science/article/pii/S0164121217303060
    
</ul>

