---
comments: true
date: 2011-02-15 21:44:07
layout: post
slug: krumo-une-alternative-a-print_r-et-var_dump
title: 'PHP: Krumo, une alternative à print_r() et var_dump()'
categories:
- Development
- Tutorials
tags:
- krumo
- php
---

*Edit du 24/08/2012: `var_dump()` couplée à Xdebug s'avère plus pratique*

En cherchant un moyen pour afficher `print_r()` avec une mise en page, je suis tombé sur *Krumo*, une classe *PHP* qu'on peut utiliser à la place, et qui offre une mise en page bien plus compréhensible par les humains que nous sommes.

### Présentation

*Krumo* est un remplacement pour `print()` et `var_dump()`. Autrement dit, *Krumo* est un outil de débogage (initialement pour *PHP4*/*PHP5*, maintenant pour *PHP5* seulement), qui affiche les informations d'une variable *PHP* de manière structurée.

Beaucoup de développeurs utilisent `print_r()` et `var_dump()` pour débugger. Bien que ces classes ont été crées pour présenter une varible de façon lisible par l'humain, ce n'est malheureusement pas le cas. *Krumo* est une alternative: elle fait le même travail, mais elle présent l'information plus esthétiquement en utilisant du *CSS* et du *Javascript*.

*Krumo* offre non seulement une présentation plus propre, mais aussi des fonctionnalités intéressantes qu'on verra plutard.

### Téléchargement

Rendez vous sur le site officiel: [Krumo on SourceForge.net](http://kaloyan.info/krumo/index.php#download).  
Ou cliquez sur ce lien pour télécharger la dernière version (15/02/2011): [krumo_0.2.1a_*PHP*5-Only.zip](http://sourceforge.net/projects/krumo/files/krumo/Krumo%200.2.1a%20%28*PHP*5%20Only%29/krumo_0.2.1a_*PHP*5-Only.zip/download).

### Installation

L'installation est simple et classique, il suffit d'extraire le dossier de *Krumo* sur votre serveur et de l'inclure dans votre script (ou *bootstrap*).  
Exemple:

    require_once(dirname(__FILE__) . '/krumo/class.krumo.php');

Notez que vous n'êtes pas obligés de mettre tous les fichiers dans le répertoire _krumo/_, seuls _class.krumo.php_, _krumo.ini_, _krumo.js_ et le dossier _skins/_ sont nécessaires.

### Paramétrage (facultatif)

Vous pouvez jeter un coup d'œil sur _krumo.ini_, pour:

#### Changer de skin

    [ skin ]
        selected = "green"

La valeur de _selected_ doit être le nom d'un sous-dossier du dossier _skins/_.

#### Indiquer le chemin du dossier où Krumo est installé.

    url = "http://www.dinduks.com/Krumo/"

Et cela pour rendre les images des skins accessibles sur le Web.

### Utilisation

Voici un exemple basique:

    krumo(array('a1'=> 'A1', 3, 'rouge'));

Comme vous le remarquez, *Krumo* marche de la même manière que les classes qu'elle est censée remplacer.

Elle peut aussi afficher plusieurs *variables*:

    krumo($_SERVER, $_ENV);

Et possède plusieurs méthodes statiques, par exemple:

    // Équivalent à print_r(debug_backtrace());
    krumo::backtrace();

    // Affiche tous les fichiers inclus (ou requis)
    krumo::includes();

    // Affiche toutes les fonctions incluses
    krumo::functions();

    // Affiche toutes les classes déclarées
    krumo::classes();

    // Affiche toutes les constantes définies
    krumo::defines();

Vous pouvez activer ou désactiver *Krumo* grâce aux méthodes suivantes:

    krumo::enable();
    krumo::disable();

### Exemples

Vous pouvez voir des exemples d'utilisation sur le [site officiel de Krumo](http://krumo.kaloyan.info/#example).

### Conclusion

*Krumo* permet non seulement de mieux présenter les tableaux *PHP*, mais aussi d'accéder à d'autres informations plus facilement, parfois méconnues par les développeurs.  
Pour ma part, cette classe a mérité sa place dans mes dossiers _lib/_.

Je vous invite à le tester et vous faire une idée. ;)

### Liens

Apprenez en plus sur le site et la doc officiels:

* Le site officiel: [http://krumo.sourceforge.net/](http://krumo.sourceforge.net/).
* La documentation de *Krumo*: [http://kaloyan.info/krumo/docs/](http://kaloyan.info/krumo/docs/).
