---
comments: true
date: 2011-02-03 17:51:57
layout: post
slug: tutoriel-recuperer-le-contenu-dune-page-web-avec-curl
title: 'PHP: Récupérer le contenu d''une page web avec cURL'
categories:
- Development
- Tutorials
tags:
- curl
- php
---

Bonjour,

Je vais à travers ce tutoriel, vous montrer comment utiliser concrètement *cURL* avec *PHP*, en récupérant une description à partir de *Wikipedia*.  
Vous pouvez retrouver le code commenté en bas de l'article.

*cURL* (abréviation de *Client URL Request Library*) est une interface en ligne de commande destinée à récupérer le contenu d'une ressource accessible par un réseau informatique. (source: [*Wikipedia*](http://fr.wikipedia.org/wiki/CURL))

### Installer cURL

Sous *Linux* il suffit d'installer le paquet *_php5-curl_*: `sudo apt-get install php5-curl` pour les distributions dérivées de *Debian*.  
Et de redémarrer *Apache*: `sudo /etc/init.d/apache2 restart`.

Sous *Windows* cURL est disponible avec *WAMP*.  
Il faut cependant l'activer en *décommentant* la ligne `;extension=php_curl.dll` (enlever le point virgule (;) au début de ligne) dans le fichier *php.ini*.

Pour les hébergeur de sites, cURL est activé sur la plupart d'entre eux.

### Récupérer la page

    $wikipediaURL = 'http://fr.wikipedia.org/wiki/Megadeth';
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $wikipediaURL);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
    curl_setopt($ch, CURLOPT_USERAGENT, 'Le blog de Samy Dindane (www.dinduks.com)');
    $resultat = curl_exec ($ch);
    curl_close($ch);

Explications:

* On initialise cURL avec `curl_init();`
* Oui lui fourni l'url de la page à récupérer
* On lui demande de ne retourner la page `curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);`
* On fournit un User Agent avec une description de notre script, pour ne pas être identifié en tant que bot malicieux. (pas obligatoire dans tous les cas)
* On exécute la requête qui nous retourne le contenu de la page dans un tableau.
* Et finalement on ferme la connexion cURL.

Vous pouvez maintenant faire un `echo $resultat;` pour afficher le contenu récupéré.

### Passer des cookies

Au cas où le site source demanderait des cookies, récupérez les (à partir des entêtes HTTP que vous envoie la page), et passez les de cette manière:

    $cookies = "foo=bar";
    curl_setopt($ch, CURLOPT_COOKIE, $cookies);

Jusque là notre variable `$resultat` contient le code *HTML* brut de la page.
Il faut alors récupérer la section qui nous intéresse, et c'est la partie la plus intéressante de ce tutoriel. :)

### Récupérer la description

On va utiliser pour cela la classe *DOMDocument* de *PHP5*.
On instancie un objet DOMDocument et on charge le contenu de la variable $resultat dans cet objet:

    $wikipediaPage = new DOMDocument();
    $wikipediaPage->loadHTML($resultat);

On peut maintenant manipuler `$wikipediaPage` en tant que contenu DOM.  
Il faut tracer notre chemin dans ce labyrinthe de balises, mais avant, jetons un coup d'œil sur le code de notre page Wikipedia.

On remarque que la description se trouve entre les premières balises `<p>` de `<div id="bodyContent">`  
On va alors accéder à cette `<div>` avec un `foreach`:

    foreach($wikipediaPage->getElementsByTagName('div') as $div){
        if($div->getAttribute('id') == "bodyContent"){
        }
    }

Et on récupère le contenu de la fameuse `<p>` dans une variable:

    $description = '<p>' . $div->getElementsByTagName('p')->item(0)->nodeValue. '</p>';

Une petite explication s'impose:

* Avec `foreach` on parcours toutes les balises `<div>`
* Si leur (attribut) `id` est `bodyContent`, on récupère le contenu (`nodeValue`) de la première (`item(0)`) balise `<p>`.

On enlève maintenant la syntaxe propre à Wikipedia, les ancres (\[1\], \[2\]) et les virgules qui les suivent par exemple.

    $description = preg_replace('/\[[0-9]*\][,]|\[[0-9]*\]/', '', $description);

Je précise que cette expression régulière n'est pas définitive et qu'elle est sujette à l'amélioration.

Un `echo $description;` nous affiche la description et confirme que notre script a marché.  
Ici on peut dire que le tutoriel est fini et qu'on a réussi à récupérer notre description. Mais.

Mais que faire s'il y a une `<p>` vide, ou un `<p>` dans la balise `<table>`, avant le `<p>` qui contient la description?  
Il faut qu'on prenne nos précautions et prévoir les mauvaises surprises.

### Prévoir les mauvaises surprises

Et cela en nettoyant $wikipediaPage (rappellez vous, notre object DOMDocument) du contenu indésirable.

Le code suivant doit être placé dans la condition avant la récupération de la description.

On va d'abord s'occuper des `<p>` vides:

    $premierP = trim($div->getElementsByTagName('p')->item(0)->nodeValue);
    while($premierP == '<br>' || $premierP == '<br></br>' || $premierP == ''){
        $div->removeChild($div->getElementsByTagName('p')->item(0));
        $premierP = trim($div->getElementsByTagName('p')->item(0)->nodeValue);
    };

* On travaille sur le contenu du premier `<p>`
* [`trim()`](http://php.net/manual/fr/function.trim.php) enlève les caractères invisibles du début et fin de la chaîne
* Tant que son contenu est vide, ou égal à un retour à la ligne (exemple que j'ai personnellement rencontré)
* On le supprime avec `removeChild()`
* On passe au le `<p>` suivantet ainsi de suite

Au tour des tables qui m'ont posé problème, puisqu'on en a pas besoin dans cet exemple, on va tout simplement les *purger*.

    try{
        foreach( $div->getElementsByTagName('table') as $table ){
            $div->removeChild($table);
        }
    } catch(Exception $e){
    }

La requête est simple, mais pourquoi un try/catch?  
Parce que dans certains cas, l'élément `<table>` n'existe pas et PHP retourne une erreur, erreur dont on peut se passer volontiers.  
(en plus c'est mon premier try/catch en php :D)

Ce guide est terminé et j'espère qu'il vous a été utile. N'oubliez pas que ce n'est qu'un exemple et qu'il faudra le modeler selon vos besoins.  
Je vais de ma part l'améliorer au fur et à mesure que je découvre cURL.

Vous pouvez télécharger le code commenté ici: [Pastebin.com](http://pastebin.com/u2NeMt8k)

N'hésitez pas à laisser vos retours, suggestions ou corrections par commentaire. :)  
Je vous dis à bientôt.
