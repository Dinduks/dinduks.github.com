---
comments: true
date: 2011-04-19 21:35:27
layout: post
slug: php-tutoriel-pagination-avec-symfony
title: 'PHP: Pagination avec Symfony'
categories:
- Development
- Tutorials
tags:
- php
- symfony
---

Bienvenue,

Dans ce tutoriel je vais vous expliquer comment réaliser une pagination, avec *Symfony* 1.4 et *Doctrine*.

Tout d’abord, supposons qu’on a un module *user* dans l'application *admin*.

### Avant la pagination, côté *action.class.php*

Pour récupérer la liste des utilisateur, il faut exécuter une requête `$qUsers` dans *action.class.php*:

    $qUsers = Doctrine_Query::create()->from("User u");
    $this->aUsers = $qUsers->fetchArray();

Du côté du *template* ça sera ça:

    <table>
      <thead>
        <tr>
          <td><?= __("Nom") ?></td>
          <td><?= __("Prénom") ?></td>
          <td><?= __("Pseudo") ?></td>
          <td><?= __("E-mail") ?></td>
        </tr>
      </thead>
      <tbody>
    <?
    foreach($aUsers as $user) {
    ?>
        <tr>
          <td><?= $user["last_name"] ?></td>
          <td><?= $user["first_name"] ?></td>
          <td><?= $user["pseudo"] ?></td>
          <td><?= $user["email"] ?></td>
        </tr>
    <?
    }
    ?>
      </tbody>
    </table>

### Mise en place de la pagination

Dans *actions.class.php*, juste après notre requête, on doit:

#### Instancier un objet *sfDoctrinePager*

    $this->pager = new sfDoctrinePager('user', 3);

Et lui donner deux paramètres: un nom, et le nombre de résultats à afficher par page.

#### Lui préciser la requête pour récupérer les résultats

Oui, l'objet sfDoctrinePager ne devinera pas ce dont on a besoin, on va donc lui donner notre requête, $qUsers dans notre cas:

    $this->pager->setQuery($qUsers);

#### Lui demander d'afficher la première page par défaut:

    $this->pager->setPage($this->getRequestParameter('page', 1));


#### Initialiser!

    $this->pager->init();

#### Du côté du template

On commence par vérifier si on a besoin de la mise en page, au cas où le nombre des résultats est inférieur au nombre maximum d'éléments par page, 3 dans notre exemple.

    if( $pager->haveToPaginate() ){
    }

Ensuite, on crée un conteneur pour les numéros de pages, et on fait un lien pour aller à la première page, et un autre à la dernière.

    <table>
      <tr>
        <td>
          <a href="<? url_for('user/index?page='.$pager->getFirstPage()) ?>"></a>
        </td>
        <td>
          <a href="<? url_for('user/index?page='.$pager->getLastPage()) ?>"></a>
        </td>
      </tr>
    </table>

Ouais, les `<table>` c'est le mal, mais ce n'est qu'un exemple, et ça m'évite de faire du *CSS*. #jailaflemme

Maintenant, entre les deux liens, on fait un `foreach` pour parser les liens vers les autres pages.

Vous pouvez aussi mettre des liens pour la page précédente, et la page suivante, en utilisant respectivement les méthodes `getPreviousPage()` et `getNextPage()`. ;)

    <? foreach ($pager->getLinks as $page) : ?>
    <td>
      <?php echo ($page == $pager->getPage()) ? $page : "<a href='" . url_for('user/index?page='.$page); "'>". $page ."</a>" ?>
    </td>
    <? endforeach; ?>

Explications:

  * On récupére la liste des liens avec le `foreach`
  * Ensuite on commence à parser les liens
  * A quoi sert la vérification? Tout simplement à ne pas donner de lien au numéro de page sur laquelle on est!

Et voilà, c'est fini.

J'espère que cet article vous a été utile, n'hésitez pas à laisser des commentaire au cas où vous avez des remarques, suggestions, ou corrections. :)


Vous pouvez me suivre sur [**Twitter**](www.dinduks.com/twitter), des tutoriels comme celui ci y en aura encore tant que j'utilise *Symfony*.
