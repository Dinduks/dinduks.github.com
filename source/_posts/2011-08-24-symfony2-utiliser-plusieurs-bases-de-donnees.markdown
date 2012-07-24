---
comments: true
date: 2011-08-24 16:26:15
layout: post
slug: symfony2-utiliser-plusieurs-bases-de-donnees
title: 'Symfony2: Utiliser plusieurs bases de données'
categories:
- Development
- Symfony 2
- Tutorials
tags:
- doctrine
- doctrine2
- php
- symfony
- symfony2
---

Dans le cas où votre site développé avec *Symfony2* utiliserait plusieurs bases de données, il faudra *déclarer* autant de connexions et d'*Entity Managers* que de bases de données.

*Un Entity Manager est tout simplement une interface qui inter-réagi avec une base de donnée*.

Pour illustrer mon exemple, je vais utiliser une bdd *site* et une autre *forum*.

#### Déclarer les connexions dans *config.yml*

    doctrine:
      dbal:
        default_connection: site # précise la connexion utilisée par défaut
        connections:
          site:
            driver:   %database_driver%
            host:     %database_host%
            port:     %database_port%
            dbname:   site
            user:     site_usr
            password: site_pwd
            charset:  UTF8
          forum:
            driver:   %database_driver%
            host:     %database_host%
            port:     %database_port%
            dbname:   forum
            user:     forum_usr
            password: forum_pwd
            charset:  UTF8


#### Déclarer les EM, dans le même fichier

Tout d'abord désactivez l'*auto-mapping*, comme ça vous pourrez choisir quel EM va gérer les entités de quel *bundle*.

    doctrine:
      orm:
        auto_mapping: false

_Note: Si vous avez une erreur relative à cette ligne, supprimez-la carrément._

Ensuite, juste en bas, déclarez les EM en précisant les *mappings* avec chaque bundle. 

    doctrine:
      orm:
        auto_mapping: false
        default_entity_manager: web # précise l'em utilisé par défaut (lors de l'utilisation de la ligne de commande par exemple)
        entity_managers:
          web:
            connection: web
            mappings:
              DinduksMachinBundle : ~
              DinduksTrucBundle : ~
              FOSUserBundle: ~
          forum:
            connection: forum
            mappings:
              DinduksForumBundle : ~

Pour faire simple, les mappings font le lien entre un EM et les entités d'un bundle spéficique. C'est eux qui appellent, si j'ose dire, l'EM X quand on veut manipuler l'entité Y.

Attention: N'oubliez pas de toujours mapper vos bundles fraîchement créés avec un EM, sinon vous aurez un erreur de bundle inexistant lors de l'utilisation de la commande `doctrine:generate:entities`.

#### Utilisation

De la même manière que vous appelez votre EM par défaut, appelez l'EM dont vous avez besoin en prenant soin de passer son nom en paramètres à la fonction `getEntityManager()`.

    $forumEm = $this->get('doctrine')->getEntityManager('forum');

J'espère que ce tutoriel vous sera utile. A bientôt. :)
